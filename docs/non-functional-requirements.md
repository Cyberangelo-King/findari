# Findari — Non-Functional Requirements

> Defines **how the system must behave** — quality attributes, constraints, and standards that apply across all functional features.
> These requirements are binding for every phase unless explicitly scoped.
>
> **Priority key:** 🔴 MVP · 🟡 Phase 1.5 · 🟢 Phase 2+

---

## NFR-01: Performance

| ID | Requirement | Priority |
|----|-------------|----------|
| NFR-01.1 | All pages shall load within 3 seconds on a standard Nigerian mobile data connection (estimated 3G/4G: ~5 Mbps). | 🔴 |
| NFR-01.2 | Search results shall be returned and rendered within 2 seconds of query submission. | 🔴 |
| NFR-01.3 | Restaurant profile pages shall load within 3 seconds, including map embed initialisation and the first 10 reviews. | 🔴 |
| NFR-01.4 | Review submission (text + up to 5 photos) shall complete and show confirmation within 5 seconds under standard conditions. | 🔴 |
| NFR-01.5 | Images served from the photo gallery shall be compressed and delivered via CDN. No uncompressed original shall be served to the client. | 🔴 |
| NFR-01.6 | The system shall implement lazy loading for restaurant cards and review lists — only visible content is loaded on first render. | 🟡 |
| NFR-01.7 | The system shall cache frequently accessed data (home feed, top-rated restaurants) at the CDN layer with a maximum stale age of 60 seconds. | 🟡 |

---

## NFR-02: Mobile & Responsive Design

| ID | Requirement | Priority |
|----|-------------|----------|
| NFR-02.1 | The platform shall be fully functional on mobile browsers as the primary access device. Mobile-first is the default design target (375px base width). | 🔴 |
| NFR-02.2 | All buttons, inputs, and interactive form elements shall meet a minimum touch target size of 44×44px to ensure thumb-friendliness on small screens. | 🔴 |
| NFR-02.3 | All primary actions (search, review, save, navigate) shall be reachable without requiring the user to stretch or use two hands on a standard smartphone. | 🔴 |
| NFR-02.4 | The bottom navigation bar shall remain accessible at the bottom of the viewport on all mobile screen sizes. | 🔴 |
| NFR-02.5 | The platform shall render correctly at the following breakpoints: 375px (Mobile), 425px (Mobile L), 768px (Tablet), 1024px+ (Desktop). | 🟡 |
| NFR-02.6 | On tablet (768px), the home and search screens shall display a 2-column restaurant card grid. | 🟡 |
| NFR-02.7 | On desktop (1024px+), the bottom navigation shall be replaced by a side navigation panel. Restaurant profile layout shall adopt a side-by-side format (info left, map/photos right). | 🟡 |
| NFR-02.8 | The platform shall not require a native iOS or Android app install. All MVP functionality shall be available via the mobile web browser. | 🔴 |
| NFR-02.9 | The platform shall not use autoplay media or heavy CSS animations that degrade performance on low-end Android devices. | 🔴 |

---

## NFR-03: Trust, Safety & Content Integrity

| ID | Requirement | Priority |
|----|-------------|----------|
| NFR-03.1 | All reviewer accounts shall complete OTP email verification before they are permitted to post any review. | 🔴 |
| NFR-03.2 | Anonymous reviews shall not be permitted under any circumstances. | 🔴 |
| NFR-03.3 | Every review shall display its post date prominently so users can assess recency. | 🔴 |
| NFR-03.4 | Flagged reviews shall be reviewed and actioned by an admin within 48 hours of being reported. | 🔴 |
| NFR-03.5 | Removed reviews shall not be permanently deleted. They shall be archived in an audit log with removal reason and admin identifier. | 🔴 |
| NFR-03.6 | The spam-check layer applied at review submission shall reject obvious bot patterns (e.g. repeated identical text, high-velocity submissions) before the review is published. | 🔴 |
| NFR-03.7 | A user account shall not be permitted to post more than one review per restaurant. Edits to an existing review are allowed; duplicate submissions are blocked. | 🔴 |
| NFR-03.8 | Business claim verification shall require at minimum a business email address and phone number before the claim enters the admin queue. | 🔴 |
| NFR-03.9 | The "Open Now" badge shall only be shown when confirmed from business-provided operating hours — it shall never be estimated or inferred. A grey/neutral state shall display when hours are not set. | 🔴 |
| NFR-03.10 | Users who have been banned shall see a clear account suspension message and be prevented from posting reviews, flagging content, or claiming listings. | 🟡 |

