# Sample Bug Reports

Five real-scenario defect reports across different platforms and severity levels, demonstrating professional bug documentation standards.

---

## BUG-2026-001

**Title:** App crashes when user double-taps "Confirm Payment" button during high-latency network connection

| Field | Value |
|---|---|
| **Severity** | 🔴 Critical |
| **Priority** | High |
| **Type** | Functional |
| **Status** | Fixed ✅ |
| **Platform** | iOS |
| **Device** | iPhone 14 — iOS 17.2 |
| **Network** | Throttled Slow 3G (Charles Proxy) |
| **App Version** | v2.1.0 |
| **Test Environment** | Staging |

**Summary:**  
When a user taps the "Confirm Payment" button and immediately taps it again before the API response returns, the app freezes for approximately 3 seconds and then crashes to the home screen. This causes a critical UX failure during checkout and may result in duplicate payment attempts on the server side.

**Steps to Reproduce:**
1. Log in with a valid user account.
2. Add any item to cart and proceed to checkout.
3. On the payment screen, tap "Confirm Payment."
4. Before the loading state appears (within ~300ms), rapidly tap "Confirm Payment" a second time.
5. Observe app behavior.

**Reproducibility Rate:** 8/10 attempts

**Actual Result:**  
The app freezes for approximately 3 seconds, then crashes abruptly to the device home screen. No error message is shown. The payment status is unknown to the user.

**Expected Result:**  
After the first tap, the "Confirm Payment" button should immediately become disabled and display a loading spinner. The button should remain inactive until the API returns a response (success or error). Double-tap should have no additional effect.

**Evidence:** Screenshot + Logcat log attached (see `/assets/BUG-2026-001/`)

**Developer Note:** Root cause — missing button debounce and no state management preventing duplicate API calls.

---

## BUG-2026-002

**Title:** Miniapp banner thumbnail not loading on Samsung Galaxy devices running Android 12

| Field | Value |
|---|---|
| **Severity** | 🟠 High |
| **Priority** | High |
| **Type** | UI/UX — Rendering |
| **Status** | Fixed ✅ |
| **Platform** | Android |
| **Device** | Samsung Galaxy A32 — Android 12 |
| **Network** | WiFi (stable) |
| **App Version** | v3.4.2 |
| **Test Environment** | Staging |

**Summary:**  
The Miniapp banner in the MyTelkomsel lifestyle section fails to render its thumbnail image on Samsung Galaxy devices running Android 12. The banner section shows a broken image placeholder, while the title and CTA button load correctly. This issue does not occur on Android 13+ or iOS devices.

**Steps to Reproduce:**
1. Log in to MyTelkomsel on a Samsung Galaxy A32 (Android 12).
2. Scroll to the Lifestyle/Miniapp section on the home screen.
3. Observe the Ayolari or VNSP banner card.

**Reproducibility Rate:** Always (10/10) on Android 12 devices tested

**Actual Result:**  
Banner image shows a broken placeholder icon. No thumbnail is visible.

**Expected Result:**  
Banner thumbnail image loads correctly within 3 seconds, matching the approved design.

**Evidence:** Screenshot comparing Samsung Galaxy A32 (broken) vs Samsung Galaxy A54 Android 13 (correct)

**Root Cause (Post-Fix):** WebP image format not fully supported on Android 12 WebView version shipped with Samsung One UI 4. Fix: added JPEG fallback format.

---

## BUG-2026-003

**Title:** CMS rich text editor loses formatting when content is saved and reopened

| Field | Value |
|---|---|
| **Severity** | 🟠 High |
| **Priority** | Medium |
| **Type** | Functional — Data Integrity |
| **Status** | Open 🔴 |
| **Platform** | Web (Chrome 120) |
| **Device** | MacBook Pro — macOS Sonoma |
| **Network** | WiFi |
| **App Version** | CMS Digipac v1.8.3 |
| **Test Environment** | Staging |

