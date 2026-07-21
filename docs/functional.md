# Findari — Functional Requirements

> Defines **what the system must do** — every user-facing and system behaviour required for Findari to operate correctly.
> Derived from the PRD, features-and-functions spec, and design document.
>
> **Priority key:** 🔴 MVP · 🟡 Phase 1.5 · 🟢 Phase 2+
> **User types:** Guest · Reviewer (verified user) · Business Owner · Admin

---

## FR-01: User Registration & Authentication

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-01.1 | The system shall allow a new user to register using an email address. | 🔴 |
| FR-01.2 | The system shall send a 6-digit OTP to the user's email upon registration. The OTP shall expire after 10 minutes. | 🔴 |
| FR-01.3 | The system shall not create an account until the OTP is successfully verified. | 🔴 |
| FR-01.4 | The system shall provide a "Resend OTP" option, available after a 60-second countdown. | 🔴 |
| FR-01.5 | After OTP verification, the system shall prompt the user to enter a display name (2–50 characters) and select an Abuja neighbourhood. | 🔴 |
| FR-01.6 | The system shall allow returning users to log in via email OTP (no password required). | 🔴 |
| FR-01.7 | The system shall not allow anonymous reviews. Every reviewer must be OTP-verified before posting. | 🔴 |
| FR-01.8 | The system shall support Google OAuth as an optional sign-in method. | 🟡 |
| FR-01.9 | The system shall allow users to log out from any screen. | 🟡 |
| FR-01.10 | The system shall allow users to change their registered email address after verification. | 🟡 |
| FR-01.11 | The system shall allow users to permanently delete their account and associated data. | 🟡 |

---

## FR-02: Restaurant Discovery & Search

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-02.1 | The system shall display a home feed of restaurant listings visible to all users (logged in or not). | 🔴 |
| FR-02.2 | The system shall provide a global search bar allowing users to search by restaurant name, cuisine type, or neighbourhood. | 🔴 |
| FR-02.3 | The system shall display horizontally-scrollable neighbourhood filter chips on the home screen (Wuse 2, Jabi, Maitama, Guzape, Garki, Asokoro, Utako, and others). | 🔴 |
| FR-02.4 | The system shall display a restaurant card for each result showing: name, cuisine type, neighbourhood, price range (₦), star rating, and review count. | 🔴 |
| FR-02.5 | The system shall show an "Open Now" badge on restaurant cards and profiles for listings whose current time falls within their business hours. | 🔴 |
| FR-02.6 | The system shall display a results count label on the search results screen (e.g. "14 spots in Jabi"). | 🔴 |
| FR-02.7 | The system shall display an empty state message when a search returns no results, with a suggestion to try a different area or query. | 🔴 |
| FR-02.8 | The system shall allow users to filter search results by cuisine type. | 🟡 |
| FR-02.9 | The system shall allow users to filter search results by price range using a ₦ slider or range selector. | 🟡 |
| FR-02.10 | The system shall allow users to sort search results by: Most Reviewed, Highest Rated, Nearest. | 🟡 |
| FR-02.11 | The system shall surface a "Trending / Top Rated" section on the home screen highlighting the highest-rated spots that week. | 🟡 |
| FR-02.12 | The system shall surface a "Recently Reviewed" section on the home screen showing restaurants with the most recent review activity. | 🟡 |
| FR-02.13 | The system shall support an admin-controlled "Featured Spots" section on the home screen. | 🟢 |
| FR-02.14 | The system shall display a "Friends' Activity Feed" showing restaurants recently reviewed or saved by the user's connected contacts. | 🟢 |

---

## FR-03: Restaurant Profile

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-03.1 | The system shall display a full restaurant profile page accessible to all users (logged in or not). | 🔴 |
| FR-03.2 | The profile shall display: restaurant name, cuisine type, neighbourhood, hero image (or placeholder), price range (₦), open/closed status, closing time, address, phone number, and business hours (Mon–Sun). | 🔴 |
| FR-03.3 | The profile shall display an overall star rating (numeric, e.g. 4.7) derived from the average of all verified reviews. | 🔴 |
| FR-03.4 | The profile shall display three separate rating breakdown bars for Food, Service, and Ambience. | 🔴 |
| FR-03.5 | The profile shall display the total review count prominently alongside the overall rating. | 🔴 |
| FR-03.6 | The profile shall embed a Google Maps pin showing the restaurant's exact location. | 🔴 |
| FR-03.7 | The phone number, if provided, shall be a tap-to-call link on mobile devices. | 🔴 |
| FR-03.8 | The profile shall display a customer photo gallery in a horizontally scrollable grid, sourced from reviewer uploads. | 🔴 |
| FR-03.9 | The profile shall list all verified reviews, sorted by most recent by default. Each review shall show: reviewer avatar (initials), display name, Verified badge, date posted, star rating, and review text. | 🔴 |
| FR-03.10 | Each review on the profile shall include a flag icon allowing any user to report it as fake, irrelevant, or abusive. | 🔴 |
| FR-03.11 | The profile shall display a "Write a Review" CTA button. Tapping it redirects unauthenticated users to the sign-up flow, then returns them to the review form. | 🔴 |
| FR-03.12 | The profile shall display an "Unclaimed" badge on listings not yet verified by an owner, and a "Claim This Business" CTA. | 🔴 |
| FR-03.13 | The system shall allow users to save (bookmark) a restaurant to their Saved Spots list via a heart icon. | 🟡 |
| FR-03.14 | The profile shall include a "Share" button that copies or opens the restaurant's URL for sharing. | 🟡 |
| FR-03.15 | Tapping any photo in the gallery shall open it in a full-screen lightbox view. | 🟡 |
| FR-03.16 | If a verified business owner has responded to a review, the response shall appear directly below that review on the profile. | 🟡 |
| FR-03.17 | The system shall allow users to sort reviews by: Most Recent, Highest Rated, Lowest Rated. | 🟢 |

