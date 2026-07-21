# Findari — Screens & Pages Reference

> Complete screen inventory for Findari (formerly Abuja Eats).
> Covers MVP, Phase 1.5, and Phase 2+ screens with access rules, key components, and priority flags.
>
> **Priority key:** 🔴 MVP (must ship at launch) · 🟡 Phase 1.5 (build early, not launch-blocking) · 🟢 Phase 2+ (post-traction)

---

## Screen Index

| # | Screen | User Type | Priority |
|---|--------|-----------|----------|
| 1 | Home / Discovery Feed | All users | 🔴 MVP |
| 2 | Search Results | All users | 🔴 MVP |
| 3 | Restaurant Profile | All users | 🔴 MVP |
| 4 | Sign Up / OTP Verification | New users | 🔴 MVP |
| 5 | Log In | Returning users | 🔴 MVP |
| 6 | Write a Review | Verified users | 🔴 MVP |
| 7 | Claim This Business | Business owners | 🔴 MVP |
| 8 | Admin: Review Moderation | Admin only | 🔴 MVP |
| 9 | Admin: Business Claim Approval | Admin only | 🔴 MVP |
| 10 | Admin: Listing Seeder | Admin only | 🔴 MVP |
| 11 | User Profile | Logged-in users | 🟡 Phase 1.5 |
| 12 | Saved Spots | Logged-in users | 🟡 Phase 1.5 |
| 13 | Business Dashboard | Verified owners | 🟡 Phase 1.5 |
| 14 | Edit Listing Info | Verified owners | 🟡 Phase 1.5 |
| 15 | Edit User Profile / Settings | Logged-in users | 🟡 Phase 1.5 |
| 16 | Public Reviewer Profile | All users | 🟢 Phase 2+ |
| 17 | Friends' Activity Feed | Logged-in users | 🟢 Phase 2+ |
| 18 | Rating Trend Chart (in Dashboard) | Verified owners | 🟢 Phase 2+ |
| 19 | Promoted Listing Upgrade | Verified owners | 🟢 Phase 2+ |
| 20 | Privacy Policy & Terms | All users | 🔴 MVP (static) |

---

## MVP Screens 🔴

---

### Screen 1: Home / Discovery Feed

**Access:** All users (logged in or not)
**Route:** `/`

**Purpose:** Primary entry point. Users browse by neighbourhood, search for a spot, or scan trending restaurants.

**Layout (top → bottom):**
1. Top nav bar — logo + bell icon + user icon (or Login CTA if logged out)
2. Global search bar — full width, rounded, placeholder: *"Search restaurants, bukas…"*
3. "Browse by area" label + horizontal-scroll neighbourhood chips
   - Default chips: Wuse 2 · Jabi · Maitama · Guzape · Garki · Asokoro · Utako
4. Trending / Nearby section header
5. Restaurant cards (stacked list)
6. Bottom navigation bar — Home · Search · Saved · Profile

**Key components:**
- Neighbourhood chip (pill, scrollable, active chip fills `#E85C2C`)
- Restaurant card: thumbnail icon (32×32) + name + star rating + cuisine · area · price range
- Open Now badge (green)
- Price range badge (orange, in ₦)

**Functions:**
| Feature | Priority |
|---------|----------|
| Global search bar | 🔴 |
| Neighbourhood filter chips | 🔴 |
| Restaurant cards with rating + price | 🔴 |
| Open Now filter toggle | 🔴 |
| Cuisine type filter (dropdown/chips) | 🟡 |
| Price range filter (slider) | 🟡 |
| Trending / Top Rated section | 🟡 |
| Recently Reviewed section | 🟡 |
| Featured Spots (admin-curated) | 🟢 |
| Friends' activity feed | 🟢 |

---

### Screen 2: Search Results

**Access:** All users
**Route:** `/search?q=…&area=…&cuisine=…`

**Purpose:** Display filtered results after a search query or neighbourhood tap.

**Layout:**
1. Top bar — back arrow + active search query field (editable)
2. Active filter chips row (dismissible): area, cuisine, Open Now, price range
3. Results count label — *"14 spots in Jabi"*
4. Restaurant cards list (same card component as Home)
5. Empty state — *"No results for [query] in [area]. Try a different area."*

