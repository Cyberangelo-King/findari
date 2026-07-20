# Findari — Risks & Contingencies

> Honest risk assessment for building Findari with Google AI Studio as a web application.
> Every risk has a likelihood rating (🔴 High / 🟡 Medium / 🟢 Low), an impact rating, and a concrete mitigation plan.

---

## Part 1: AI Studio Build Risks

### Risk 1: AI Studio generates code that looks right but breaks on mobile
**Likelihood:** 🔴 High | **Impact:** High

**What happens:** AI Studio often defaults to desktop-first layouts. The output might look correct in the browser preview but break on a real phone — buttons too small, content overflowing, inputs not zooming correctly.

**Mitigation:**
- After each screen is generated, open it on your actual phone (use a local server or drag the HTML file into Chrome mobile sim via DevTools → Toggle device toolbar → iPhone SE 375px)
- Add this check to your correction prompt: *"Test at 375px width. Fix any overflow, ensure all tap targets are at least 44px, and confirm the layout stacks vertically not horizontally."*
- Check inputs specifically: iOS Safari zooms in on inputs with font-size < 16px. Tell AI Studio: *"All form inputs must have font-size: 16px minimum to prevent iOS zoom."*

---

### Risk 2: AI Studio loses context between sessions
**Likelihood:** 🔴 High | **Impact:** High

**What happens:** Each AI Studio session starts fresh. By Screen 3 or 4, AI Studio will not remember the design system, component styles, or decisions made in earlier sessions. Output will drift — different colours, different spacing, inconsistent component styles.

**Mitigation:**
- **Always paste the CSS variables block at the top of every new session prompt** — it's in the master prompt above, copy it every time
- Keep a single `styles.css` file. After each session, copy the CSS AI Studio generated into this file. Share the file path or paste the current version at the start of each new session
- Do not start Screen N until you've saved the CSS from Screen N-1
- Create a `base.html` template file (head, nav, bottom nav, CSS link) — paste it at the start of each session and say "extend this base file"

---

### Risk 3: AI Studio cannot build the backend
**Likelihood:** 🔴 High (certainty) | **Impact:** High

**What happens:** AI Studio builds the UI. It cannot spin up a Node.js server, connect to PostgreSQL, handle OTP emails, or manage Cloudinary uploads. The frontend it generates will be static — no real data, no real auth, no real reviews.