---

## NFR-04: Data Accuracy & Integrity

| ID | Requirement | Priority |
|----|-------------|----------|
| NFR-04.1 | All price ranges displayed on the platform shall be in Nigerian Naira (₦) only. No other currency shall be shown. | 🔴 |
| NFR-04.2 | No restaurant listing shall be made publicly visible until it contains at minimum: name, neighbourhood, cuisine type, and price range. | 🔴 |
| NFR-04.3 | The overall star rating displayed on a restaurant profile shall be calculated as the real-time average of all verified reviews, rounded to one decimal place. | 🔴 |
| NFR-04.4 | Sub-category ratings (Food, Service, Ambience) shall be calculated and displayed independently from the overall rating. | 🔴 |
| NFR-04.5 | All seeded listings (imported via admin bulk tool) shall carry "Unverified/Unclaimed" status until a business owner successfully completes the claim flow. | 🔴 |
| NFR-04.6 | The system shall prevent duplicate restaurant listings for the same business name and address combination. The admin seeder shall flag potential duplicates before import. | 🔴 |
| NFR-04.7 | User-uploaded photos shall be validated for file type (JPEG, PNG, WEBP only) and maximum file size (10MB per photo) before upload is accepted. | 🔴 |

---

## NFR-05: Security

| ID | Requirement | Priority |
|----|-------------|----------|
| NFR-05.1 | All data in transit shall be encrypted using HTTPS/TLS 1.2 or higher. HTTP shall redirect to HTTPS. | 🔴 |
| NFR-05.2 | No passwords shall be stored. Authentication is OTP-only (email). | 🔴 |
| NFR-05.3 | OTP codes shall be single-use. A code that has been successfully verified shall be invalidated immediately and cannot be reused. | 🔴 |
| NFR-05.4 | OTP codes shall expire after 10 minutes from generation. | 🔴 |
| NFR-05.5 | The system shall rate-limit OTP requests to prevent brute-force and OTP flooding attacks (maximum 5 OTP requests per email address per hour). | 🔴 |
| NFR-05.6 | All API endpoints shall validate authentication tokens on every request. Unauthenticated requests to protected routes shall return a 401 response. | 🔴 |
| NFR-05.7 | Business Dashboard routes shall validate that the authenticated user is the verified owner of the specific listing being accessed. | 🔴 |
| NFR-05.8 | Admin routes shall be accessible only to accounts with the Admin role. Access attempts by non-admin users shall return a 403 response. | 🔴 |
| NFR-05.9 | All form inputs shall be sanitised server-side to prevent SQL injection and cross-site scripting (XSS) attacks. | 🔴 |
| NFR-05.10 | User-uploaded files shall be scanned for malicious content before being stored or served. | 🟡 |
| NFR-05.11 | The system shall implement CSRF protection on all state-changing API endpoints. | 🔴 |

---

## NFR-06: Legal & Compliance

| ID | Requirement | Priority |
|----|-------------|----------|
| NFR-06.1 | A Privacy Policy and Terms of Service page shall be live and publicly accessible before the platform opens to the public. | 🔴 |
| NFR-06.2 | The platform shall comply with the Nigeria Data Protection Regulation (NDPR). This includes: obtaining consent at sign-up, enabling data access requests, and enabling account/data deletion. | 🔴 |
| NFR-06.3 | A clearly documented defamatory review policy shall exist and be enforced. Reviews that are found to be defamatory after admin review shall be removed and the incident logged. | 🔴 |
| NFR-06.4 | Users shall be informed of the data collected at sign-up, including what is shared publicly (display name, reviews) vs. kept private (email address, phone number). | 🔴 |
| NFR-06.5 | The platform shall not sell or share user personal data with third parties for marketing purposes. | 🔴 |
| NFR-06.6 | All email communications (OTP, claim approval, review notifications) shall include an unsubscribe option for non-transactional messages. | 🟡 |

---

## NFR-07: Reliability & Availability

