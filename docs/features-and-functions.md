# Findari — Features & Functions

> Detailed breakdown of every feature by screen, user type, and priority.
> Priority: 🔴 MVP · 🟡 Phase 1.5 · 🟢 Phase 2+

---

## Screen 1: Home / Discovery Feed

**Accessible to:** All users (logged in or not)

| Function | Description | Priority |
|---|---|---|
| Global search bar | Search by restaurant name, cuisine type, or neighbourhood | 🔴 |
| Neighbourhood filter chips | Scrollable chips: Wuse 2, Jabi, Maitama, Guzape, Garki, Asokoro, Utako, etc. | 🔴 |
| Restaurant cards | Show: name, cuisine, neighbourhood, price range, star rating, review count | 🔴 |
| Open Now filter | Toggle to show only restaurants currently open | 🔴 |
| Cuisine filter | Dropdown or chip set: Nigerian, Chinese, Continental, Suya, Café, etc. | 🟡 |
| Price range filter | Slider or range selector in Naira | 🟡 |
| Trending / Top Rated | Curated section surfacing highest-rated spots this week | 🟡 |
| Recently Reviewed | Show restaurants with the most recent review activity | 🟡 |
| Featured spots | Manually curated section (admin-controlled) | 🟢 |
| Friends' activity feed | See restaurants recently reviewed by connections | 🟢 |

**Navigation bar (bottom):** Home · Search · Saved · Profile

---

## Screen 2: Restaurant Profile Page

**Accessible to:** All users

| Function | Description | Priority |
|---|---|---|
| Hero image | Primary photo of restaurant (or placeholder if none uploaded) | 🔴 |
| Restaurant name | Large, prominent heading | 🔴 |
| Cuisine type + Neighbourhood | Sub-heading below name | 🔴 |
| Open Now badge | Green badge if currently open; red if closed; greyed if hours not set | 🔴 |
| Closing time display | "Closes at 10pm" shown alongside Open Now badge | 🔴 |
| Price range badge | "₦1,500–₦4,000" in orange badge | 🔴 |
| Overall star rating | Numeric (e.g. 4.7) + breakdown bars for Food / Service / Ambience | 🔴 |
| Total review count | "(38 reviews)" beneath overall score | 🔴 |
| Address + map embed | Google Maps embed showing exact location | 🔴 |
| Phone number | Tap-to-call link (if provided by business) | 🔴 |
| Business hours | Mon–Sun grid with open/close times | 🔴 |
| Photo gallery | Customer-uploaded photos in scrollable grid (up to 5 per review) | 🔴 |
| Review list | All reviews sorted by most recent; each shows avatar, name, verified badge, date, stars, text | 🔴 |
| Verified badge on reviews | "✓ Verified" label on all OTP-verified reviewers | 🔴 |
| Flag review button | Small flag icon on each review to report as fake/abusive | 🔴 |
| Write a Review CTA | Prominent button, bottom of profile | 🔴 |
| Save / Bookmark button | Heart icon to save to user's saved list | 🟡 |
| Owner response on reviews | If business claimed, owner reply appears below each relevant review | 🟡 |
| Share listing button | Share URL to restaurant profile | 🟡 |
| Photo lightbox | Tap any photo to view full screen | 🟡 |
| Sort reviews | Sort by: Most Recent / Highest Rated / Lowest Rated | 🟢 |

---

## Screen 3: Write a Review

**Accessible to:** Verified logged-in users only

| Function | Description | Priority |
|---|---|---|
| Restaurant name header | Reminds reviewer which restaurant they're rating | 🔴 |
| Overall star rating | Interactive 1–5 star selector | 🔴 |
| Sub-category ratings | Separate 1–5 star selectors for: Food · Service · Ambience | 🔴 |
| Review text field | Free-text field, minimum 20 characters, max 1,000 characters | 🔴 |
| Photo upload | Tap to upload up to 5 photos from camera roll; preview thumbnails shown | 🔴 |
| Post button | Submits review; goes live immediately after spam check | 🔴 |
| Discard / Cancel | X button returns to restaurant profile without saving | 🔴 |
| Visit date selector | Optional: "When did you visit?" date picker | 🟡 |
| Dish tag | Optional: Tag which dish you ordered | 🟢 |
| Anonymous option | NOT supported — all reviews require verified identity | — |

**Validation rules:**
- Must be logged in and OTP-verified
- Minimum 1 star must be selected
- Minimum 20 characters in text
- Max 5 photos
- One review per restaurant per user (edit allowed, not duplicate)

---

## Screen 4: User Profile

**Accessible to:** Logged-in user (own profile only in MVP)

| Function | Description | Priority |
|---|---|---|
| Avatar / initials | Auto-generated initials avatar (no photo upload in MVP) | 🔴 |
| Display name | Full name as provided at signup | 🔴 |
| Location + join date | "Abuja · Joined June 2026" | 🔴 |
| Stats bar | Reviews written · Saved spots · Average rating given | 🔴 |
| Review history | All reviews posted, sorted by date; each shows restaurant name, stars, date, verified label | 🔴 |
| Saved spots list | All bookmarked restaurants with name and neighbourhood | 🟡 |
| Edit profile | Update display name and location | 🟡 |
| Settings | Notification preferences, account, logout | 🟡 |
| Public profile view | Other users can view a reviewer's profile and reviews | 🟢 |

---

## Screen 5: Business Dashboard

**Accessible to:** Verified business owners only

| Function | Description | Priority |
|---|---|---|
| Business name + verified badge | "Verified business · [Neighbourhood]" | 🔴 |
| Metrics grid | Avg rating · Total reviews · Profile views · Views this week | 🟡 |
| Recent reviews list | Latest unresponded reviews shown first | 🟡 |
| Reply to review | Text input to write a public response; posted below the review | 🟡 |
| Edit listing info | Update address, hours, price range, photos, description, phone | 🔴 |
| Claim This Business flow | Multi-step: find listing → submit verification → await approval → gain access | 🔴 |
| Rating trend chart | Line chart showing avg rating over last 30/60/90 days | 🟢 |
| Notification alerts | Badge when new review is posted | 🟢 |
| Promoted listing upgrade | CTA for paid placement at top of neighbourhood results | 🟢 (V2) |

---

## Authentication Flows

### Reviewer Registration
1. Enter email address
2. OTP sent to email (6-digit code, expires in 10 minutes)
3. Enter OTP → account created
4. Enter display name and Abuja neighbourhood
5. Optional: connect Google account for faster future login

### Business Owner Claim
1. Find restaurant listing on platform
2. Click "Claim This Business"
3. Enter: business email, phone number, CAC number (optional but speeds verification)
4. Admin reviews claim within 24–48 hours
5. Owner receives access to dashboard via email link

---

## Platform / Admin Functions

| Function | Description | Priority |
|---|---|---|
| Review moderation queue | Admin view of all flagged reviews; accept or remove | 🔴 |
| Business claim approval | Admin queue for reviewing and approving listing claims | 🔴 |
| Restaurant seeding | Bulk import tool for adding the initial 100+ listings | 🔴 |
| Featured spots management | Admin UI to manually curate featured section on home | 🟡 |
| User ban / suspension | Ban accounts that abuse the review system | 🟡 |
