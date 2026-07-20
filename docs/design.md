# Findari — Design Document

> Screen-by-screen UI design system, layout specifications, and component structure.
> Brand color: #E85C2C (warm orange-red). Mobile-first. 375px base width.

---

## Design Principles

1. **Food-forward.** Photos and ratings are always the hero. Text supports; imagery sells.
2. **Trust at a glance.** Verified badges, review dates, and star breakdowns must be visible without scrolling or tapping.
3. **Abuja-specific.** Neighbourhood names are primary navigation. The platform should feel built for this city, not adapted from a generic template.
4. **Performance over decoration.** No heavy animations. No autoplay. Fast load is a feature.
5. **Thumb-friendly.** All primary actions reachable without stretching. Bottom navigation for primary nav.

---

## Global Layout

### Navigation Bar (Top)
- **Background:** `#E85C2C`
- **Logo:** Bowl + spoon icon + "Abuja Eats" or "Findari" wordmark in white
- **Right actions:** Bell (notifications) + User icon, or Back arrow + Share icon on inner screens
- **Height:** 44px

### Bottom Navigation (Persistent)
- 4 tabs: Home · Search · Saved · Profile
- Active tab: `#E85C2C` icon + label
- Inactive: `var(--color-text-tertiary)`
- Border-top: 0.5px `var(--color-border-tertiary)`

---

## Screen 1: Home / Discovery

### Layout (top to bottom)
1. **Top nav** — logo + bell + user icon
2. **Search bar** — full width, rounded, icon on left, placeholder: "Search restaurants, bukas…"
3. **"Browse by area" label** — 9px uppercase section header
4. **Neighbourhood chips** — horizontal scroll, pill shape, active chip filled #E85C2C
   - Default chips: Wuse 2 · Jabi · Maitama · Guzape · Garki · Asokoro · Utako
5. **"Nearby spots" / "Trending" label** — same section header
6. **Restaurant cards** — stacked list, each card contains:
   - Thumbnail icon (32×32, rounded 6px) — left
   - Restaurant name (10px, semibold)
   - Star rating (gold ★ at 9px)
   - Cuisine type · Neighbourhood · Price range (9px, secondary + orange)
7. **Bottom navigation**

### Restaurant Card Component
```
┌──────────────────────────────────────┐
│ [ICON] Restaurant Name               │
│        ★★★★★                         │
│        Cuisine · Area · ₦1k–3k      │
└──────────────────────────────────────┘
```
- Background: `var(--color-background-secondary)`
- Border radius: 8px
- Padding: 7px 8px
- Gap between icon and text: 7px

---

## Screen 2: Restaurant Profile

### Layout (top to bottom)
1. **Top bar** — back arrow + "Restaurant" label + share icon (all white on orange)
2. **Hero image** — full width, 55px height in wireframe (expand to ~200px on real implementation), background placeholder if no photo
3. **Restaurant name** — 16px, semibold, primary text
4. **Sub-heading** — cuisine + neighbourhood, 12px, secondary text
5. **Status badges row:**
   - Open Now badge — green bg `#EAF3DE`, green text `#3B6D11`, clock icon + "Open now · closes Xpm"
   - Price range badge — orange bg `#FFF0EB`, dark orange text `#993C1D`, "₦1,500–₦4,000"
6. **Rating block:**
   - Large number (4.7) — 20px, semibold
   - Three rating bars: Food / Service / Ambience
   - Bar track: `var(--color-border-tertiary)`, fill: `#E85C2C`, height 4px
7. **"Write a review" button** — full width, orange, rounded 7px
8. **Reviews list** — each review:
   - Avatar (initials, 18px circle, `#FFF0EB` bg, `#E85C2C` text)
   - Reviewer name (9px, semibold) + Verified badge + Date (right-aligned)
   - Stars (9px gold)
   - Review text (9px, secondary, 1.4 line height)
9. **Bottom navigation**

### Rating Bar Component
```
Food     [████████░░]
Service  [██████░░░░]
Ambience [███████░░░]
```

### Review Item Component
```
┌──────────────────────────────────────┐
│ [AO] Amaka O.  ✓ Verified    2d ago │
│ ★★★★★                               │
│ Best egusi soup in Jabi...           │
└──────────────────────────────────────┘
```