| ID | Requirement | Priority |
|----|-------------|----------|
| NFR-07.1 | The platform shall target 99.5% uptime during its MVP and early growth phase. | 🟡 |
| NFR-07.2 | Planned maintenance windows shall be scheduled outside peak hours (06:00–22:00 WAT) and communicated to users in advance where possible. | 🟡 |
| NFR-07.3 | The system shall handle failed OTP delivery gracefully — if an OTP email fails to send, the user shall see a clear error message with a retry option. | 🔴 |
| NFR-07.4 | If the Google Maps API is unavailable, the restaurant profile shall degrade gracefully — displaying the address in text without the map embed rather than showing a broken component. | 🔴 |
| NFR-07.5 | If photo CDN storage is temporarily unavailable during review submission, the system shall allow the review text to be submitted and queue the photo upload for retry. | 🟡 |
| NFR-07.6 | The system shall display user-friendly error pages (404 for missing listings, 500 for server errors) rather than raw error output. | 🔴 |

---

## NFR-08: Scalability

| ID | Requirement | Priority |
|----|-------------|----------|
| NFR-08.1 | The system architecture shall support a minimum of 500 concurrent users at MVP launch without degradation to page load times. | 🟡 |
| NFR-08.2 | The database schema shall be designed to accommodate future expansion beyond Abuja to other Nigerian cities (Lagos, Port Harcourt, Enugu) without requiring structural migration. | 🟡 |
| NFR-08.3 | The listing data model shall support future addition of new data fields (e.g. delivery integration, reservation system) without breaking existing API contracts. | 🟢 |
| NFR-08.4 | Photo storage shall use a cloud provider (Cloudinary or equivalent) whose free tier covers MVP needs and whose paid tiers scale linearly with usage. | 🔴 |

---

## NFR-09: Accessibility

| ID | Requirement | Priority |
|----|-------------|----------|
| NFR-09.1 | All interactive elements (buttons, links, form inputs) shall have descriptive ARIA labels for screen reader compatibility. | 🟡 |
| NFR-09.2 | The colour contrast ratio between text and background shall meet WCAG 2.1 AA minimum (4.5:1 for normal text, 3:1 for large text). | 🟡 |
| NFR-09.3 | The star rating selector shall be operable via keyboard (tab to focus, arrow keys to change value) in addition to tap/click. | 🟡 |
| NFR-09.4 | All photos uploaded by users or businesses shall support alt text (auto-generated where not manually provided). | 🟢 |

---

## NFR-10: Internationalisation & Localisation

| ID | Requirement | Priority |
|----|-------------|----------|
| NFR-10.1 | The platform language shall be English (Nigerian English conventions preferred). | 🔴 |
| NFR-10.2 | All currency values shall be displayed in Nigerian Naira (₦). | 🔴 |
| NFR-10.3 | Neighbourhood names and Abuja-specific place names shall use their locally recognised spellings (e.g. Wuse 2, Maitama, Guzape, Asokoro). | 🔴 |
| NFR-10.4 | Date and time formats shall use Nigerian convention: day-month-year (e.g. 12 June 2026) and 12-hour clock with AM/PM. | 🟡 |
| NFR-10.5 | The system shall be architected to support future multi-language localisation (at minimum: Yoruba, Hausa, Igbo) without requiring a full rewrite. | 🟢 |

---

## NFR-11: Analytics & Observability

| ID | Requirement | Priority |
|----|-------------|----------|
| NFR-11.1 | The platform shall integrate Google Analytics 4 to track page views, session duration, search queries, and review submission events. | 🟡 |
| NFR-11.2 | The platform shall integrate Mixpanel (or equivalent) to track user-level events: sign-ups, reviews posted, restaurants saved, searches performed. | 🟡 |
| NFR-11.3 | Server-side error logging shall capture and alert on 5xx errors, with a maximum notification delay of 5 minutes. | 🟡 |
| NFR-11.4 | Business Dashboard profile view counts shall be tracked and updated with a maximum lag of 24 hours. | 🟡 |

---

## NFR-12: Tech Stack Constraints

| Constraint | Detail |
|------------|--------|
| **Platform type** | Web application (mobile-responsive) — native iOS/Android deferred post-traction |
| **Frontend hosting** | Vercel |
| **Backend hosting** | Railway or Render |
| **Database** | PostgreSQL (via Supabase or self-hosted) |
| **Photo storage** | Cloudinary (free tier covers MVP; scales with usage) |
| **Maps** | Google Maps API |
| **Authentication** | Email OTP (Supabase Auth or custom); optional Google OAuth |
| **Analytics** | Google Analytics 4 + Mixpanel |
| **Build approach** | React + Node.js + PostgreSQL (preferred) or Bubble.io (if budget-constrained) |

---

*Last updated: July 2026 — Findari v1.0 Planning & Design phase*