**Key components:**
- Editable search field in top bar (user can refine without going back)
- Dismissible filter chips
- Empty state illustration + suggestion text
- Bottom navigation bar (Search tab active)

**Functions:**
| Feature | Priority |
|---------|----------|
| Text search (name, cuisine, area) | 🔴 |
| Filter by neighbourhood | 🔴 |
| Filter by Open Now | 🔴 |
| Filter by cuisine type | 🟡 |
| Filter by price range | 🟡 |
| Sort by: Most Reviewed / Highest Rated / Nearest | 🟡 |

---

### Screen 3: Restaurant Profile

**Access:** All users
**Route:** `/restaurant/:slug`

**Purpose:** Full listing page. The primary trust-building surface — where a user decides whether to visit.

**Layout (top → bottom):**
1. Top bar — back arrow + "Restaurant" label + share icon (white on `#E85C2C`)
2. Hero image — full width (~200px tall); placeholder if no photo uploaded
3. Restaurant name (16px semibold)
4. Sub-heading — cuisine + neighbourhood (12px secondary)
5. Status badge row:
   - Open Now badge (green bg `#EAF3DE`, text `#3B6D11`) or Closed (red bg `#FCEBED`)
   - Closing time note — *"Closes at 10pm"*
   - Price range badge (orange bg `#FFF0EB`, dark orange text `#993C1D`) — e.g. *"₦1,500–₦4,000"*
6. Rating block:
   - Large overall score (e.g. 4.7 · 20px semibold)
   - Three rating bars: Food · Service · Ambience (fill: `#E85C2C`, track: border-tertiary, height 4px)
   - Total review count — *(38 reviews)*
7. "Write a Review" CTA button — full width, orange, rounded
8. Address + Google Maps embed (exact location pin)
9. Tap-to-call phone number (if provided)
10. Business hours grid (Mon–Sun, open/close times)
11. Photo gallery — horizontal scroll, customer-uploaded photos (up to 5 per review)
12. Reviews list:
    - Each review: avatar (initials circle) + name + ✓ Verified badge + date (right-aligned) + stars + review text
    - Flag icon on each review (report as fake/abusive)
    - Owner response shown below review (if claimed and responded)
13. Bottom navigation bar

**Key components:**
- Open Now / Closed badge
- Price range badge
- Rating breakdown bars (Food / Service / Ambience)
- Photo gallery (scrollable)
- Review item component (avatar + verified badge + flag button)
- Google Maps embed

**Functions:**
| Feature | Priority |
|---------|----------|
| Hero image | 🔴 |
| Open Now indicator | 🔴 |
| Price range (₦) | 🔴 |
| Star rating + breakdown bars | 🔴 |
| Address + Maps embed | 🔴 |
| Phone (tap-to-call) | 🔴 |
| Business hours | 🔴 |
| Photo gallery | 🔴 |
| Verified reviews list | 🔴 |
| Flag review button | 🔴 |
| Write a Review CTA | 🔴 |
| Save / Bookmark (heart icon) | 🟡 |
| Share listing button | 🟡 |
| Photo lightbox (full-screen tap) | 🟡 |
| Owner response on reviews | 🟡 |
| Sort reviews (Most Recent / Highest / Lowest) | 🟢 |

---

### Screen 4: Sign Up / OTP Verification

**Access:** New users (unauthenticated)
**Route:** `/signup`

**Purpose:** Create a verified reviewer account. All reviewers must verify via OTP before posting.

**Layout (step-by-step flow):**

**Step 1 — Enter email**
- Findari logo + "Create your account" heading
- Email input field
- "Continue" primary button
- "Already have an account? Log in" link

**Step 2 — OTP entry**
- "Check your inbox" heading
- Subtext: *"We sent a 6-digit code to [email]. It expires in 10 minutes."*
- 6-box OTP input (auto-focus, auto-advance)
- "Resend code" link (active after 60s countdown)
- Back link