**Summary:**  
When an editor publishes an article containing bold text and bullet lists using the CMS rich text editor, the formatting is lost when the article is reopened for editing. The content appears as plain text. The published front-end article is unaffected — only the CMS editor view loses formatting on re-open.

**Steps to Reproduce:**
1. Log in to CMS Digipac as Editor.
2. Create a new article.
3. Add body content with bold text, a bullet list, and a hyperlink.
4. Click "Publish."
5. Navigate back to the articles list.
6. Reopen the published article by clicking "Edit."
7. Observe the body content in the rich text editor.

**Reproducibility Rate:** Always (5/5 attempts)

**Actual Result:**  
All formatting (bold, bullets, links) is stripped. Body content appears as plain text in the editor.

**Expected Result:**  
Article body opens in the editor with all formatting preserved, matching the original published version.

**Evidence:** Before/after screenshots of editor content

---

## BUG-2026-004

**Title:** Search results display duplicate entries when user scrolls to next page rapidly

| Field | Value |
|---|---|
| **Severity** | 🟡 Medium |
| **Priority** | Medium |
| **Type** | Functional — Pagination |
| **Status** | In Progress 🟡 |
| **Platform** | Android & iOS |
| **Device** | iPhone 13 (iOS 16.6) / Samsung Galaxy S23 (Android 14) |
| **Network** | 4G LTE |
| **App Version** | Milov v1.2.0 |
| **Test Environment** | Staging |

**Summary:**  
When a user performs a search and quickly scrolls to the bottom of results to trigger pagination (infinite scroll), some content items from page 1 appear duplicated at the top of page 2 results. This causes a confusing UX where users see the same item twice in their search results.

**Steps to Reproduce:**
1. Open the Milov app and navigate to Search.
2. Search for a keyword that returns 20+ results (e.g., "video").
3. Wait for the first 10 results to load.
4. Rapidly scroll to the very bottom of the list.
5. Observe the next batch of loaded results.

**Reproducibility Rate:** 6/10 attempts (intermittent, more frequent on slower connections)

**Actual Result:**  
Items 8–10 from page 1 appear again as items 1–3 of page 2.

**Expected Result:**  
Pagination loads unique items in sequence. No item appears more than once in search results.

---

## BUG-2026-005

**Title:** "Forgot Password" email link expires immediately when opened on iOS Mail app

| Field | Value |
|---|---|
| **Severity** | 🟠 High |
| **Priority** | High |
| **Type** | Functional — Authentication |
| **Status** | Verified ✅ |
| **Platform** | iOS |
| **Device** | iPhone 14 Pro — iOS 17.1 |
| **Network** | WiFi |
| **App Version** | v2.3.0 |
| **Test Environment** | Production |

**Summary:**  
When a user requests a password reset and opens the reset link from the native iOS Mail app, the link immediately shows "This link has expired" — even when opened within seconds of receiving the email. The same link works correctly when opened from Gmail app or a desktop browser. This effectively blocks iOS Mail users from resetting their password.

**Steps to Reproduce:**
1. On an iPhone, open the app and tap "Forgot Password."
2. Enter a registered email address.
3. Open Apple Mail (native iOS Mail app) and locate the reset email.
4. Tap the password reset link inside the email.
5. Observe the result in the browser/app.

**Reproducibility Rate:** Always (10/10) when using iOS native Mail app

**Actual Result:**  
"This link has expired or is invalid. Please request a new password reset." — shown immediately.

**Expected Result:**  
Password reset page opens and allows user to set a new password. Link should be valid for at least 30 minutes.

**Evidence:** Screen recording showing link tapped in iOS Mail app → immediately shows expired page

**Root Cause (Post-Fix):** iOS Mail app pre-fetches links in emails for link preview generation, which consumed the single-use token before the user clicked it. Fix: changed to multi-use token with time-based expiry (30 minutes) instead of single-use.

---

> **Note:** Bug scenarios are based on real defect types encountered during professional QA work. Business-specific details have been anonymized.
