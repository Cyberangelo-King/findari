# Findari (Abuja Eats)

**Abuja's first dedicated platform for discovering, rating, and reviewing local restaurants, bukas, cafés, and food spots.**

> Built by Abuja people, for Abuja people.

---

## Documentation

All product documentation lives in `docs/`. Start with `master-prompt.md` when building.

| File | Description |
|---|---|
| [`master-prompt.md`](docs/master-prompt.md) | **Start here.** Entry point for AI-assisted builds; references all other docs |
| [`prd.md`](docs/prd.md) | Product Requirements Document — features, priorities, user journeys |
| [`features-and-functions.md`](docs/features-and-functions.md) | Detailed feature breakdown by screen and user type |
| [`trd.md`](docs/trd.md) | Technical requirements — database schema, API endpoints, architecture |
| [`design.md`](docs/design.md) | Screen-by-screen UI design and component structure |
| [`style.md`](docs/style.md) | Design tokens, CSS, typography, spacing |
| [`copy.md`](docs/copy.md) | All UI text, CTAs, error messages, email templates |
| [`user-workflow.md`](docs/user-workflow.md) | Step-by-step user flows with realistic scenarios |
| [`goals.md`](docs/goals.md) | Business, product, and user goals |
| [`brand.md`](docs/brand.md) | Visual identity, brand personality, logo, voice |

---

## Product Summary

Findari solves a real Abuja problem: people have no reliable place to find honest reviews of local food spots before spending their money. Survey data from 17 Abuja residents (June 2026) confirmed:
- **94%** would use a dedicated Abuja food review app
- **58.8%** currently rely on word of mouth
- **94%** have been disappointed by a restaurant with no prior information

### MVP Features
- Restaurant search by name, cuisine, and neighbourhood (Wuse, Jabi, Maitama, Guzape, etc.)
- Verified reviews with photo uploads (up to 5 per review)
- Price range display in Naira (₦)
- Open Now indicator
- Star breakdown: Food / Service / Ambience
- Business listing claim + owner dashboard
- Google Maps embed on every profile

### Tech Stack
- **Frontend:** React (Vite) + Tailwind CSS → Vercel
- **Backend:** Node.js + Express → Render / Railway
- **Database:** PostgreSQL
- **Auth:** Email OTP + optional Google OAuth
- **Photos:** Cloudinary
- **Maps:** Google Maps API

---

## Phase Timeline

| Phase | Status |
|---|---|
| Phase 1 — Research & Validation | ✅ Complete |
| Phase 2 — Planning & Design | 🔄 In Progress |
| Phase 3 — Build MVP | Months 2–5 |
| Phase 4 — Testing | Months 5–6 |
| Phase 5 — Launch | Months 6–7 |
| Phase 6 — Growth | Month 7+ |

---

*Prepared by Zia the Creator · June 2026*
