# Findari — Master Build Prompt

> Entry point for building with Google Stitch / Google AI Studio / any AI-assisted dev environment.
> Read this file first. It references all other docs in this folder.

---

## What You Are Building

**Findari** (formerly Abuja Eats) is a mobile-first web platform for discovering, rating, and reviewing restaurants and food spots in Abuja, Nigeria. It is a review-and-discovery product — not a delivery app, not a booking platform. Think Yelp, built specifically for the Abuja food scene.

**Tech stack:**
- Frontend: React (Vite) — mobile-first, responsive
- Backend: Node.js + Express
- Database: PostgreSQL
- Auth: Email OTP (Nodemailer/Africa's Talking) + optional Google OAuth
- Photos: Cloudinary
- Maps: Google Maps API
- Hosting: Vercel (frontend) + Render or Railway (backend)
- Analytics: Google Analytics 4 + Mixpanel

---

## Reference Documents

Read these in order before generating any code:

| File | Purpose |
|---|---|
| `prd.md` | Full product requirements — features, priorities, user journeys |
| `features-and-functions.md` | Detailed feature breakdown by screen and user type |
| `trd.md` | Database schema, API endpoints, technical architecture |
| `design.md` | Layout, screen-by-screen UI design, component structure |
| `style.md` | Design tokens, color system, typography, spacing, CSS |
| `copy.md` | All UI text — labels, headlines, CTAs, error messages, emails |
| `user-workflow.md` | Step-by-step user flows for reviewer and business owner |
| `goals.md` | Product and business goals, success metrics |
| `brand.md` | Visual identity, logo, color palette, personality |

---

## Build Instructions

### Phase 1 — Foundation
1. Set up React + Vite project with React Router
2. Configure Tailwind CSS with the design tokens from `style.md`
3. Set up PostgreSQL with the schema from `trd.md`
4. Set up Node.js + Express backend with all API routes from `trd.md`
5. Configure Cloudinary for photo uploads
6. Configure Google Maps API
7. Set up email OTP authentication flow

### Phase 2 — Core Screens (build in this order)
1. **Home / Search** — search bar + neighbourhood chips + restaurant card list
2. **Restaurant Profile** — hero image, stats, open/closed badge, rating breakdown, review list, map
3. **Write a Review** — star rating (overall + food/service/ambience), text input, photo upload (up to 5)
4. **User Profile** — avatar, stats (reviews / saved / avg rating), review history, saved spots
5. **Business Dashboard** — metrics grid, review response interface, edit listing button

### Phase 3 — Auth & Verification
1. Email signup with OTP
2. Phone OTP via Africa's Talking (Nigerian SMS)
3. Business owner claim flow (manual verification queue)

### Phase 4 — Polish & Launch Prep
1. Google Maps embed on restaurant profiles
2. 'Open Now' status from business hours
3. Review flagging system
4. Admin moderation queue
5. Privacy policy + terms of service pages
6. NDPR compliance banner

---

## Key Constraints

- **Mobile-first always.** Most Abuja users are on mobile. Design for 375px first, scale up.
- **Price in Naira only.** All price ranges displayed as ₦X,XXX–₦X,XXX.
- **No anonymous reviews.** OTP verification is required before any review can be posted.
- **Open Now is calculated**, never estimated. Only shown when business hours are in the system.
- **No delivery, no booking.** This is a review platform. Never add checkout or reservation flows.
- **Performance matters.** Pages must load in under 3 seconds on 4G Nigerian mobile data. Optimise images. Lazy load below the fold.

---

## Brand Colours (quick reference)

| Token | Value | Use |
|---|---|---|
| Primary | `#E85C2C` | Buttons, active states, logo, badges |
| Primary Light | `#FFF0EB` | Backgrounds, chips, avatar fills |
| Primary Dark | `#993C1D` | Hover states, dark text on light |
| Accent Gold | `#F5A623` | Star ratings |
| Success | `#EAF3DE` / `#3B6D11` | Open badge, verified badge |
| Error | `#FCEBEB` / `#A32D2D` | Closed badge, error states |

Full design system in `style.md`.

---

## Data to Seed at Launch

Minimum 100 Abuja restaurant listings required before public launch. Seed data must include:
- Restaurant name
- Neighbourhood (Wuse 2, Jabi, Maitama, Guzape, Garki, Asokoro, Utako, etc.)
- Cuisine type
- Price range (₦ min – ₦ max per person)
- Business hours (Mon–Sun open/close times)
- Phone number (if publicly available)
- Approximate address

Seed 3–5 realistic reviews per restaurant with staggered dates. Do not use placeholder names — use realistic Nigerian names.
