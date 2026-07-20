# Findari — Style Guide

> Design tokens, CSS variables, typography, spacing, and component styles.
> Stack: Tailwind CSS (recommended) or plain CSS with custom properties.

---

## Color Palette

### Brand Colors
```css
:root {
  --color-primary:        #E85C2C;  /* Main orange-red — buttons, active states, logo */
  --color-primary-light:  #FFF0EB;  /* Soft background — avatar fills, chip backgrounds */
  --color-primary-dark:   #993C1D;  /* Hover states, dark subtext on light backgrounds */
  --color-accent-gold:    #F5A623;  /* Star ratings only */
}
```

### Neutral Colors
```css
:root {
  --color-text-primary:      #1A1A1A;  /* Headings, bold labels */
  --color-text-secondary:    #4A4A4A;  /* Body text, sublabels */
  --color-text-tertiary:     #9A9A9A;  /* Placeholders, metadata, timestamps */

  --color-background-primary:   #FFFFFF;
  --color-background-secondary: #F7F7F7;  /* Cards, inputs, secondary surfaces */

  --color-border-primary:    #D0D0D0;
  --color-border-secondary:  #E0E0E0;
  --color-border-tertiary:   #EBEBEB;  /* Hairlines, dividers */
}
```

### Semantic Colors
```css
:root {
  --color-success-bg:    #EAF3DE;
  --color-success-text:  #3B6D11;

  --color-error-bg:      #FCEBEB;
  --color-error-text:    #A32D2D;

  --color-warning-bg:    #FFF8E1;
  --color-warning-text:  #7A5700;
}
```

---

## Typography

### Font Stack
```css
:root {
  --font-sans: 'Inter', 'DM Sans', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

body {
  font-family: var(--font-sans);
  font-size: 14px;
  line-height: 1.5;
  color: var(--color-text-primary);
  -webkit-font-smoothing: antialiased;
}
```

### Scale
```css
/* Mobile scale (base) */
.text-2xs  { font-size: 7px; }
.text-xs   { font-size: 8px; }
.text-sm   { font-size: 9px; }
.text-base { font-size: 10px; }
.text-md   { font-size: 11px; }
.text-lg   { font-size: 12px; }
.text-xl   { font-size: 14px; }
.text-2xl  { font-size: 16px; }
.text-3xl  { font-size: 20px; }

/* Weight */
.font-normal   { font-weight: 400; }
.font-medium   { font-weight: 500; }
.font-semibold { font-weight: 600; }
```

---

## Spacing

```css
:root {
  --space-1:  4px;
  --space-2:  6px;
  --space-3:  8px;
  --space-4:  10px;
  --space-5:  12px;
  --space-6:  16px;
  --space-7:  20px;
  --space-8:  24px;
  --space-9:  32px;
  --space-10: 40px;
}
```

---

## Border Radius
```css
:root {
  --radius-sm:  4px;   /* Badges, labels */
  --radius-md:  6px;   /* Inputs, small cards */
  --radius-lg:  8px;   /* Restaurant cards, review items */
  --radius-xl:  10px;  /* Modal containers */
  --radius-2xl: 16px;  /* Phone frames (wireframes only) */
  --radius-full: 9999px; /* Chips, avatars */
}
```

---

## Shadows
```css
:root {
  --shadow-xs: 0 1px 2px rgba(0,0,0,0.05);
  --shadow-sm: 0 2px 4px rgba(0,0,0,0.08);
  --shadow-md: 0 4px 12px rgba(0,0,0,0.10);
  --shadow-lg: 0 8px 24px rgba(0,0,0,0.12);
}
```

---

## Component Tokens

### Buttons
```css
.btn-primary {
  background: var(--color-primary);
  color: #ffffff;
  border: none;
  border-radius: var(--radius-lg);
  padding: 12px 16px;
  font-size: 14px;
  font-weight: 500;
  width: 100%;
  cursor: pointer;
  transition: background 0.15s ease;
}
.btn-primary:hover  { background: var(--color-primary-dark); }
.btn-primary:active { opacity: 0.9; }
.btn-primary:disabled { background: #ccc; cursor: not-allowed; }

.btn-outline {
  background: transparent;
  color: var(--color-primary);
  border: 1px solid var(--color-primary);
  border-radius: var(--radius-lg);
  padding: 11px 16px;
  font-size: 14px;
  font-weight: 500;
  width: 100%;
  cursor: pointer;
  transition: all 0.15s ease;
}
.btn-outline:hover { background: var(--color-primary-light); }
```

### Chips / Neighbourhood Filters
```css
.chip {
  background: var(--color-background-secondary);
  border: 0.5px solid var(--color-border-tertiary);
  border-radius: var(--radius-full);
  padding: 6px 14px;
  font-size: 12px;
  color: var(--color-text-secondary);
  cursor: pointer;
  white-space: nowrap;
  transition: all 0.15s ease;
}
.chip:hover  { border-color: var(--color-primary); color: var(--color-primary); }
.chip.active { background: var(--color-primary); color: #fff; border-color: var(--color-primary); }
```