---

## FR-04: Review System

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-04.1 | The system shall allow OTP-verified users to write a review for any listed restaurant. | 🔴 |
| FR-04.2 | The review form shall include an interactive 1–5 star overall rating selector. | 🔴 |
| FR-04.3 | The review form shall include separate 1–5 star selectors for Food, Service, and Ambience. | 🔴 |
| FR-04.4 | The review form shall include a free-text field with a minimum of 20 characters and a maximum of 1,000 characters. | 🔴 |
| FR-04.5 | The review form shall allow the user to upload up to 5 photos from their camera roll. Uploaded photos shall display as thumbnail previews before submission. | 🔴 |
| FR-04.6 | The "Post" button shall be disabled until at least 1 star is selected and the text field contains a minimum of 20 characters. | 🔴 |
| FR-04.7 | Upon submission, the review shall be published immediately after an automated spam check passes. | 🔴 |
| FR-04.8 | The system shall enforce one review per user per restaurant. Users may edit their existing review but may not post a duplicate. | 🔴 |
| FR-04.9 | All reviews shall display a "✓ Verified" badge indicating the reviewer completed OTP verification. | 🔴 |
| FR-04.10 | The review date shall be displayed prominently on every review item (e.g. "2 days ago" or "June 12, 2026"). | 🔴 |
| FR-04.11 | The system shall allow users to flag a review as fake, irrelevant, or abusive. Flagged reviews shall enter the admin moderation queue. | 🔴 |
| FR-04.12 | The review form shall include an optional "When did you visit?" date picker. | 🟡 |
| FR-04.13 | The review form shall include an optional dish tag field (tag which dish was ordered). | 🟢 |

---

## FR-05: Saved Spots

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-05.1 | The system shall allow logged-in users to save any restaurant to a personal Saved Spots list by tapping the heart icon. | 🟡 |
| FR-05.2 | Tapping the heart icon again shall remove the restaurant from the Saved Spots list. | 🟡 |
| FR-05.3 | The system shall display a dedicated Saved Spots screen (accessible via bottom navigation) listing all bookmarked restaurants. | 🟡 |
| FR-05.4 | The Saved Spots screen shall display an empty state message when no restaurants have been saved. | 🟡 |

---

## FR-06: User Profile

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-06.1 | The system shall display a profile screen for the logged-in user showing: display name, location, join date, stats (reviews written, saved spots, average rating given), review history, and saved spots. | 🟡 |
| FR-06.2 | The system shall auto-generate an initials-based avatar for every user (no profile photo upload required in MVP). | 🟡 |
| FR-06.3 | The system shall allow users to edit their display name and neighbourhood. | 🟡 |
| FR-06.4 | The system shall allow users to configure notification preferences (e.g. email notifications for review likes, platform updates). | 🟡 |
| FR-06.5 | The system shall display all reviews posted by the user in their review history, sorted by most recent. | 🟡 |
| FR-06.6 | The system shall provide a publicly viewable reviewer profile page accessible to all users, showing display name, join date, review count, and public review history. | 🟢 |

---

## FR-07: Business Owner — Claim This Business

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-07.1 | Every unclaimed listing shall display a "Claim This Business" button visible to all users. | 🔴 |
| FR-07.2 | Clicking "Claim This Business" shall open a multi-step verification form collecting: business email, phone number, and optional CAC registration number. | 🔴 |
| FR-07.3 | On submission, the claim shall enter the admin approval queue with a "Pending" status. The user shall see a confirmation screen stating review will occur within 24–48 hours. | 🔴 |
| FR-07.4 | Upon admin approval, the system shall send the business owner an email with a link to access the Business Dashboard. | 🔴 |
| FR-07.5 | Upon admin rejection, the system shall notify the applicant by email with a reason. | 🔴 |
| FR-07.6 | A claimed and verified listing shall display a "Verified Business" badge on its profile. | 🔴 |

