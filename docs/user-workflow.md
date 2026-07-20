# Findari — User Workflows

> Step-by-step user flows with realistic scenarios, decision points, and timing.
> Two primary workflows: Reviewer and Business Owner.

---

## Workflow 1: Diner (Reviewer)

### Scenario
Adaeze lives in Jabi. She heard from a colleague about a restaurant called "Mama Titi's Kitchen" but isn't sure if it's worth trying. She picks up her phone during her lunch break.

---

### Step 1: Discovery
**Entry point:** Google search for "mama titi jabi abuja" or Findari link shared in a WhatsApp group

- Adaeze lands on the Findari home screen
- She sees a search bar and neighbourhood chips
- She taps the search bar and types "Mama Titi"
- Results appear within 2 seconds

*Time: ~15 seconds*

---

### Step 2: Restaurant Profile
- Adaeze taps the result: "Mama Titi's Kitchen"
- She sees the profile:
  - **Open Now** badge — green — closes 10pm
  - **Price range** — ₦1,500–₦4,000
  - **Overall rating** — 4.7 (Food: 4.8 / Service: 4.3 / Ambience: 4.6)
  - **38 reviews**, most recent 2 days ago
- She scrolls through 5–6 reviews — all verified, all with dates
- She spots a photo of the egusi soup she's been told about
- She taps the map to see exactly where it is on Google Maps
- She decides: *I'll go.*
- She taps the heart icon to save it for later reference

*Time: ~2 minutes*

---

### Step 3: First Visit — Review (New User)
Two days later, Adaeze went and loved it. She wants to leave a review.

- She opens Findari, taps on Mama Titi's Kitchen
- Taps "Write a review"
- Prompted to create an account — she enters her email
- OTP sent — she checks her email, enters the code
- Account created, she enters her name ("Adaeze O.") and area ("Jabi")
- She is taken back to the Write a Review screen

*Time: ~1 minute for signup*

---

### Step 4: Writing the Review
- She taps 5 stars overall
- Sets Food: 5, Service: 4, Ambience: 5
- Types her review (65 words):
  *"The egusi soup is exactly what people say — thick, well-seasoned, and the portions are generous. I also had the ofe onugbu and it was excellent. The service was decent, took about 20 minutes for the food but it was worth the wait. The space is simple but clean. Will definitely be back."*
- She uploads 2 photos — one of the egusi, one of the plating
- Taps "Post review"
- Toast: "Your review is live!"

*Time: ~3 minutes*

---

### Step 5: Return Use
The following week, a friend asks Adaeze about a place in Maitama.

- She opens Findari, taps the Maitama chip
- Browses the list, finds the spot, checks reviews
- Shares the listing URL to her friend via WhatsApp in 30 seconds

*Time: ~45 seconds*

---

## Workflow 2: Business Owner

### Scenario
Tunde runs Mama Titi's Kitchen in Jabi. A regular customer told him his restaurant appeared on a food app with some reviews — some positive, one critical. He wants to claim the listing and respond.

---

### Step 1: Finding the Listing
- Tunde searches "Mama Titi" on Findari
- Sees his restaurant listed (auto-generated from public data)
- Taps on it to see the profile
- He reads all 8 reviews — 7 positive, 1 mentioning a 40-minute wait time

*Time: ~3 minutes*

---

### Step 2: Claiming the Listing
- He scrolls to the bottom and taps "Claim this business"
- A modal appears:
  - "Is this your place? Claim your listing to update info, respond to reviews, and track your reputation — for free."
- He enters:
  - Business email: `mamatiti.kitchen@gmail.com`
  - Phone: `+234 803 456 7890`
  - CAC number: (skips — optional)
- Taps "Submit claim"
- Confirmation screen: "We're reviewing your claim. We'll get back to you within 24 hours."

*Time: ~5 minutes*

---

### Step 3: Verification & Access
- 18 hours later, Tunde receives an email: "Your listing claim has been approved"
- He taps the dashboard link in the email
- He's signed in via OTP to the same email he submitted

*Time: ~30 seconds to access dashboard*

---

### Step 4: Dashboard Review
Tunde sees:
- **Avg rating:** 4.7
- **Total reviews:** 38
- **Profile views:** 214
- **This week:** 12 views

He reads the recent unresponded reviews in the dashboard.

---

### Step 5: Responding to the Critical Review
- He finds Kemi M.'s review: "Food was good but waited 40 minutes for my order on a weekday afternoon"
- He taps "Reply to this review"
- Types:
  *"Hi Kemi, thank you for coming in and for the honest feedback. We do sometimes run long during peak hours and we're working on it. We hope you'll give us another chance — and we promise we'll be faster next time!"*
- Taps "Post response"
- The response appears publicly below Kemi's review

*Time: ~4 minutes*

---

### Step 6: Updating Listing Info
- Tunde taps "Edit listing info"
- Updates:
  - Opening hours (his listing had Mon–Sat; he's now open Sundays 12pm–8pm)
  - Adds his phone number
  - Corrects the price range from ₦2,000–₦5,000 to ₦1,500–₦4,000
  - Uploads a better cover photo
- Saves changes — listing updates immediately

*Time: ~5 minutes*

---

## Edge Cases & Error Flows

### User tries to review without an account
- Taps "Write a review"
- Prompt: "Sign in to post a review"
- Inline signup flow — does not leave the page
- Returns to review form with context preserved

### User tries to post a second review for the same restaurant
- System detects existing review
- Shows: "You've already reviewed this spot. Want to edit your existing review?"
- Link takes them to their own review to edit

### Business claim for a restaurant someone else already claimed
- System flags the duplicate
- Shows: "This business has already been claimed. If you believe this is an error, contact us at [email]."

### Flagged review workflow
- User flags review as spam
- Admin receives flag in moderation queue
- Admin reviews within 48 hours
- If removed: review disappears from profile, reviewer receives no notification
- If kept: flag is closed, no action taken

### OTP code expired
- User enters expired OTP
- Error: "That code has expired. Hit 'Resend code' to get a new one."
- New OTP generated and sent; old code invalidated

---

## Mobile-Specific Considerations

- **Photo upload:** Always uses native camera roll selector — no custom gallery in-app
- **Map interaction:** Tapping map on restaurant profile opens the native Google Maps app (deep link)
- **Back navigation:** Android hardware back button is supported; iOS swipe-back works on all screens
- **Keyboard handling:** Review text area pushes content above keyboard; Post button stays visible
- **Offline state:** If connection drops mid-review, draft is preserved in localStorage until submitted