### Search Bar
```css
.search-bar {
  background: var(--color-background-secondary);
  border: 1px solid var(--color-border-tertiary);
  border-radius: var(--radius-lg);
  padding: 12px 14px;
  display: flex;
  align-items: center;
  gap: 10px;
  transition: border-color 0.15s ease;
}
.search-bar:focus-within { border-color: var(--color-primary); }
.search-bar input {
  background: none;
  border: none;
  outline: none;
  font-size: 14px;
  color: var(--color-text-primary);
  flex: 1;
}
.search-bar input::placeholder { color: var(--color-text-tertiary); }
```

### Restaurant Card
```css
.resto-card {
  background: var(--color-background-secondary);
  border-radius: var(--radius-lg);
  padding: 12px 14px;
  display: flex;
  gap: 12px;
  align-items: flex-start;
  cursor: pointer;
  transition: box-shadow 0.15s ease;
}
.resto-card:hover { box-shadow: var(--shadow-sm); }
```

### Badges
```css
.badge-open {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  background: var(--color-success-bg);
  color: var(--color-success-text);
  border-radius: var(--radius-sm);
  padding: 3px 8px;
  font-size: 12px;
  font-weight: 500;
}
.badge-closed {
  background: var(--color-error-bg);
  color: var(--color-error-text);
}
.badge-price {
  background: var(--color-primary-light);
  color: var(--color-primary-dark);
  border-radius: var(--radius-sm);
  padding: 3px 8px;
  font-size: 12px;
  font-weight: 500;
}
.badge-verified {
  background: var(--color-success-bg);
  color: var(--color-success-text);
  border-radius: var(--radius-sm);
  padding: 1px 5px;
  font-size: 10px;
}
```

### Stars
```css
.stars {
  color: var(--color-accent-gold); /* #F5A623 */
  font-size: 14px;
  letter-spacing: 1px;
}
.stars .empty { color: var(--color-border-secondary); }
```

### Avatar
```css
.avatar {
  border-radius: var(--radius-full);
  background: var(--color-primary-light);
  color: var(--color-primary);
  font-weight: 500;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}
.avatar-sm { width: 28px; height: 28px; font-size: 11px; }
.avatar-md { width: 40px; height: 40px; font-size: 14px; }
.avatar-lg { width: 56px; height: 56px; font-size: 20px; }
```

### Form Inputs
```css
.form-input {
  background: var(--color-background-secondary);
  border: 1px solid var(--color-border-tertiary);
  border-radius: var(--radius-md);
  padding: 10px 12px;
  font-size: 14px;
  color: var(--color-text-primary);
  width: 100%;
  transition: border-color 0.15s ease;
}
.form-input:focus { outline: none; border-color: var(--color-primary); }
.form-input::placeholder { color: var(--color-text-tertiary); }

.form-textarea {
  resize: vertical;
  min-height: 80px;
  line-height: 1.5;
}
```

### Photo Upload Zone
```css
.photo-upload {
  border: 1.5px dashed var(--color-border-secondary);
  border-radius: var(--radius-md);
  padding: 20px;
  text-align: center;
  cursor: pointer;
  transition: border-color 0.15s ease;
}
.photo-upload:hover { border-color: var(--color-primary); }
```

---

## Top Navigation Bar
```css
.nav-bar {
  background: var(--color-primary);
  padding: 12px 16px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: sticky;
  top: 0;
  z-index: 100;
}
.nav-bar .logo { font-size: 16px; font-weight: 500; color: #fff; }
.nav-bar .nav-icon { font-size: 20px; color: rgba(255,255,255,0.9); cursor: pointer; }
```

## Bottom Navigation Bar
```css
.bottom-nav {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 8px 0 12px;
  border-top: 0.5px solid var(--color-border-tertiary);
  background: var(--color-background-primary);
  position: fixed;
  bottom: 0;
  left: 0; right: 0;
  z-index: 100;
}
.bnav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 3px;
  cursor: pointer;
}
.bnav-item .icon { font-size: 22px; color: var(--color-text-tertiary); }
.bnav-item .label { font-size: 10px; color: var(--color-text-tertiary); }
.bnav-item.active .icon  { color: var(--color-primary); }
.bnav-item.active .label { color: var(--color-primary); }
```

---

## Accessibility

- All interactive elements have minimum 44×44px touch target
- Colour contrast: primary text on white background ≥ 4.5:1
- All images have descriptive alt text
- Form fields have visible labels (not just placeholders)
- Error states are never communicated by colour alone — always pair with icon or text
- Focus states visible on all interactive elements (outline: 2px solid var(--color-primary))