---

## FR-08: Business Owner — Dashboard & Listing Management

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-08.1 | Verified business owners shall have access to a Business Dashboard displaying: average rating, total reviews, profile views (total and this week). | 🟡 |
| FR-08.2 | The Business Dashboard shall list recent reviews, prioritising those without an owner response. | 🟡 |
| FR-08.3 | Verified owners shall be able to post a public written response to any review on their listing. The response shall appear directly below the review on the profile. | 🟡 |
| FR-08.4 | Verified owners shall be able to edit the following listing details: address, neighbourhood, cuisine type(s), price range (₦ min–max), opening hours (per day, with "Closed" toggle), phone number, short description (max 300 chars), and hero photos (up to 10). | 🔴 |
| FR-08.5 | The Business Dashboard shall display a line chart showing average rating trend over the last 30, 60, or 90 days. | 🟢 |
| FR-08.6 | The system shall notify the business owner (via email or in-app badge) when a new review is posted on their listing. | 🟢 |
| FR-08.7 | The system shall offer a paid promoted listing feature that places the business at the top of neighbourhood search results. | 🟢 |

---

## FR-09: Admin Functions

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-09.1 | The system shall provide an admin-only Review Moderation Queue displaying all flagged reviews with: review text, restaurant name, reviewer name, and flag reason. | 🔴 |
| FR-09.2 | Admins shall be able to action each flagged review with: Keep, Remove, Warn User, or Ban User. All actions shall be logged with a timestamp. | 🔴 |
| FR-09.3 | Removed reviews shall be logged in an audit trail and not permanently deleted from the database. | 🔴 |
| FR-09.4 | The system shall provide an admin-only Business Claim Approval Queue listing all pending claims with: restaurant name, claimed by, submission date, business email, phone, and CAC number (if provided). | 🔴 |
| FR-09.5 | Admins shall be able to action each claim with: Approve, Reject, or Request More Info. | 🔴 |
| FR-09.6 | The system shall provide an admin Listing Seeder tool for bulk importing restaurants via CSV/spreadsheet. The import shall support: name, neighbourhood, cuisine, price range, address, phone, and business hours. | 🔴 |
| FR-09.7 | The Listing Seeder shall validate each row before import and display inline errors for invalid entries. A preview table shall be shown before the import is committed. | 🔴 |
| FR-09.8 | Seeded listings shall be created with "Unverified/Unclaimed" status by default. | 🔴 |
| FR-09.9 | The system shall provide an admin UI to manually curate the "Featured Spots" section on the home screen. | 🟡 |
| FR-09.10 | Admins shall be able to ban or suspend user accounts that abuse the review system. | 🟡 |

---

## FR-10: Navigation & Information Architecture

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-10.1 | The system shall display a persistent bottom navigation bar with four tabs: Home, Search, Saved, and Profile. | 🔴 |
| FR-10.2 | The active navigation tab shall be visually differentiated (filled icon + label in brand colour `#E85C2C`). | 🔴 |
| FR-10.3 | The system shall display a persistent top navigation bar on all screens, showing the Findari logo and contextual actions (back arrow, share icon, settings). | 🔴 |
| FR-10.4 | The system shall provide static Privacy Policy and Terms of Service pages linked from the footer and sign-up flow. | 🔴 |
| FR-10.5 | On desktop (1024px+), the bottom navigation shall be replaced by a side navigation panel. | 🟡 |

---

## FR-11: Photo & Media Handling

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-11.1 | The system shall allow reviewers to upload up to 5 photos per review from their device camera roll. | 🔴 |
| FR-11.2 | Uploaded photos shall be stored in Cloudinary (or equivalent cloud storage) and served via CDN. | 🔴 |
| FR-11.3 | The system shall display uploaded photos in a scrollable gallery on the restaurant profile. | 🔴 |
| FR-11.4 | Business owners shall be able to upload up to 10 hero photos for their listing. | 🟡 |
| FR-11.5 | Tapping any gallery photo shall open a full-screen lightbox view with swipe navigation. | 🟡 |

---

## FR-12: Maps & Location

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-12.1 | The system shall embed a Google Maps pin on every restaurant profile showing the listing's exact address. | 🔴 |
| FR-12.2 | All price ranges shall be displayed in Nigerian Naira (₦) only. | 🔴 |
| FR-12.3 | The "Open Now" status shall be calculated from the business-provided operating hours and the current time. It shall not be estimated or assumed. | 🔴 |

---

*Last updated: July 2026 — Findari v1.0 Planning & Design phase*
