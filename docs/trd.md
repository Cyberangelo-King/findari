# Findari — Technical Requirements Document

> Stack: React + Node.js + PostgreSQL · Hosted on Vercel + Render/Railway

---

## 1. System Architecture

```
┌─────────────────────────────────────────┐
│              Client (React)              │
│  Vite · React Router · Tailwind CSS     │
│  Hosted: Vercel                         │
└────────────────┬────────────────────────┘
                 │ HTTPS / REST
┌────────────────▼────────────────────────┐
│         API Server (Node.js/Express)    │
│  Auth · Restaurants · Reviews · Users  │
│  Hosted: Render or Railway              │
└──┬──────────┬──────────────┬────────────┘
   │          │              │
   ▼          ▼              ▼
PostgreSQL  Cloudinary   Google Maps API
(Primary DB) (Photo CDN)  (Map embeds)
             Africa's       Mixpanel
             Talking (SMS)  GA4
```

---

## 2. Database Schema

### `users`
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  display_name VARCHAR(80) NOT NULL,
  email VARCHAR(255) UNIQUE NOT NULL,
  phone VARCHAR(20),
  neighbourhood VARCHAR(100),
  is_verified BOOLEAN DEFAULT FALSE,
  is_admin BOOLEAN DEFAULT FALSE,
  avatar_initials VARCHAR(3),
  review_count INT DEFAULT 0,
  avg_rating_given DECIMAL(2,1) DEFAULT 0,
  joined_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);
```

### `restaurants`
```sql
CREATE TABLE restaurants (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name VARCHAR(200) NOT NULL,
  slug VARCHAR(200) UNIQUE NOT NULL,
  neighbourhood VARCHAR(100) NOT NULL,
  cuisine_type VARCHAR(100) NOT NULL,
  price_min INT NOT NULL,           -- in Naira
  price_max INT NOT NULL,           -- in Naira
  address TEXT,
  phone VARCHAR(20),
  description TEXT,
  cover_photo_url TEXT,
  lat DECIMAL(9,6),
  lng DECIMAL(9,6),
  hours JSONB,                      -- { mon: {open: "09:00", close: "22:00"}, ... }
  avg_rating DECIMAL(2,1) DEFAULT 0,
  avg_food DECIMAL(2,1) DEFAULT 0,
  avg_service DECIMAL(2,1) DEFAULT 0,
  avg_ambience DECIMAL(2,1) DEFAULT 0,
  review_count INT DEFAULT 0,
  profile_view_count INT DEFAULT 0,
  is_claimed BOOLEAN DEFAULT FALSE,
  is_active BOOLEAN DEFAULT TRUE,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);
```

### `reviews`
```sql
CREATE TABLE reviews (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  restaurant_id UUID REFERENCES restaurants(id) ON DELETE CASCADE,
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  overall_rating INT CHECK (overall_rating BETWEEN 1 AND 5) NOT NULL,
  food_rating INT CHECK (food_rating BETWEEN 1 AND 5),
  service_rating INT CHECK (service_rating BETWEEN 1 AND 5),
  ambience_rating INT CHECK (ambience_rating BETWEEN 1 AND 5),
  review_text TEXT NOT NULL,
  visit_date DATE,
  photo_urls JSONB DEFAULT '[]',    -- array of Cloudinary URLs
  is_flagged BOOLEAN DEFAULT FALSE,
  is_removed BOOLEAN DEFAULT FALSE,
  flag_reason VARCHAR(100),
  owner_response TEXT,
  owner_responded_at TIMESTAMP,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  UNIQUE(restaurant_id, user_id)    -- one review per restaurant per user
);
```

### `saved_spots`
```sql
CREATE TABLE saved_spots (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  restaurant_id UUID REFERENCES restaurants(id) ON DELETE CASCADE,
  saved_at TIMESTAMP DEFAULT NOW(),
  UNIQUE(user_id, restaurant_id)
);
```

### `business_claims`
```sql
CREATE TABLE business_claims (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  restaurant_id UUID REFERENCES restaurants(id),
  claimant_email VARCHAR(255) NOT NULL,
  claimant_phone VARCHAR(20),
  cac_number VARCHAR(50),
  status VARCHAR(20) DEFAULT 'pending', -- pending | approved | rejected
  reviewed_by UUID REFERENCES users(id),
  reviewed_at TIMESTAMP,
  created_at TIMESTAMP DEFAULT NOW()
);
```

### `otp_verifications`
```sql
CREATE TABLE otp_verifications (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) NOT NULL,
  otp_code VARCHAR(6) NOT NULL,
  expires_at TIMESTAMP NOT NULL,
  is_used BOOLEAN DEFAULT FALSE,
  created_at TIMESTAMP DEFAULT NOW()
);
```

---

## 3. API Endpoints

### Auth
```
POST /api/auth/send-otp          - Send OTP to email
POST /api/auth/verify-otp        - Verify OTP, create/login user
POST /api/auth/logout             - Invalidate session
GET  /api/auth/me                 - Get current user
```

### Restaurants
```
GET  /api/restaurants             - List/search restaurants
     ?q=           (search query)
     ?neighbourhood=
     ?cuisine=
     ?open_now=true
     ?price_min=&price_max=
     ?sort=rating|recent|name
     ?page=&limit=

