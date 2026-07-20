# Findari — Post-AI-Studio Guide

> What to do after Google AI Studio has generated your screens.
> This guide takes you from a folder of HTML files all the way to a live, real web application with real users.

---

## Where You'll Be After AI Studio

After completing all AI Studio sessions, you will have:
- ✅ 5–7 HTML files (one per screen) with embedded CSS and JavaScript
- ✅ A consistent visual design that matches the wireframes
- ✅ Working interactive elements (star selector, photo upload, navigation)
- ✅ Realistic sample data hardcoded into the templates

What you will **not** have:
- ❌ A real database — restaurant data is hardcoded
- ❌ Real user accounts — "logged in" state is faked with localStorage
- ❌ Real photo uploads — Cloudinary is not yet connected
- ❌ Real OTP auth — the OTP form submits but goes nowhere
- ❌ A live URL — the files only exist on your computer

This guide closes that gap. Work through it in order.

---

## Phase 1: Clean Up and Consolidate (1–2 days)

Before connecting anything, clean up what AI Studio produced.

### Step 1.1 — Organise your files
Create this folder structure on your computer:
```
findari/
├── index.html           ← Home screen
├── restaurant.html      ← Restaurant profile
├── write-review.html    ← Review form
├── profile.html         ← User profile
├── dashboard.html       ← Business dashboard
├── auth.html            ← OTP signup/login
├── claim.html           ← Business claim flow
├── css/
│   └── styles.css       ← All CSS pulled out of HTML files
├── js/
│   └── app.js           ← All JavaScript pulled out of HTML files
└── assets/
    └── icons/           ← Any SVG icons or images
```

### Step 1.2 — Extract CSS into one shared file
Go through every HTML file. Cut all `<style>` block contents and paste them into `css/styles.css`. Add `<link rel="stylesheet" href="css/styles.css">` to every HTML file's `<head>`. This prevents CSS drift between screens.

### Step 1.3 — Extract JavaScript into one shared file
Same process for JavaScript. Cut all `<script>` block contents into `js/app.js`. Add `<script src="js/app.js" defer></script>` to every HTML file's `<body>`.

### Step 1.4 — Test every screen locally
Open each HTML file in Chrome. For every screen:
- Resize to 375px (iPhone SE) using DevTools
- Test every button, link, and interactive element
- Write down anything that's broken — fix these before moving on

### Step 1.5 — Final AI Studio clean-up session (optional but recommended)
Paste all your CSS into one final AI Studio session and say:
*"Review this CSS file. Remove duplicate rules, consolidate overlapping selectors, and ensure every CSS variable reference matches the `:root` definitions at the top. Return the cleaned file."*

---

## Phase 2: Choose Your Backend Path (Decision Day)

You have three options. Choose one before writing a single line of backend code.

---

### Option A: Supabase (Recommended for solo builders)

**What it is:** A hosted PostgreSQL database with a built-in REST API, authentication, file storage, and a dashboard to manage data. You write almost no backend code.

**Why choose this:** You can go from static HTML files to a working app with real data in 3–5 days without writing a Node.js server. Supabase handles auth (including OTP), database, and file storage (replaces Cloudinary).

**Cost:** Free tier is generous — up to 500MB database, 1GB file storage, 50,000 monthly active users. More than enough for MVP.

**How Findari maps to Supabase:**

| Findari need | Supabase solution |
|---|---|
| PostgreSQL database | Supabase Database (paste the schema from `trd.md` directly) |
| Email OTP auth | Supabase Auth → Email OTP (built-in, zero config) |
| Photo uploads | Supabase Storage (replace Cloudinary) |
| REST API | Supabase auto-generates a REST API for all your tables |
| Real-time updates | Supabase Realtime (reviews appear without page refresh) |