**Mitigation:**
- **This is expected.** Plan your build in two phases:
  - Phase A: AI Studio builds all screens as static HTML/JS (what it's good at)
  - Phase B: You or a developer connects a backend (see `post-build-guide.md`)
- For Phase A, use hardcoded sample data — the realistic restaurant names in `master-prompt.md`
- Mock the auth flow: build the OTP screens but use a hardcoded "correct" OTP (e.g. `123456`) for testing the frontend only
- Use localStorage to fake "logged in" state during frontend development

---

### Risk 4: AI Studio outputs inconsistent code quality
**Likelihood:** 🟡 Medium | **Impact:** Medium

**What happens:** Sometimes AI Studio writes clean, semantic HTML with good CSS. Other times it produces deeply nested divs, inline styles, `!important` everywhere, or JavaScript that works once then breaks.

**Mitigation:**
- **Always review the output before pasting it into your project** — read it, don't just copy-paste blindly
- If the code is messy, tell AI Studio: *"Refactor this code to use semantic HTML5 elements (`<nav>`, `<main>`, `<article>`, `<section>`). Remove all inline styles. Move all styles to the `<style>` block. Remove any `!important` declarations."*
- After finishing all screens, do one final session: *"Review all the code I've shared. Identify and fix: duplicate CSS rules, inconsistent component naming, and any inline styles."*

---

### Risk 5: Interactive JavaScript features don't work correctly
**Likelihood:** 🟡 Medium | **Impact:** Medium

**What happens:** The star rating selector, photo upload preview, disabled Post button logic, and OTP auto-advance inputs require working JavaScript. AI Studio sometimes gets these partially right — they look correct but have edge case bugs.

**Mitigation:**
- Test every interactive element manually and thoroughly after each session
- For the star selector specifically: click each star in order (1 through 5), then click backwards. Verify fill state updates correctly in both directions
- For the Post button disabled state: type 19 characters → button should stay disabled. Type the 20th → button should enable. Delete back to 19 → button should disable again
- For OTP input: type a digit → cursor should auto-move to next box. Paste all 6 digits at once → all boxes should fill
- If any of these fail, paste the broken JavaScript back into AI Studio and say: *"This JavaScript has a bug. [Describe exactly what happens vs. what should happen]. Fix it."*

---

### Risk 6: Google Maps integration breaks
**Likelihood:** 🟡 Medium | **Impact:** Medium

**What happens:** Google Maps requires a valid API key. AI Studio will generate the embed code, but without a real key it shows an error state. The key also requires billing to be enabled on your Google Cloud account, which costs money for high usage.

**Mitigation:**
- Create a Google Cloud account and enable the Maps JavaScript API before starting Screen 2
- Restrict your API key to your domain only (prevents abuse charges)
- The free tier covers ~28,000 map loads per month — more than enough for MVP
- If you want to avoid Maps entirely for now: replace the map with a link — "Open in Google Maps" button that deep-links using the restaurant's coordinates. AI Studio can build this as a fallback.

---

### Risk 7: Cloudinary photo upload doesn't work from the frontend
**Likelihood:** 🟡 Medium | **Impact:** Medium

**What happens:** Cloudinary direct uploads from the browser require a signed upload preset. AI Studio will generate the upload code, but if the preset isn't configured correctly in your Cloudinary account, photos won't save.

**Mitigation:**
- Create a Cloudinary account (free tier is enough for MVP)
- In Cloudinary dashboard: Settings → Upload → Add upload preset → set to "Unsigned" → copy the preset name
- When AI Studio generates the upload code, replace `YOUR_CLOUD_NAME` and `YOUR_UPLOAD_PRESET` with your real values
- Test photo upload on one screen before connecting it to all screens
- Size limit: Set max file size to 5MB in both the HTML `accept` attribute and Cloudinary preset settings

---

## Part 2: Product & Business Risks

### Risk 8: You don't have 100 restaurant listings at launch
**Likelihood:** 🟡 Medium | **Impact:** High

**What happens:** An empty or sparse restaurant directory makes the platform feel dead. Users who visit and see only 12 listings will not return.

**Mitigation:**
- Start building the restaurant database now, before the site is live
- Use public sources: Google Maps listings for Abuja, Zomato Nigeria data, Instagram restaurant accounts
- Assign the data collection to someone: 2 hours of research can produce 100 listings in a spreadsheet
- Build a CSV bulk import into the admin panel — far faster than adding one by one
- Never launch publicly with fewer than 80 complete listings (name + neighbourhood + cuisine + price + hours)

---

### Risk 9: Fake or malicious reviews appear early
**Likelihood:** 🟡 Medium | **Impact:** High

**What happens:** Restaurant owners may post fake positive reviews for themselves. Competitors may post fake negative reviews. Early on, you are the only moderator.

**Mitigation:**
- OTP verification is the first line of defence — it prevents fully anonymous abuse
- Build the review flagging system from day one, not as an afterthought
- In the first 90 days: review every single submission manually. At 200 reviews/day you'll need automation; at 5–10 reviews/day (realistic early stage) manual is fine
- Watch for these red flags: multiple reviews from the same IP, reviews posted within minutes of account creation, reviews with no photos or extremely generic text
- If a review is clearly fake, remove it and ban the account. Document your policy in writing before launch

---

### Risk 10: Business owners get defensive or threatening
**Likelihood:** 🟡 Medium | **Impact:** Medium

**What happens:** A restaurant owner discovers a 2-star review on your platform and contacts you demanding removal. Some may threaten legal action.

**Mitigation:**
- Publish a clear, specific defamation and content moderation policy before launch — this is your legal shield
- You are not liable for user-submitted reviews under standard platform liability rules in Nigeria (NDPR covers data, not defamation — research this with a lawyer)
- Your response policy: reviews that are factually inaccurate can be disputed. Reviews that are opinions ("the food was bad") are protected. Reviews that contain personal attacks on staff (not the business) should be edited or removed
- Build a "Request review investigation" flow for business owners — they submit a dispute, you review within 48 hours. This manages anger without automatic removal
- Never remove a valid negative review because an owner complained. This destroys trust with reviewers and the platform's credibility

---

### Risk 11: Low user return rate (platform feels useless after first visit)
**Likelihood:** 🟡 Medium | **Impact:** High

**What happens:** Users visit once to look something up, then never return. The platform has no pull to bring them back.

**Mitigation:**
- Email digest: "New reviews in Jabi this week" — simple weekly email to registered users
- "Your review helped X people this week" notifications — small but effective ego trigger
- Social sharing: make every restaurant profile shareable with a clean preview card (OG meta tags) so users share via WhatsApp and drive others back
- Business owner engagement: active owners who respond to reviews create activity that pulls reviewers back to check

---

### Risk 12: NDPR compliance gap
**Likelihood:** 🟢 Low | **Impact:** High

**What happens:** Nigeria Data Protection Regulation (NDPR) requires you to have a privacy policy, obtain consent before collecting personal data, and allow users to request deletion of their data. Failure is technically a legal risk.

**Mitigation:**
- Write and publish a privacy policy before public launch. This can be a simple page, but it must exist
- Add a checkbox at signup: "I agree to the Privacy Policy and Terms of Service" — store the acceptance timestamp in your database
- Build a "Delete my account" flow — it doesn't need to be automated at launch; a "mailto" link to your email is acceptable for MVP
- Register with NITDA (the Nigerian data protection authority) if your user base exceeds a certain threshold — check current thresholds

---

## Contingency Playbook

### If Google AI Studio produces code that won't connect to a real backend:
→ Use the static HTML output as a prototype. Show it to early users for feedback. Then hire a developer (or use Supabase — see `post-build-guide.md`) to add real functionality.

### If you run out of time before launch:
→ Cut in this order: Business Dashboard → Friends' Reviews → Save feature → Cuisine filter → Open Now (if hours data is incomplete)
→ Never cut: Search, Verified reviews, Price display, Photo uploads, Google Maps

### If the platform gets no traffic after launch:
→ Do not spend money on ads in the first 30 days
→ Manual outreach: message 50 Abuja food Instagram accounts directly. Offer to give their favourite restaurant a free "featured" listing for the first 90 days
→ Post in Abuja-focused Facebook groups and WhatsApp communities — find 10, post once per week
→ Review your own top 5 restaurants to seed the content

### If a key third-party service goes down (Cloudinary, Google Maps, etc.):
→ **Cloudinary outage:** Build in an error state — "Photo upload unavailable right now" — so users can still post text-only reviews
→ **Google Maps outage:** Show the restaurant address as plain text with a "Get directions" link to `maps.google.com/?q=[address]`
→ **Email OTP failure:** Have Africa's Talking SMS OTP as a backup — the TRD already includes this