GET  /api/restaurants/:slug       - Get single restaurant profile
POST /api/restaurants             - Create restaurant (admin only)
PUT  /api/restaurants/:id         - Update restaurant (admin or claimed owner)
GET  /api/restaurants/:id/views   - Log a profile view (anonymous)
```

### Reviews
```
GET  /api/restaurants/:id/reviews   - Get all reviews for a restaurant
POST /api/restaurants/:id/reviews   - Post a new review (auth required)
PUT  /api/reviews/:id               - Edit own review (within 24h)
POST /api/reviews/:id/flag          - Flag a review as inappropriate
POST /api/reviews/:id/respond       - Business owner responds to review
DELETE /api/reviews/:id             - Remove review (admin only)
```

### Users
```
GET  /api/users/:id               - Get public user profile
PUT  /api/users/me                - Update own profile
GET  /api/users/me/reviews        - Get own review history
GET  /api/users/me/saved          - Get saved spots list
POST /api/users/me/saved/:restId  - Save a restaurant
DELETE /api/users/me/saved/:restId - Unsave a restaurant
```

### Business
```
POST /api/business/claim/:restId  - Submit claim for a restaurant
GET  /api/business/dashboard      - Business owner dashboard data
PUT  /api/business/listing        - Update claimed listing info
```

### Admin
```
GET  /api/admin/claims            - List pending business claims
PUT  /api/admin/claims/:id        - Approve or reject a claim
GET  /api/admin/flagged-reviews   - List flagged reviews
DELETE /api/admin/reviews/:id     - Remove a review
POST /api/admin/restaurants/seed  - Bulk import restaurants
```

---

## 4. Photo Upload Flow

1. Client requests a signed Cloudinary upload URL from backend
2. Client uploads image directly to Cloudinary (bypasses server)
3. Cloudinary returns image URL
4. Client includes URL in review submission payload

**Constraints:**
- Max file size: 5MB per image
- Max 5 images per review
- Accepted types: JPEG, PNG, WebP
- Transform on upload: resize to max 1200px wide, compress to 80% quality

---

## 5. Open Now Logic

```javascript
function isOpenNow(hours, timezone = 'Africa/Lagos') {
  const now = new Date().toLocaleString('en-US', { timeZone: timezone });
  const date = new Date(now);
  const dayNames = ['sun', 'mon', 'tue', 'wed', 'thu', 'fri', 'sat'];
  const today = dayNames[date.getDay()];
  const todayHours = hours[today];
  if (!todayHours || todayHours.closed) return false;
  const currentMinutes = date.getHours() * 60 + date.getMinutes();
  const [openH, openM] = todayHours.open.split(':').map(Number);
  const [closeH, closeM] = todayHours.close.split(':').map(Number);
  const openMinutes = openH * 60 + openM;
  const closeMinutes = closeH * 60 + closeM;
  return currentMinutes >= openMinutes && currentMinutes < closeMinutes;
}
```

---

## 6. Rating Aggregation

When a new review is posted or updated, recalculate restaurant averages:

```sql
UPDATE restaurants SET
  avg_rating = (SELECT AVG(overall_rating) FROM reviews WHERE restaurant_id = $1 AND is_removed = FALSE),
  avg_food = (SELECT AVG(food_rating) FROM reviews WHERE restaurant_id = $1 AND food_rating IS NOT NULL AND is_removed = FALSE),
  avg_service = (SELECT AVG(service_rating) FROM reviews WHERE restaurant_id = $1 AND service_rating IS NOT NULL AND is_removed = FALSE),
  avg_ambience = (SELECT AVG(ambience_rating) FROM reviews WHERE restaurant_id = $1 AND ambience_rating IS NOT NULL AND is_removed = FALSE),
  review_count = (SELECT COUNT(*) FROM reviews WHERE restaurant_id = $1 AND is_removed = FALSE),
  updated_at = NOW()
WHERE id = $1;
```

---

## 7. Security

- All API routes require CORS whitelist (frontend domain only)
- JWT tokens for session management (7-day expiry, refreshed on activity)
- OTP codes expire after 10 minutes
- Rate limit on OTP endpoint: 3 requests per email per hour
- Rate limit on review creation: 5 reviews per user per day
- Cloudinary URLs signed; direct upload only via pre-signed token
- Business claim verification is manual (admin-reviewed, not automated)
- All user inputs sanitised before database write
- SQL queries use parameterised statements only — no string interpolation

---

## 8. Environment Variables

```env
DATABASE_URL=postgresql://...
JWT_SECRET=...
CLOUDINARY_CLOUD_NAME=...
CLOUDINARY_API_KEY=...
CLOUDINARY_API_SECRET=...
GOOGLE_MAPS_API_KEY=...
SMTP_HOST=...
SMTP_USER=...
SMTP_PASS=...
AFRICAS_TALKING_API_KEY=...
AFRICAS_TALKING_USERNAME=...
MIXPANEL_TOKEN=...
NODE_ENV=production
PORT=3000
```