**To connect your HTML files to Supabase:**
1. Create a project at [supabase.com](https://supabase.com)
2. Go to SQL Editor → paste the schema from `trd.md` → run it
3. Add the Supabase JavaScript client to each HTML file:
   ```html
   <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
   ```
4. Initialise the client:
   ```javascript
   const supabase = window.supabase.createClient(
     'https://YOUR_PROJECT_REF.supabase.co',
     'YOUR_ANON_PUBLIC_KEY'
   );
   ```
5. Replace hardcoded restaurant cards with a real query:
   ```javascript
   const { data: restaurants, error } = await supabase
     .from('restaurants')
     .select('*')
     .order('avg_rating', { ascending: false })
     .limit(10);
   ```
6. Replace the hardcoded OTP form with Supabase Auth:
   ```javascript
   // Send OTP
   await supabase.auth.signInWithOtp({ email: userEmail });

   // Verify OTP
   await supabase.auth.verifyOtp({ email: userEmail, token: otpCode, type: 'email' });
   ```

**Estimated time to connect all screens:** 5–10 days if you're learning as you go.

---

### Option B: Build the Node.js backend yourself

**What it is:** Build the API server described in `trd.md` yourself using Node.js + Express + PostgreSQL.

**Why choose this:** Full control. Easier to extend. Better for a long-term product.

**Why it takes longer:** You need to set up the server, connect the database, handle OTP emails, configure Cloudinary, write all the API routes, handle errors, and deploy everything separately.

**Estimated time:** 3–6 weeks if you're an experienced developer. 2–4 months if you're learning.

**If you choose this path:**
- Follow the API endpoints in `trd.md` exactly
- Use the database schema in `trd.md` to set up PostgreSQL (Railway or Neon.tech both offer free hosted Postgres)
- Use Nodemailer or Resend for OTP emails
- Use Africa's Talking for SMS OTP (Nigerian numbers)
- Deploy to Render (free tier available, auto-deploys from GitHub)

---

### Option C: Hybrid — Supabase for data + Node.js for complex logic

**What it is:** Use Supabase for database, auth, and storage. Add a small Node.js server only for things Supabase can't handle natively (e.g. complex moderation logic, aggregated reports).

**Why choose this:** Gets you live fast. Lets you add custom backend logic incrementally.

**Recommendation:** Start with Option A (Supabase only). Add a Node.js layer later if you hit a wall.

---

## Phase 3: Database Setup (1 day)

Whichever backend path you chose, set up the database first.

### Step 3.1 — Create the database
If using Supabase: create a new project, go to SQL Editor, paste and run the schema from `trd.md`.
If using Railway/Neon: create a new PostgreSQL instance, connect via psql or the web UI, run the schema.

### Step 3.2 — Seed initial data
You need data before you can test anything. Run this SQL to add a few test restaurants:
```sql
INSERT INTO restaurants (name, slug, neighbourhood, cuisine_type, price_min, price_max, hours, lat, lng)
VALUES
  ('Mama Titi''s Kitchen', 'mama-titis-kitchen', 'Jabi', 'Local Nigerian', 1500, 4000,
   '{"mon":{"open":"09:00","close":"22:00"},"tue":{"open":"09:00","close":"22:00"},"wed":{"open":"09:00","close":"22:00"},"thu":{"open":"09:00","close":"22:00"},"fri":{"open":"09:00","close":"22:00"},"sat":{"open":"10:00","close":"22:00"},"sun":{"closed":true}}',
   9.0579, 7.4951),
  ('Bukka Hut Wuse 2', 'bukka-hut-wuse-2', 'Wuse 2', 'Local Nigerian', 1000, 3000, NULL, 9.0765, 7.4898),
  ('Zinc Café Maitama', 'zinc-cafe-maitama', 'Maitama', 'Café', 2000, 5000, NULL, 9.0840, 7.4916),
  ('Abuja Suya Spot', 'abuja-suya-spot', 'Garki', 'Suya / Grills', 800, 2000, NULL, 9.0488, 7.4849);
```

### Step 3.3 — Test queries
Before writing frontend code, verify the database works:
```sql
SELECT id, name, neighbourhood, avg_rating FROM restaurants;
```
If you get rows back, you're ready.

---

## Phase 4: Connect the Frontend (5–10 days)

Replace hardcoded data with real data, one screen at a time.

### Screen 1: Home — Connect restaurant list
Replace the hardcoded restaurant cards with a live query. The card HTML stays the same — you're just changing where the data comes from.

```javascript
async function loadRestaurants(neighbourhood = null) {
  let query = supabase.from('restaurants').select('*').eq('is_active', true);
  if (neighbourhood) query = query.eq('neighbourhood', neighbourhood);
  const { data } = await query.order('avg_rating', { ascending: false }).limit(20);
  renderRestaurantCards(data);
}

function renderRestaurantCards(restaurants) {
  const container = document.getElementById('restaurant-list');
  container.innerHTML = restaurants.map(r => `
    <a href="restaurant.html?id=${r.id}" class="resto-card">
      <div class="resto-thumb">...</div>
      <div class="resto-info">
        <div class="name">${r.name}</div>
        <div class="stars">${renderStars(r.avg_rating)}</div>
        <div class="meta">${r.cuisine_type} · ${r.neighbourhood}
          <span class="price">· ₦${r.price_min.toLocaleString()}–₦${r.price_max.toLocaleString()}</span>
        </div>
      </div>
    </a>
  `).join('');
}
```

### Screen 2: Restaurant Profile — Load from URL param
```javascript
const params = new URLSearchParams(window.location.search);
const restaurantId = params.get('id');

const { data: restaurant } = await supabase
  .from('restaurants')
  .select('*, reviews(*)')
  .eq('id', restaurantId)
  .single();
```

### Screen 3: Write a Review — Submit to database
```javascript
document.getElementById('post-review-btn').addEventListener('click', async () => {
  const { data: { user } } = await supabase.auth.getUser();
  if (!user) { showSignupPrompt(); return; }

  const { error } = await supabase.from('reviews').insert({
    restaurant_id: restaurantId,
    user_id: user.id,
    overall_rating: selectedRating,
    food_rating: foodRating,
    service_rating: serviceRating,
    ambience_rating: ambienceRating,
    review_text: reviewText,
    photo_urls: uploadedPhotoUrls
  });

  if (!error) {
    showToast('Your review is live!');
    window.location.href = `restaurant.html?id=${restaurantId}`;
  }
});
```

---

## Phase 5: Deploy to a Live URL (1 day)

### Step 5.1 — Push to GitHub
If your files aren't in GitHub yet:
```bash
cd findari
git init
git add .
git commit -m "Initial frontend build"
git remote add origin https://github.com/Cyberangelo-King/findari.git
git push -u origin main
```

### Step 5.2 — Deploy frontend to Vercel
1. Go to [vercel.com](https://vercel.com) and sign in with GitHub
2. Click "New Project" → import `Cyberangelo-King/findari`
3. Set framework to "Other" (since it's plain HTML, not a framework build)
4. Click Deploy
5. Your site is live at `findari.vercel.app` within 60 seconds
6. Every `git push` to main auto-deploys — no manual steps needed

### Step 5.3 — Add environment variables
In Vercel → Project Settings → Environment Variables, add:
```
SUPABASE_URL=https://YOUR_PROJECT_REF.supabase.co
SUPABASE_ANON_KEY=YOUR_ANON_PUBLIC_KEY
GOOGLE_MAPS_KEY=YOUR_MAPS_API_KEY
```

### Step 5.4 — Custom domain (optional but recommended)
1. Buy `findari.ng` or `abujaeat.ng` from a Nigerian registrar (Whogohost, Qservers, or Namecheap)
2. In Vercel → Domains → Add domain → follow DNS instructions
3. Vercel provisions HTTPS automatically

---

## Phase 6: Seed 100 Restaurants Before Launch (3–5 days)

You need 100+ listings before you open to the public.

### How to research restaurants efficiently
1. Open Google Maps → search "restaurants in Wuse 2 Abuja" → collect names, addresses, price indications
2. Check each restaurant's Instagram page for photos and hours
3. Use Zomato Nigeria (if available) for structured data
4. Build a Google Sheet with columns: Name, Neighbourhood, Cuisine, Price Min (₦), Price Max (₦), Phone, Hours

### Bulk import via Supabase
Once your spreadsheet has 100+ rows, export as CSV and import directly:
- Supabase Dashboard → Table Editor → restaurants → Import CSV
- Or write a Node.js script that reads the CSV and inserts rows via the Supabase client

### Minimum data per restaurant
Every listing needs before going live:
- ✅ Name
- ✅ Neighbourhood (must match a chip on the home screen)
- ✅ Cuisine type
- ✅ Price range (₦ min and ₦ max)
- ❌ Hours are optional at launch (Open Now just won't appear)
- ❌ Phone is optional
- ❌ Cover photo is optional (show placeholder)

---

## Phase 7: Pre-Launch Checklist

Complete every item before sharing the URL publicly.

### Legal
- [ ] Privacy policy page live at `/privacy`
- [ ] Terms of service page live at `/terms`
- [ ] NDPR consent checkbox on signup form
- [ ] "Delete my account" option reachable from settings

### Technical
- [ ] All 5 main screens work on mobile (375px)
- [ ] All 5 main screens work on desktop (1024px)
- [ ] Real OTP auth works end to end (send code → receive email → enter code → logged in)
- [ ] Review submission saves to database
- [ ] Photos upload to Cloudinary or Supabase Storage
- [ ] Open Now displays correctly (test a restaurant with today's hours set to closed)
- [ ] No broken links between screens
- [ ] 404 page exists

### Data
- [ ] 80–100 restaurant listings in database
- [ ] At least 5 restaurants with hours set (to demonstrate Open Now)
- [ ] At least 10 restaurants have a cover photo

### Performance
- [ ] Lighthouse Performance score ≥ 70 on mobile (Chrome DevTools → Lighthouse → Mobile)
- [ ] Pages load in ≤ 5 seconds on 3G (simulate in Chrome DevTools → Network → Slow 3G)
- [ ] Images are compressed (max 200KB per image)

### Analytics
- [ ] Google Analytics 4 tag installed on every page
- [ ] Mixpanel or PostHog event tracking installed (optional but recommended)
- [ ] Verify events firing: page_view, review_submitted, restaurant_viewed, user_registered

---

## Phase 8: Soft Launch Strategy (Week 1)

Do not blast the link everywhere on day one. Soft launch first.

### Day 1–3: Internal testing
- Share with 5–10 trusted friends in Abuja
- Ask them to: find a restaurant they know, check if the info is accurate, leave a review
- Collect feedback — fix critical issues before wider launch

### Day 4–7: Closed beta
- Share in 3–5 Abuja-specific WhatsApp or Telegram groups (food groups, professional groups)
- Post in Abuja Facebook groups: "We're building a restaurant review app for Abuja — give us honest feedback"
- Target: 50 users, 20 reviews

### Week 2: Soft public launch
- Post on your personal Instagram, Twitter/X
- DM 20 Abuja food influencer accounts with the link and ask for a shoutout in exchange for a free "featured listing" badge
- Target: 200 users, 50 reviews

### Week 3+: Growth
- Reach out to restaurants directly — tell them they're listed, offer them the claim flow
- Consistent social posting — one "Best of [neighbourhood]" post per week highlighting top-rated spots

---

## Tools Summary

| Need | Tool | Cost |
|---|---|---|
| Frontend hosting | Vercel | Free |
| Backend / Database | Supabase | Free (up to 500MB) |
| File/photo storage | Supabase Storage | Free (up to 1GB) |
| Email OTP | Supabase Auth | Free |
| SMS OTP (backup) | Africa's Talking | Pay per SMS (~₦3–5) |
| Maps | Google Maps API | Free up to 28k loads/mo |
| Domain | Whogohost or Namecheap | ₦8,000–₦20,000/year |
| Analytics | Google Analytics 4 | Free |
| Error monitoring | Sentry (free tier) | Free |
| **Total MVP cost** | | **~₦20,000/year** |
