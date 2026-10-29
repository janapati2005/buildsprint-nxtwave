# Antigravity Build Log — BuildSprint

## 1. What Was Changed for Public Deployment Readiness

### Unverified Public URL Removal & Explicit Unconfigured State ([index.html](file:///c:/Users/Hari%20Aditya/Downloads/BuildSprint_NxtWave_Submission_Kit/index.html))
- **Removed Unverified Default URL:** Removed the placeholder domain (`nxtwave-buildsprint.org`) from default configuration. The application now starts in an explicit `⚠️ Not Configured (Local Dev)` state when running locally, avoiding any false implication of an active external domain.
- **Static Host Auto-Detection:** Built `isLocalEnvironment()` and `getEffectiveBaseUrl()`. When hosted on any live public static service (GitHub Pages, Vercel, Netlify, Cloudflare Pages), the prototype automatically detects `window.location.origin` as the live production host and generates matching share links.
- **Localhost Link Labeling:** When in local development mode without a configured public URL, WhatsApp share previews explicitly mark links as `(Local Dev Test Link: http://localhost:8080/index.html?ref=CODE)` with guidance instructing organizers to configure their deployed URL before distributing externally.
- **Preserved `?ref=CODE` Formatting:** Added `buildReferralUrl(baseUrl, refCode)` to ensure delimiters (`?` vs `&`) are properly formatted regardless of whether the base URL already has parameters.

### Verified Scannable QR Code Canvas
- **ISO/IEC 18004 Reed-Solomon Encoder:** Mathematically accurate QR generator implemented in pure vanilla JS rendering onto an HTML5 `<canvas id="qrCanvas">`.
- **OpenCV Verification:** Verified physical scannability using OpenCV's `cv2.QRCodeDetector().detectAndDecode()`.
- **Dual State Labeling:**
  - In local development mode without a configured URL, displays `⚠️ Development Preview` and encodes the local link with a clear note.
  - When configured or running on a public host, displays `✓ Production Ready` / `✓ Public Scannable` and encodes the live URL.
  - Added a "💾 Download QR PNG" button for campus connectors.

### Configurable Target Graduation Year Cohort
- **Dynamic Cohort Selection:** Retained the reactive **"🎯 Target Cohort"** selector in the Growth Dashboard (supporting 2026, 2027, 2028, and 2025 batches).
- **Synchronized Recalculation:** Changing the cohort recomputes qualified eligibility ratios, updates the hero scorecard label, refreshes the registration form dropdown, and updates channel qualification metrics without data loss.

### Keyboard Accessibility & Interaction Hardening
- Choice buttons in the project matcher support both mouse click and keyboard selection (`Enter` and `Space` with `role="radio"` and `tabindex="0"`).
- Reset demo data confirmation modal supports dismissal via the `Escape` key.
- All form inputs retain explicit `<label for="...">` associations and `aria-describedby` error bindings.

---

## 2. What Was Tested

### Automated QA Test Suite ([test_prototype.py](file:///c:/Users/Hari%20Aditya/Downloads/BuildSprint_NxtWave_Submission_Kit/test_prototype.py))
- Executed the Python DOM and constraint test suite testing **53 distinct checkpoints**:
  - Viewport meta tags and mobile responsive styling.
  - Registration form elements, required fields, and email regex patterns.
  - Mandatory consent checkbox enforcement.
  - URL parameter detection (`?ref=CODE`) and state preservation.
  - Configurable target graduation year selector and dynamic recomputation listeners.
  - Public URL configuration input, environment status badge, and explicit unconfigured state.
  - Localhost link prevention in production shares and query delimiter joining helper (`buildReferralUrl`).
  - Genuine HTML5 QR Code Canvas existence and algorithm implementation.
  - OpenCV QRCodeDetector compatibility verification (`cv2.QRCodeDetector`).
  - Project matcher questions, scoped MVP, starter stack, 3 execution tasks, and AI caution.
  - ₹2,000 budget allocation (₹900 / ₹700 / ₹400) and 500-student target ladder (30 → 500).
  - Keyboard listeners for modal dismiss (`Escape`) and quiz choice selection (`Enter`).
  - Zero third-party scripts or external network dependencies.
  - **Result: 53 / 53 tests passed (100% pass rate).**

### Computer Vision QR Validation
- Generated QR code matrices for deployed URLs (`https://nxtwave-buildsprint-demo.vercel.app/?ref=AMRITA-CR01`) and local dev links (`http://localhost:8080/index.html?ref=CBIT-CODING04`) were tested with OpenCV's `cv2.QRCodeDetector().detectAndDecode()`.
- Both decoded strings matched target strings with 100% accuracy.

---

## 3. What Remains Mocked

1. **Backend Registration Ingestion:** Submissions are written to browser `localStorage` (`buildsprint_demo_registrations`). No external HTTP POST request is made to NxtWave CRM or marketing automation systems.
2. **External Analytics Dispatch:** Events are recorded to an internal in-memory and `localStorage` stream (`buildsprint_demo_telemetry`). No external network beacon is sent to PostHog, Mixpanel, or Google Tag Manager without explicit production consent.
3. **Official Workshop Details:** Speaker identities, live stream URLs, and official event calendars remain placeholders pending official briefing.

---

## 4. Engineering Trade-offs Made

| Trade-off Decision | Alternatives Considered | Rationale |
| :--- | :--- | :--- |
| **Explicit "Not Configured" Default State** | Hardcoding a plausible demo domain (e.g. `nxtwave-buildsprint.org`) | Hardcoding an unverified public domain damages credibility and risks students copying non-functional links. The explicit "Not configured" state prompts organizers to supply their real deployed URL. |
| **Static Host Auto-Detection** | Always requiring manual URL entry | When deployed to GitHub Pages or Vercel, the app automatically detects `window.location.origin`, providing a zero-configuration experience for organizers. |
| **Self-Contained Pure JS QR Encoder** | External QR CDN script (e.g. `cdnjs.cloudflare.com/ajax/libs/qrcodejs/...`) | Keeps the prototype 100% self-contained and runnable offline without external network dependencies, privacy leaks, or CDN downtime risks. |
| **Single-File Architecture (`index.html`)** | Multi-file structure (`styles.css`, `app.js`) | Avoids CORS issues when opening via `file:///` protocol in modern browsers (where local script imports or fetch requests can be blocked by default browser security policies). |
