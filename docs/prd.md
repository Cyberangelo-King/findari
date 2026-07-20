# Findari (Abuja Eats) — Product Requirements Document

> Version 1.0 · Phase 2: Planning & Design · Prepared by Zia the Creator · June 2026

---

## 1. Product Overview

### 1.1 Product Name
**Findari** (formerly Abuja Eats)

### 1.2 One-Line Description
Abuja's first dedicated platform for discovering, rating, and reviewing local restaurants, bukas, cafés, and food spots — built by Abuja people, for Abuja people.

### 1.3 The Problem
Abuja residents have no reliable, centralised place to find honest reviews of local food spots before spending their money. People currently rely on fragmented word-of-mouth, Instagram posts, and WhatsApp group chats — all of which are unsearchable, unverified, and inconsistent.

**Survey data (17 respondents, June 2026):**
- 94% said they would use a dedicated Abuja food review app
- 47% said their #1 frustration is not knowing if quality is consistent
- 58.8% currently rely on word of mouth to discover new restaurants
- 94% have been disappointed by a restaurant they had no prior information about

### 1.4 The Solution
Findari is a web-based platform where users can:
- Search for any restaurant or food spot in Abuja
- Read verified reviews from real customers
- See accurate price ranges in Naira
- Browse real customer photos
- Leave their own verified reviews
- Businesses can claim their listings and respond to feedback

### 1.5 Vision Statement
To become the most trusted food discovery platform in Abuja — and eventually all of Nigeria — by championing authentic Nigerian food culture and giving every diner the information they need before they walk through the door.

---

## 2. Target Users

### 2.1 Primary User — The Diner (Reviewer)

| Attribute | Detail |
|---|---|
| Age | 25–34 years old (70.6% of survey respondents) |
| Location | Wuse/Wuse 2, Jabi/Utako, Guzape/Asokoro |
| Behaviour | Eats out regularly; research-oriented before spending |
| Motivation | Honest, current info on food quality, price, and service |
| Current habit | Asks friends, checks Instagram, uses Google Maps |
| Pain point | Has been disappointed multiple times with no way to have known |

### 2.2 Secondary User — The Business Owner

| Attribute | Detail |
|---|---|
| Who | Restaurant owners, buka operators, café managers, suya spot vendors |
| Motivation | Visibility, review responses, and listing control |
| Pain point | No dedicated Nigerian platform to manage reputation |
| Value offered | Free listing claim, review responses, profile management, optional paid promotion |

---

## 3. Feature Requirements

Priority key: 🔴 Must Have (MVP) · 🟡 Important, build early · 🟢 Nice to have (later)

### 3.1 Core Features — Diner

| Feature | Description | Survey Signal | Priority |
|---|---|---|---|
| Price Range Display | Every listing shows ₦ price range per person | 88.2% said this is most important | 🔴 |
| Verified Review System | Accounts must verify before reviewing; reviews flagged as verified | 82.4% cited this as #1 trust factor | 🔴 |
| Search by Neighbourhood | Filter by Abuja area (Wuse, Jabi, Maitama, Guzape, etc.) | 64.7% requested | 🔴 |
| Photo Uploads on Reviews | Up to 5 photos per review | 52.9% said photos are key trust signal | 🔴 |
| Open Now Indicator | Shows if currently open based on listed hours | Independent survey + open text | 🔴 |
| Star Rating System | 1–5 stars on Food, Service, and Ambience separately | 35.3% requested breakdown | 🔴 |
| Review Recency Display | Date of each review shown prominently | 47% cite inconsistency as #1 frustration | 🔴 |
| Save Favourite Spots | Bookmark restaurants to a personal saved list | 47.1% requested | 🟡 |
| Filter by Cuisine Type | Filter by food type (Nigerian, Chinese, Continental, etc.) | General usability | 🟡 |
| See Friends' Reviews | See what contacts have reviewed and rated | 29.4% requested | 🟢 |

### 3.2 Core Features — Business Owner

| Feature | Description | Priority |
|---|---|---|
| Free Listing Claim | Owners claim auto-generated listing and verify ownership | 🔴 |
| Review Response | Owners publicly respond to any review | 🟡 |
| Listing Management | Update address, hours, price range, photos, description, phone | 🔴 |
| Business Dashboard | Profile views, avg rating, review count, recent activity | 🟡 |
| Promoted Listing | Paid placement at top of neighbourhood results | 🟢 (V2) |

### 3.3 Platform & Infrastructure