**Step 3 — Complete profile**
- "Almost there" heading
- Display name input
- Abuja neighbourhood dropdown (Wuse 2, Jabi, Maitama, etc.)
- "Start exploring" button → redirects to Home

**Validation rules:**
- Valid email format required
- OTP must match; expired OTP shows inline error
- Display name: 2–50 characters
- Neighbourhood: required selection

**Functions:**
| Feature | Priority |
|---------|----------|
| Email OTP sign-up | 🔴 |
| OTP expiry + resend | 🔴 |
| Display name + neighbourhood setup | 🔴 |
| Google Sign-In (OAuth) | 🟡 |

---

### Screen 5: Log In

**Access:** Returning users
**Route:** `/login`

**Purpose:** Return users re-authenticate via email OTP (no passwords stored).

**Layout:**
1. Findari logo
2. "Welcome back" heading
3. Email input
4. "Send login code" button
5. OTP entry screen (same component as Sign Up Step 2)
6. "Don't have an account? Sign up" link

---

### Screen 6: Write a Review

**Access:** Verified logged-in users only
**Route:** `/restaurant/:slug/review` (modal or full-screen overlay)

**Purpose:** Let a verified user rate and describe their experience at a specific restaurant.

**Layout (top → bottom):**
1. Top bar — X (cancel) + "Write a review" label + "Post" button (white, 10px, disabled until valid)
2. Restaurant name reminder header (10px semibold)
3. "Overall rating" label → 5 large interactive stars (gold when selected; pulse animation if unselected on submit attempt)
4. "Rate by category" section:
   - Food: 1–5 mini star selector inline
   - Service: 1–5 mini star selector inline
   - Ambience: 1–5 mini star selector inline
5. "Your review" label → text area (placeholder: *"Tell others what you thought…"*, min-height 38px, expands, max 1,000 chars)
6. Character counter (shown when text is entered)
7. "Add photos" label → dashed-border upload zone, camera icon, "Tap to add up to 5 photos"; thumbnail row appears after selection
8. Optional: "When did you visit?" date picker
9. "Post review" full-width button (orange, disabled until: ≥1 star + ≥20 chars)

**Validation rules:**
- Must be logged in and OTP-verified
- Min 1 star overall; min 20 characters text; max 5 photos
- One review per restaurant per user (edit allowed, duplicate not)
- No anonymous reviews

**Functions:**
| Feature | Priority |
|---------|----------|
| Overall star rating selector | 🔴 |
| Sub-category ratings (Food/Service/Ambience) | 🔴 |
| Review text field (min 20 chars) | 🔴 |
| Photo upload (up to 5) | 🔴 |
| Post / Discard buttons | 🔴 |
| Visit date picker | 🟡 |
| Dish tag (tag which dish you ordered) | 🟢 |

---

### Screen 7: Claim This Business

**Access:** Any user who can prove ownership of a listed restaurant
**Route:** `/restaurant/:slug/claim`

**Purpose:** Multi-step flow for restaurant owners to claim their auto-generated listing and unlock the Business Dashboard.

**Flow steps:**

**Step 1 — Find listing**
- User locates their restaurant on the platform (via search or profile page)
- Taps "Claim This Business" button (visible on every unclaimed listing)

**Step 2 — Submit verification**
- Form fields:
  - Business email address
  - Phone number (tap-to-verify via OTP preferred)
  - CAC registration number (optional — speeds up approval)
- "Submit claim" button → confirmation screen: *"We'll review your claim within 24–48 hours."*

**Step 3 — Await admin approval**
- Informational screen or email confirmation
- Status: Pending / Approved / Rejected

**Step 4 — Access granted**
- Owner receives email link → lands on Business Dashboard

**Functions:**
| Feature | Priority |
|---------|----------|
| Claim This Business CTA | 🔴 |
| Business verification form | 🔴 |
| Admin review queue integration | 🔴 |
| Email notification on approval | 🔴 |

---

### Screen 8: Admin — Review Moderation Queue

**Access:** Admin only
**Route:** `/admin/reviews`

**Purpose:** Review and action flagged reviews reported by users.