---

## Screen 3: Write a Review

### Layout (top to bottom)
1. **Top bar** — X (cancel) + "Write a review" label + "Post" button (white, 10px)
2. **Restaurant name** — 10px, semibold, reminder of which spot they're reviewing
3. **"Overall rating" label** — 9px, form label style
4. **Star selector** — 5 large interactive stars (14px each), gold when selected
5. **"Rate by category" label**
6. **Sub-ratings** — Food / Service / Ambience, each with mini 5-star selector inline
7. **"Your review" label**
8. **Text area** — rounded, placeholder: "Tell others what you thought…", min-height 38px, expands
9. **"Add photos" label**
10. **Photo upload zone** — dashed border, camera icon, "Tap to add up to 5 photos", thumbnail row appears after selection
11. **"Post review" button** — full width, orange, disabled until minimum requirements met

### Validation States
- Stars not selected → stars pulse gently (CSS animation)
- Text too short → "Please write at least 20 characters" hint appears inline
- Post button disabled until: 1 star selected + text ≥ 20 chars

---

## Screen 4: User Profile

### Layout (top to bottom)
1. **Top bar** — "My Profile" label + settings icon
2. **Avatar** — 36px circle, initials, `#FFF0EB` bg, `#E85C2C` text
3. **Display name** — 14px, semibold
4. **Location + join date** — "Abuja · Joined June 2026", 11px, secondary
5. **Stats bar** — 3 equal-width pill boxes:
   - Reviews · Saved · Avg given
   - Value: 14px semibold · Label: 9px tertiary
6. **"Recent reviews" section header**
7. **Review cards** — compact: restaurant name + stars (right) + date + verified
8. **"Saved spots" section header**
9. **Saved cards** — heart icon + restaurant name + neighbourhood
10. **Bottom navigation** (Profile tab active)

---

## Screen 5: Business Dashboard

### Layout (top to bottom)
1. **Top bar** — building icon + "Business" label + settings icon
2. **Business header card** — `#FFF0EB` bg, business name in `#E85C2C`, "Verified business · [Neighbourhood]" in `#993C1D`
3. **Metrics grid** — 2×2 grid:
   - Avg rating | Total reviews
   - Profile views | Views this week
   - Each cell: `var(--color-background-secondary)`, value 14px semibold, label 8px tertiary
4. **"Recent reviews to respond to" section header**
5. **Review respond cards** — avatar + name + stars (right) | review excerpt | "Reply to this review" outline button
6. **"Edit listing info" button** — full width, outline style (border `#E85C2C`, text `#E85C2C`)

---

## Component Library Reference

### Buttons
```
Primary:   bg #E85C2C · text white · radius 7px · padding 6px 10px · font 10px 500
Outline:   border 0.5px #E85C2C · text #E85C2C · transparent bg
Disabled:  bg #ccc · text white · cursor not-allowed
```

### Badges
```
Open Now:  bg #EAF3DE · text #3B6D11 · radius 4px · pad 2px 5px · 8px 500
Closed:    bg #FCEBEB · text #A32D2D
Price:     bg #FFF0EB · text #993C1D · radius 4px · pad 2px 5px · 8px 500
Verified:  bg #EAF3DE · text #3B6D11 · radius 4px · pad 1px 4px · 7px
```

### Form Inputs
```
Background: var(--color-background-secondary)
Border:     0.5px solid var(--color-border-tertiary)
Radius:     6px
Padding:    6px 7px
Font:       9px secondary text color
Focus:      border-color #E85C2C · outline none
```

### Avatar (Initials)
```
Small (18px): circle · bg #FFF0EB · text #E85C2C · 8px 500
Large (36px): circle · bg #FFF0EB · text #E85C2C · 14px 500
```

---

## Responsive Breakpoints

| Breakpoint | Width | Notes |
|---|---|---|
| Mobile (base) | 375px | Primary design target |
| Mobile L | 425px | Slightly more card width |
| Tablet | 768px | 2-column card grid on home/search |
| Desktop | 1024px+ | 3-column grid; side nav replaces bottom nav |

On tablet and desktop: restaurant profile layout becomes side-by-side (info left, map/photos right).