| Feature | Description | Priority |
|---|---|---|
| User Registration & Login | Email signup with OTP verification; optional Google sign-in | 🔴 |
| Restaurant Profile Page | Name, address, area, cuisine, price, hours, photos, reviews | 🔴 |
| Home / Search Screen | Search bar + browse by neighbourhood + trending spots | 🔴 |
| Review Flagging System | Flag reviews as fake, irrelevant, or abusive | 🔴 |
| Google Maps Integration | Map on every profile showing exact location | 🔴 |
| Photo Storage | Cloud storage for user-uploaded photos | 🔴 |
| Mobile-Responsive Design | Fully functional on mobile browsers | 🔴 |

---

## 4. Out of Scope for MVP

- Native iOS/Android app — web first, mobile after traction
- Food delivery integration — review platform only
- In-app reservations or bookings — Phase 2
- Paid promoted listings — after sufficient user base
- AI-powered recommendations — too complex for MVP
- Video reviews — 17.6% demand; deprioritised for v1
- Lagos / other city expansion — after Abuja is proven

---

## 5. User Journeys

### 5.1 Reviewer Journey

| Step | Action |
|---|---|
| 1 | Discovers Findari via social media, friend recommendation, or Google |
| 2 | Lands on homepage — sees search bar and browse-by-neighbourhood |
| 3 | Searches for a restaurant or browses their area (e.g. Jabi) |
| 4 | Opens restaurant profile — reads reviews, checks price, sees photos and open hours |
| 5 | Decides to leave a review — prompted to create an account if not logged in |
| 6 | Verifies account via OTP sent to email or phone |
| 7 | Rates (Food / Service / Ambience), writes review, uploads photos |
| 8 | Review goes live — profile shows their review history |
| 9 | Returns next time they want to find or review a food spot |

### 5.2 Business Owner Journey

| Step | Action |
|---|---|
| 1 | Discovers their restaurant is already listed (via customer, social, or search) |
| 2 | Visits platform and finds their listing |
| 3 | Clicks 'Claim This Business' — submits verification (CAC, phone, or email) |
| 4 | Gains access to business dashboard after verification |
| 5 | Updates listing: address, hours, price range, description, and photos |
| 6 | Reads existing reviews and responds publicly |
| 7 | Monitors dashboard for new reviews, rating trends, and profile views |

---

## 6. Non-Functional Requirements

### Performance
- Pages must load within 3 seconds on standard Nigerian mobile data
- Search results must return within 2 seconds

### Mobile Experience
- Fully functional on mobile browsers — primary access device
- All buttons, inputs, and forms must be thumb-friendly on small screens

### Trust & Safety
- All reviewer accounts must go through OTP verification before posting
- Flagged reviews reviewed by admin within 48 hours
- No anonymous reviews allowed

### Data Accuracy
- Price ranges in Nigerian Naira (₦) only
- 'Open Now' calculated from business-provided hours, not estimated
- All listings must have at minimum: name, neighbourhood, cuisine type, price range before going live

### Legal
- Privacy policy and terms of service live before public launch
- Defamatory review policy documented and enforced
- NDPR (Nigeria Data Protection Regulation) compliance required

---

## 7. Success Metrics

| Metric | Target |
|---|---|
| Listings at launch | 100+ Abuja restaurants seeded in the database |
| 30-day users | 500 unique visitors |
| Reviews written | 200 reviews posted in first 60 days |
| Return visits | 30% of users return within 2 weeks |
| Business claims | 20 restaurants claim listing within 90 days |
| SEO | Rank for 'Abuja restaurants review' on Google |
| Social sharing | Reviews shared on social without prompting |

---

## 8. Technical Decisions

| Decision | Choice |
|---|---|
| Platform type | Web app (mobile-responsive) — native app deferred |
| Build approach | React + Node.js + PostgreSQL OR Bubble.io (pending budget) |
| Hosting | Vercel (frontend) + Railway or Render (backend) |
| Photo storage | Cloudinary — free tier covers MVP needs |
| Maps | Google Maps API |
| Authentication | Email OTP for reviewers; manual verification for business owners |
| Analytics | Google Analytics + Mixpanel |

---

## 9. Open Questions

1. Build with a developer or use Bubble.io no-code? Budget determines this.
2. Business owner verification method — CAC number, phone call, or email domain?
3. Who manages review moderation early on — founder manually or automated flagging?
4. Is 'Findari' the final name, or is 'Abuja Eats' still in consideration?
5. Mobile app companion from day one, or strictly web-first?

---

## 10. Phase Timeline

| Phase | Description | Timeline |
|---|---|---|
| Phase 1 | Research & Validation | Complete ✅ |
| Phase 2 | Planning & Design | Weeks 5–8 (current) |
| Phase 3 | Build MVP | Months 2–5 |
| Phase 4 | Testing | Months 5–6 |
| Phase 5 | Launch | Months 6–7 |
| Phase 6 | Growth | Month 7+ |