**Layout:**
1. Admin top bar — "Review Moderation" label + badge count of pending flags
2. Filter tabs: All · Pending · Resolved
3. Flagged review cards:
   - Review text + restaurant name + reviewer name + flag reason
   - Action buttons: "Keep review" · "Remove review" · "Warn user" · "Ban user"
4. Resolution logged with timestamp

**Validation rules:**
- Flagged reviews resolved within 48 hours (per non-functional requirements)
- Removed reviews logged for audit trail (not permanently deleted)

---

### Screen 9: Admin — Business Claim Approval

**Access:** Admin only
**Route:** `/admin/claims`

**Purpose:** Review and approve or reject incoming business ownership claims.

**Layout:**
1. Admin top bar — "Claim Approvals" label + pending count badge
2. Claim cards:
   - Restaurant name + claimed by + submission date
   - Submitted: business email, phone, CAC number (if provided)
   - Action buttons: "Approve" · "Reject" · "Request more info"
3. Approved claim triggers email to owner with dashboard access link

---

### Screen 10: Admin — Listing Seeder

**Access:** Admin only
**Route:** `/admin/seed`

**Purpose:** Bulk import tool to add the initial 100+ Abuja restaurant listings before public launch.

**Features:**
- CSV/spreadsheet upload (name, neighbourhood, cuisine, price range, address, phone, hours)
- Row-by-row validation with inline error feedback
- Preview table before committing
- Submit → listings created with "Unverified" status (pending owner claim)

---

### Screen 20: Privacy Policy & Terms of Service

**Access:** All users
**Routes:** `/privacy` · `/terms`

**Purpose:** Legal pages required before public launch (NDPR compliance, defamatory review policy).

**Note:** Static pages. Must be live before launch. Link in footer and during sign-up flow.

---

## Phase 1.5 Screens 🟡

---

### Screen 11: User Profile

**Access:** Logged-in user (own profile)
**Route:** `/profile`

**Purpose:** Review history, stats, and personal identity on the platform.

**Layout:**
1. Top bar — "My Profile" label + settings icon
2. Avatar — 36px circle, initials, `#FFF0EB` bg, `#E85C2C` text
3. Display name (14px semibold)
4. Location + join date — *"Abuja · Joined June 2026"* (11px secondary)
5. Stats bar — 3 equal-width pill boxes: Reviews · Saved · Avg Rating Given
6. "Recent reviews" section:
   - Review cards: restaurant name + stars (right) + date + ✓ Verified label
7. "Saved spots" section:
   - Saved restaurant cards: heart icon + name + neighbourhood
8. Bottom navigation (Profile tab active)

**Functions:**
| Feature | Priority |
|---------|----------|
| Review history list | 🔴 (within Phase 1.5) |
| Stats bar (reviews / saved / avg) | 🔴 (within Phase 1.5) |
| Saved spots list | 🟡 |
| Edit profile | 🟡 |
| Settings / Logout | 🟡 |
| Public profile view (other users) | 🟢 |

---

### Screen 12: Saved Spots

**Access:** Logged-in users
**Route:** `/saved`

**Purpose:** Bookmarked restaurants — the user's personal shortlist.

**Layout:**
1. Top bar — "Saved" label
2. Saved restaurant cards (same card component as Home)
3. Empty state — "You haven't saved any spots yet. Tap ♥ on any restaurant to save it."
4. Bottom navigation (Saved tab active)

---

### Screen 13: Business Dashboard

**Access:** Verified business owners only
**Route:** `/business/dashboard`

**Purpose:** Central hub for owners to monitor their listing performance and respond to reviews.

**Layout:**
1. Top bar — building icon + "Business" label + settings icon
2. Business header card — name in `#E85C2C` + "Verified business · [Neighbourhood]" in `#993C1D`; bg `#FFF0EB`
3. Metrics grid (2×2):
   - Avg rating · Total reviews
   - Profile views · Views this week
4. "Recent reviews to respond to" section header
5. Review respond cards — avatar + name + stars (right) | review excerpt | "Reply to this review" outline button
6. "Edit listing info" full-width outline button

