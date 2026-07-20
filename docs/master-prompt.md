# Findari — Master Build Prompt (Google AI Studio Edition)

> **HOW TO USE THIS FILE:**
> Open Google AI Studio. Create a new prompt. Paste the entire contents of this file into the system prompt box. Then paste the contents of each referenced doc file one by one when AI Studio asks for more context. Start building screen by screen — do not ask it to build everything at once.

---

## What You Are Building

**Findari** (formerly Abuja Eats) is a mobile-first web application for discovering, rating, and reviewing restaurants and food spots in Abuja, Nigeria. It is a review-and-discovery platform — not a delivery app, not a booking platform. Think Yelp, built for Abuja.

**Your job:** Generate clean, working HTML/CSS/JavaScript (or React, depending on session) for each screen I describe. Follow the design specs, use the exact colour tokens provided, and write code I can drop directly into my project.

---

## Tech Stack for This Build

Use this stack. Do not deviate without being asked.

```
Frontend:   HTML5 + CSS (custom properties) + Vanilla JavaScript
            OR React (Vite) if the session supports it

Styling:    CSS custom properties (no frameworks unless asked)
            Tailwind CDN is acceptable if setup is requested

Icons:      Tabler Icons via CDN
            <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/tabler-icons.min.css">

Fonts:      Inter via Google Fonts
            <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&display=swap" rel="stylesheet">

Maps:       Google Maps JavaScript API (I will supply my API key)

Photos:     Cloudinary (I will supply cloud name and upload preset)

Auth:       Email OTP — backend handles this; frontend just renders the form

Backend:    Node.js + Express (built separately — AI Studio handles frontend only)

Database:   PostgreSQL (schema is in trd.md — backend concern only)
```

---

## Design System (Must Memorise)

Apply these tokens to every component you generate. Never hardcode colours — always use the CSS variable names.

```css
:root {
  /* Brand */
  --color-primary:        #E85C2C;
  --color-primary-light:  #FFF0EB;
  --color-primary-dark:   #993C1D;
  --color-accent-gold:    #F5A623;

  /* Text */
  --color-text-primary:   #1A1A1A;
  --color-text-secondary: #4A4A4A;
  --color-text-tertiary:  #9A9A9A;

  /* Surfaces */
  --color-bg-primary:     #FFFFFF;
  --color-bg-secondary:   #F7F7F7;

  /* Borders */
  --color-border-primary:   #D0D0D0;
  --color-border-secondary: #E0E0E0;
  --color-border-tertiary:  #EBEBEB;

  /* Semantic */
  --color-success-bg:   #EAF3DE;
  --color-success-text: #3B6D11;
  --color-error-bg:     #FCEBEB;
  --color-error-text:   #A32D2D;

  /* Spacing */
  --space-1: 4px;   --space-2: 6px;   --space-3: 8px;
  --space-4: 10px;  --space-5: 12px;  --space-6: 16px;
  --space-7: 20px;  --space-8: 24px;  --space-9: 32px;

  /* Radius */
  --radius-sm:   4px;
  --radius-md:   6px;
  --radius-lg:   8px;
  --radius-xl:   10px;
  --radius-full: 9999px;

  /* Shadows */
  --shadow-sm: 0 2px 4px rgba(0,0,0,0.08);
  --shadow-md: 0 4px 12px rgba(0,0,0,0.10);

  /* Font */
  --font-sans: 'Inter', -apple-system, sans-serif;
}
```

---

## Non-Negotiable Rules

Every file you generate must follow these rules. No exceptions.

1. **Mobile-first, always.** Base styles target 375px. Tablet (768px) and desktop (1024px) via media queries.
2. **No anonymous reviews.** Never render a review form without an auth check. If user is not logged in, show the signup prompt inline.
3. **Price in Naira only.** Display all amounts as `₦X,XXX` — never dollars, euros, or unformatted numbers.
4. **Open Now is calculated, not guessed.** The badge only appears when business hours data exists. If hours are null/empty, render nothing — not "Unknown".
5. **Thumb-friendly targets.** All buttons and tap targets minimum 44×44px.
6. **No delivery or booking features.** If I ask for these by accident, remind me they are out of scope.
7. **Performance.** No autoplay media. Lazy-load images below the fold. No blocking scripts in `<head>`.
8. **Accessibility.** Semantic HTML. Alt text on all images. Labels on all inputs — not just placeholders. Focus states visible.

---

## Build Order (Follow This Sequence)

Build one screen at a time. Complete and verify each before moving to the next.

### Screen 1: Home / Discovery
- Top nav (orange, logo + bell + profile icon)
- Search bar (full width, rounded)
- "Browse by area" neighbourhood chips (horizontal scroll: Wuse 2, Jabi, Maitama, Guzape, Garki, Asokoro, Utako)
- "Nearby spots" section with 3 restaurant cards
- Bottom navigation (Home · Search · Saved · Profile)
- Active state: Home

### Screen 2: Restaurant Profile
- Top nav (back arrow + "Restaurant" label + share icon)
- Hero image placeholder (full width, 200px tall, grey bg)
- Restaurant name, cuisine + neighbourhood sub-heading
- Open Now badge (green) + Price range badge (orange)
- Rating block: big number + Food/Service/Ambience bars
- "Write a review" primary button
- Review list (show 3 sample reviews with avatar, verified badge, date, stars, text)
- Bottom navigation

### Screen 3: Write a Review
- Top nav (X button + "Write a review" + "Post" text button)
- Restaurant name sub-header
- Overall star selector (interactive, 5 stars)
- Sub-category ratings (Food / Service / Ambience — mini star selectors)
- Review text area (min 20 chars validation)
- Photo upload zone (dashed border, camera icon, "Tap to add up to 5 photos")
- Post button (disabled until star selected + 20 chars)

