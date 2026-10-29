# BuildSprint — NxtWave Growth Challenge Prototype

A polished, mobile-first, zero-dependency prototype engineered for simulated growth campaigns supporting NxtWave's free **“Build Your First AI Project in 60 Minutes”** workshop.

The prototype models the growth hypothesis: **500 final-year engineering student registrations in 7 days with a ₹2,000 community enablement budget and zero paid media.**

---

## 🌐 Public Deployment & Hosting Guide

Because BuildSprint is built as a zero-dependency, single-file application ([index.html](file:///c:/Users/Hari%20Aditya/Downloads/BuildSprint_NxtWave_Submission_Kit/index.html)), it can be hosted instantly on any static web platform.

### Option 1: GitHub Pages (Recommended Free Static Hosting)
1. Push this repository to GitHub.
2. In your GitHub repository, navigate to **Settings** → **Pages**.
3. Under **Build and deployment**, select `Deploy from a branch` and choose `main` / `root`.
4. Once deployed, open your live URL (e.g. `https://<username>.github.io/<repo-name>/index.html`).
5. **Auto-Detection in Action:** When opened on GitHub Pages, BuildSprint automatically detects the live public origin (`window.location.origin`), displays `🌐 Public Host Detected`, and generates live WhatsApp invites and scannable QR codes matching your deployed URL!

### Option 2: Vercel (Instant Zero-Config Deploy)
1. Install Vercel CLI (`npm i -g vercel`) or import the repo via [vercel.com](https://vercel.com).
2. Run `vercel deploy --prod` from this folder.
3. The generated production URL (e.g. `https://buildsprint-nxtwave.vercel.app`) is immediately auto-detected by the app.

### Option 3: Netlify / Cloudflare Pages / AWS S3
- Drag and drop this folder into the [Netlify Drop](https://app.netlify.com/drop) console.
- Alternatively, upload `index.html` to any static web hosting bucket.

---

## 💻 Local Development & Testing

When running locally, BuildSprint enforces strict safety guardrails:

```bash
# Start local static server
python -m http.server 8080
```

- **Base Prototype:** `http://localhost:8080/index.html`
- **With Campus Connector Attribution:** `http://localhost:8080/index.html?ref=AMRITA-CR01`
- **With Club Lead Attribution:** `http://localhost:8080/index.html?ref=CBIT-CODING04`

### Localhost Safeguards:
1. **Explicit "Not Configured" Default:** The prototype never invents or hardcodes unverified public URLs. Until an organizer enters a deployed URL or hosts the app publicly, the public URL status remains explicitly marked as `⚠️ Not Configured (Local Dev)`.
2. **Localhost Link Labeling:** All WhatsApp previews and share messages clearly label local links as `[Development / Localhost Test Link]` to prevent testers from sending non-resolving localhost URLs to external student groups.
3. **Configured URL Fallback:** You can enter your intended deployed production URL in the **"Public Deployed Website URL"** input in the Share Kit. The app will immediately update share text and QR codes to encode that URL.

---

## 🌟 Architecture & Key Features

### 1. Genuinely Scannable QR Code Canvas (Zero Dependencies)
- **ISO/IEC 18004 Reed-Solomon Encoder:** Real mathematical QR generator implemented in pure vanilla JS rendering to `<canvas id="qrCanvas">`.
- **Physical Camera Scannable:** Verified against OpenCV's `cv2.QRCodeDetector` for reliable scanning across iOS and Android devices.
- **Dynamic Tagging:** Encodes the live deployed URL (or configured URL) preserving `?ref=CODE`.
- **Downloadable Asset:** Campus connectors can click "💾 Download QR PNG" to obtain high-resolution QR codes for physical campus sticker sheets.

### 2. Configurable Target Graduation Year Cohort
- **Dynamic Eligibility Logic:** No hardcoded cohort lock-in. A reactive **"🎯 Target Cohort"** selector in the Growth Dashboard allows toggling between `2026 Batch (Current Final-Year)`, `2027 Batch (Pre-Final Year)`, `2028`, and `2025`.
- **Synchronized Recalculation:** Changing the target cohort instantly updates hero metrics, registration options, qualified final-year ratios, and channel breakdown columns without data loss.

### 3. Attribution Engine & Referral Loop
- **URL Parameter Capture:** Captures `?ref=CODE` or `?referral=CODE` on initial load.
- **Sticky Feedback:** Displays active attribution badge in the navigation bar.
- **Form Prefill:** Carries attribution code into the registration form.
- **Peer Multiplier:** Post-registration confirmation card generates an attributable peer share link (`?ref=STUDENT-YY`) to incentivize forwarding to classmates.

### 4. Interactive 3-Question Project Matcher
- **Targeted Quiz:** 3 questions identifying problem domain, coding comfort level, and placement goals.
- **Scoped Result:** 60-minute MVP scope, starter stack, and first 3 execution tasks.
- **AI Validation Caution:** Prominent warning educating students to enforce schema validation and test for hallucinations in placement interviews.
- **Auto-Fill CTA:** Clicking "Build this at the workshop ↗" pre-selects the corresponding track in the registration form.

### 5. Growth Dashboard & Analytics
- **Live Metrics:** Real-time counters for Total Registrations (with progress bar towards 500), Qualified Final-Year count/ratio, Active Referral Channels, and Cost Per Registration (`₹2,000 / Total`).
- **Channel Attribution Table:** Breakdown by code, source description, final-year ratio, and share percentage.
- **7-Day Cumulative Ladder:** Visual tracker comparing actual registrations against the planning hypothesis (Day 1: 30 → Day 7: 500).
- **Reviewer Tools:**
  - `⚡ Load Sample Cohort`: Hydrates 35 realistic records across 5 colleges to test analytics.
  - `📥 Export JSON`: Download all simulated browser registrations.
  - `🗑️ Reset Demo Data`: Safe deletion with a confirmation modal (with Escape key support).

---

## 🔒 Limitations & Demo Data Handling

1. **Browser-Local Storage:** All registrations are saved strictly to the browser's `localStorage` (`buildsprint_demo_registrations`). No external API call is made.
2. **Zero External Data Transmission:** No personal student data is transmitted across the internet.
3. **Placeholder Event Schedule:** Workshop dates, speaker credentials, and live stream links remain placeholders pending official NxtWave confirmation.

---

## 🧪 Pre-Submission QA Verification

Run the automated test suite locally:
```bash
python test_prototype.py
```

### Verification Checklist (53 Checkpoints):
- [x] **Unverified URL Removal:** No invented public domains in default state; explicit unconfigured state.
- [x] **Scannable QR Canvas:** Verified ISO/IEC 18004 Reed-Solomon QR encoder compatible with OpenCV.
- [x] **Configurable Cohort:** Dynamic graduation year selection with real-time recalculation.
- [x] **Localhost Protection:** Development links explicitly labeled; public shares preserve `?ref=CODE`.
- [x] **Static Host Compatibility:** Zero dependencies, relative asset paths, client-side routing.
- [x] **Form Validation:** Mandatory field checks, email format validation, graduation year required.
- [x] **Mandatory Consent:** Explicit demo-mode disclaimer checkbox required before submit.
- [x] **Attribution Preservation:** Preserves `?ref=CODE` across matcher, form, and confirmation state.
- [x] **Keyboard Accessibility:** Choice buttons respond to Enter/Space; modal closes on Escape key.
- [x] **Mobile Responsiveness:** Tested on 360px+ viewports without horizontal scrolling.