**Functions:**
| Feature | Priority |
|---------|----------|
| Metrics grid | 🟡 |
| Recent reviews list | 🟡 |
| Reply to review | 🟡 |
| Edit listing info CTA | 🔴 (within Phase 1.5) |
| Rating trend chart (line chart, 30/60/90 days) | 🟢 |
| New review notification badge | 🟢 |
| Promoted listing upgrade CTA | 🟢 (V2) |

---

### Screen 14: Edit Listing Info

**Access:** Verified business owners
**Route:** `/business/edit`

**Purpose:** Owners keep their listing accurate — address, hours, price range, photos, phone, description.

**Form fields:**
- Business name (read-only after claim)
- Address (editable)
- Neighbourhood (dropdown)
- Cuisine type (multi-select)
- Price range (₦ min – ₦ max)
- Opening hours (Mon–Sun, open/close time pickers, "Closed" toggle)
- Phone number
- Short description (max 300 chars)
- Photo uploads (up to 10 hero photos)
- "Save changes" primary button

---

### Screen 15: Edit User Profile / Settings

**Access:** Logged-in users
**Route:** `/profile/settings`

**Sections:**
- Edit display name
- Edit neighbourhood
- Notification preferences (email: new review likes, platform updates)
- Account: change email, delete account
- "Log out" button

---

## Phase 2+ Screens 🟢

---

### Screen 16: Public Reviewer Profile

**Access:** All users
**Route:** `/reviewer/:username`

**Purpose:** Publicly viewable profile showing a reviewer's history and credibility.

**Shows:** Display name · join date · review count · avg rating given · review history (public)
**Does not show:** Email, phone, or any personal contact info

---

### Screen 17: Friends' Activity Feed

**Access:** Logged-in users with connected contacts
**Route:** `/activity` or section on Home

**Purpose:** Social layer — see restaurants recently reviewed or saved by people you follow.

**Requires:** Contact connection or manual follow system (scoped to Phase 2)

---

### Screen 18: Rating Trend Chart

**Access:** Verified business owners (within Business Dashboard)
**Route:** Embedded in `/business/dashboard`

**Purpose:** Line chart showing average rating trend over the last 30 / 60 / 90 days. Helps owners spot quality regressions or improvements.

**Component:** Time range selector tabs → chart renders from review timestamp data

---

### Screen 19: Promoted Listing Upgrade

**Access:** Verified business owners
**Route:** `/business/promote`

**Purpose:** Paid placement at the top of neighbourhood search results.

**Requires:** Payment integration (Flutterwave / Paystack) — deferred to Phase 2 once sufficient user base achieved.

---

## Authentication Flow Summary

### Reviewer Registration
1. Enter email → OTP sent (6-digit, 10-min expiry)
2. Enter OTP → account created
3. Enter display name + Abuja neighbourhood
4. Optional: connect Google for faster future login

### Reviewer Login
1. Enter email → OTP sent
2. Enter OTP → logged in

### Business Owner Claim
1. Find listing → tap "Claim This Business"
2. Submit: business email + phone + CAC (optional)
3. Admin reviews within 24–48 hours
4. Owner receives email link → Business Dashboard access

---

## Bottom Navigation (Persistent)

| Tab | Icon | Route | Active when |
|-----|------|-------|-------------|
| Home | Home icon | `/` | Home, Search Results |
| Search | Magnifier | `/search` | Search, Filters |
| Saved | Heart | `/saved` | Saved Spots |
| Profile | Person | `/profile` | User Profile, Settings |

Active tab: `#E85C2C` icon + label · Inactive: `var(--color-text-tertiary)`

---

## Responsive Behaviour

| Breakpoint | Width | Layout changes |
|------------|-------|---------------|
| Mobile (base) | 375px | Single-column, bottom nav |
| Mobile L | 425px | Slightly wider cards |
| Tablet | 768px | 2-column card grid on Home/Search |
| Desktop | 1024px+ | 3-column grid; side nav replaces bottom nav; Restaurant Profile: info left + map/photos right |

---

*Last updated: July 2026 — Findari v1.0 Planning & Design phase*