### Screen 4: User Profile
- Top nav ("My Profile" + settings icon)
- Avatar circle (initials)
- Display name + "Abuja · Joined June 2026"
- Stats bar (Reviews · Saved · Avg given)
- Recent reviews list (compact)
- Saved spots list
- Bottom navigation (Profile active)

### Screen 5: Business Dashboard
- Top nav (building icon + "Business" + settings icon)
- Business header card (orange-light background, business name, verified status)
- 2×2 metrics grid (Avg rating · Reviews · Profile views · This week)
- Recent review cards with "Reply to this review" outline button
- "Edit listing info" outline button
- Bottom navigation

### Screen 6: Auth Flow (OTP)
- Email entry screen: headline "Join Abuja Eats", email input, "Send code" button
- OTP entry screen: "Check your inbox", 6-digit OTP field, "Verify" button, "Resend code" link
- Profile setup screen: name input, neighbourhood input, "Let's go" button

### Screen 7: Business Claim Flow
- "Claim this business" modal/page
- Business email, phone, CAC number (optional) fields
- "Submit claim" button
- Confirmation screen: "We're reviewing your claim"

---

## How to Prompt AI Studio — Session by Session

**Session 1 — Global styles + Screen 1 (Home)**
```
"Build Screen 1: the Home / Discovery screen for Findari. Apply the CSS design system exactly as specified. Output a single complete HTML file with embedded CSS. Make it mobile-first at 375px base width. Show 3 sample restaurant cards with realistic Nigerian restaurant names."
```

**Session 2 — Screen 2 (Restaurant Profile)**
```
"Build Screen 2: the Restaurant Profile page for Findari. Use the same CSS variables from Screen 1. Show a sample restaurant called 'Mama Titi's Kitchen' in Jabi. Include an Open Now badge (green), price badge ₦1,500–₦4,000, a 4.7 rating with Food/Service/Ambience breakdown bars, and 3 sample reviews with Nigerian reviewer names and verified badges."
```

**Session 3 — Screen 3 (Write a Review)**
```
"Build Screen 3: the Write a Review form for Findari. The overall star selector must be interactive (clicking a star fills it and all stars before it). The Post button must be disabled until at least 1 star is selected AND the text area has at least 20 characters. Show a character counter. The photo upload zone should preview thumbnails after selection."
```

**Session 4 — Screens 4 & 5 (Profile + Dashboard)**
```
"Build Screen 4 (User Profile) and Screen 5 (Business Dashboard) for Findari. These are separate pages. Use consistent CSS variables."
```

**Session 5 — Auth + Business Claim**
```
"Build the Auth flow (email OTP) and the Business Claim flow for Findari. The OTP screen should have 6 individual digit input boxes that auto-advance focus on entry."
```

**Session 6 — Connect All Screens**
```
"Now create a navigation layer that connects all 5 screens. The bottom nav should route between Home, Search (same as Home for now), Saved, and Profile. Restaurant cards on the home screen should link to the profile page. The 'Write a review' button on the profile page should open the review form."
```

---

## Sample Data to Use

Use these realistic Nigerian names and restaurant names throughout. Do not use "Lorem ipsum" or "Restaurant A".

**Restaurants:**
- Mama Titi's Kitchen — Local Nigerian — Jabi — ₦1,500–₦4,000 — 4.7★
- Bukka Hut Wuse 2 — Local Nigerian — Wuse 2 — ₦1,000–₦3,000 — 4.5★
- Zinc Café Maitama — Café — Maitama — ₦2,000–₦5,000 — 4.2★
- Abuja Suya Spot — Suya/Grills — Garki — ₦800–₦2,000 — 4.8★
- Nomad Restaurant — Continental — Guzape — ₦4,000–₦10,000 — 4.3★
- Yellow Chilli Wuse — Indian/Nigerian Fusion — Wuse 2 — ₦2,500–₦6,000 — 4.1★

**Reviewer names:**
- Amaka O., Kemi M., Tunde A., Adaeze N., Emeka P., Fatima Y., Bisi O., Chidi E.

**Sample review texts:**
- "Best egusi soup in Jabi. Consistent every time. Highly recommend the ofe onugbu too."
- "Food was good but waited 40 minutes for my order on a weekday afternoon."
- "The suya here is genuinely the best in Abuja. Fresh, well-spiced, not overcooked. Don't sleep on it."
- "Decent café, great coffee, quiet atmosphere. WiFi is reliable which is rare."

---

## When AI Studio Gets Something Wrong

If the output doesn't match the spec, use these correction prompts:

- **Wrong colour:** "The button colour is wrong. Use `var(--color-primary)` which is `#E85C2C`. Do not hardcode hex values — use the CSS variable."
- **Not mobile-first:** "This layout is not mobile-first. Start with 375px as the base. Add tablet styles inside `@media (min-width: 768px)` and desktop inside `@media (min-width: 1024px)`."
- **Missing verified badge:** "Every review must show a '✓ Verified' badge in green (`--color-success-bg` / `--color-success-text`) next to the reviewer name."
- **Post button not disabled:** "The Post button must be disabled (grey, `cursor: not-allowed`) until: (1) at least one star is selected, AND (2) the review text has ≥20 characters. Add a JavaScript event listener to enforce this."
- **Placeholder instead of label:** "Replace the placeholder-only approach with a proper `<label>` element above each input. Labels must be visible at all times — not just inside the field."
