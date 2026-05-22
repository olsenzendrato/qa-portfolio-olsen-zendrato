# Sample Bug Reports

Real-scenario defect reports from QA work across multiple projects at PT Indonesia Satu Tujuh. All reports follow professional bug documentation standards. Business-sensitive data has been anonymized.

---

## BUG-2024-001 — Mvicall

**Title:** Video upload from gallery fails — selected video cannot be edited or uploaded

| Field | Detail |
|---|---|
| **Severity** | 🟠 High |
| **Priority** | High |
| **Type** | Functional |
| **Status** | Reported |
| **Platform** | Android |
| **Device** | Vivo T1 Pro 5G — Android 13 |
| **App Version** | Mvicall v2.0.86 |
| **Test Environment** | Production |

**Summary:**  
When a user attempts to upload a video profile by selecting a file from their gallery, the video cannot be edited or uploaded. The camera upload flow works correctly. This bug blocks users from using existing videos as their Mvicall ringtone content.

**Steps to Reproduce:**
1. Log in to Mvicall.
2. Navigate to Profile → Tambah Video.
3. Select "From Gallery."
4. Choose any video from the device gallery.
5. Attempt to edit and upload the selected video.

**Reproducibility Rate:** Always (5/5)

**Actual Result:**  
The selected video cannot be edited. Upload option unavailable or fails silently.

**Expected Result:**  
User should be able to select a video from gallery, optionally trim/edit it, and upload it as their Mvicall video profile content.

**Evidence:** Screenshot + screen recording

---

## BUG-2024-002 — Milov

**Title:** Chat feature non-functional — messages cannot be sent between users

| Field | Detail |
|---|---|
| **Severity** | 🟠 High |
| **Priority** | High |
| **Type** | Functional |
| **Status** | Reported |
| **Platform** | Android |
| **Device** | Vivo T1 Pro 5G — Android 13 |
| **App Version** | Milov v1.1.21 |
| **Test Environment** | Staging |

**Summary:**  
The in-app chat feature between Milov users is completely non-functional. Users can see the chat list (which appears empty) but cannot send messages to friends. This impacts a core social feature of the Love Match game experience.

**Steps to Reproduce:**
1. Log in to Milov.
2. Navigate to Friends → select a friend.
3. Open the chat screen.
4. Type a message and tap Send.

**Reproducibility Rate:** Always (5/5)

**Actual Result:**  
Message cannot be sent. Chat remains empty. No error message shown to user.

**Expected Result:**  
Message sent successfully and visible in both sender's and recipient's chat thread.

**Evidence:** Screen recording

---

## BUG-2024-003 — Milov

**Title:** Horoscope page loads indefinitely — does not resolve even with stable WiFi connection

| Field | Detail |
|---|---|
| **Severity** | 🟡 Medium |
| **Priority** | Medium |
| **Type** | Performance |
| **Status** | Reported |
| **Platform** | Android |
| **Device** | Realme 9 Pro — Android 13 |
| **App Version** | Milov v1.1.21 |
| **Network** | WiFi (stable) |
| **Test Environment** | Staging |

**Summary:**  
The Horoscope page inside the Milov app shows a loading state indefinitely and never resolves, even after waiting for an extended period (tested over 24 hours) with a stable internet connection. No error state or retry option is presented.

**Steps to Reproduce:**
1. Log in to Milov.
2. Navigate to Home.
3. Tap "Horoscope."
4. Observe the page loading state.

**Reproducibility Rate:** Always (5/5)

**Actual Result:**  
Loading spinner appears and never resolves. Page remains blank indefinitely.

**Expected Result:**  
Horoscope content loads within 5 seconds on a stable connection. If loading fails, an error state with a "Retry" button is shown.

---

## BUG-2024-004 — Pantura

**Title:** Pesta Reward banner and share link not updated to current reward cycle (Pesta Reward 9)

| Field | Detail |
|---|---|
| **Severity** | 🟡 Medium |
| **Priority** | High |
| **Type** | Content / Functional |
| **Status** | Reported |
| **Platform** | Android |
| **Device** | Vivo T1 Pro 5G — Android 13 |
| **App Version** | Pantura v1.0.61 |
| **Test Environment** | Production |

**Summary:**  
The Pesta Reward feature in Pantura is still showing content from a previous reward cycle. Both the banner image and the shared link wording have not been updated to reflect "Pesta Reward Sembilan" (Reward Cycle 9). Additionally, a non-relevant banner appears in the home page slider.

**Steps to Reproduce:**

*Pop-up flow:*
1. Log in to Pantura.
2. Tap Share on the Pesta Reward popup.
3. Observe generated share link content.

*Banner flow:*
1. Log in to Pantura.
2. Scroll to home page banner slider.
3. Observe the last banner in the carousel.

**Reproducibility Rate:** Always

**Actual Result:**  
- Share link references previous reward cycle name.
- Banner image has not been updated to Pesta Reward 9.
- Last banner in home slider is irrelevant to current reward campaign.

**Expected Result:**  
All Pesta Reward content (banner images, share link wording, popup) reflects the active "Pesta Reward Sembilan" campaign.

---

## BUG-2024-005 — CMS Digipac (DPA)

**Title:** Form data cleared when user navigates back from Bank Detail or Contact Detail page

| Field | Detail |
|---|---|
| **Severity** | 🟠 High |
| **Priority** | High |
| **Type** | Functional — Data Integrity |
| **Status** | OK With Note (Workaround applied) |
| **Platform** | Web (Chrome) |
| **Environment** | Staging |
| **CMS Version** | DPA Staging |

**Summary:**  
When a partner user is filling in the Bank Account Detail or Contact Detail registration forms and presses the browser back button or the in-app back button, they are returned to the previous step but all data entered in the current step is lost. This forces users to re-enter information, increasing registration friction significantly.

**Steps to Reproduce:**
1. Open DPA registration flow.
2. Complete Company Detail step.
3. On Bank Account Detail page, fill in all fields.
4. Press browser back button or in-app back button.
5. Navigate forward again to Bank Account Detail.

**Reproducibility Rate:** Always

**Actual Result:**  
All previously entered Bank Account Detail data is cleared. User must re-enter all fields.

**Expected Result:**  
Data should be preserved when navigating back and forward within the multi-step registration flow.

**Resolution Note:**  
As a workaround to meet the release deadline, the back button was temporarily disabled per product team direction. A permanent fix (preserving form state on navigation) is scheduled for the next development cycle.

---

## BUG-2025-006 — Miniapp Ayolari (iOS Navigation)

**Title:** Privacy Policy link exits Ayolari miniapp on iOS — no return path available

| Field | Detail |
|---|---|
| **Severity** | 🟡 Medium |
| **Priority** | Medium |
| **Type** | UI/UX — Navigation |
| **Status** | OK With Note (Platform behavior difference documented) |
| **Platform** | iOS |
| **Device** | iPhone 11 Pro Max — iOS 16 |
| **App Version** | MyTelkomsel 9.2.0-1006878299 (iOS) |
| **Test Environment** | Production |

**Summary:**  
On iOS, tapping the Privacy Policy link on the Ayolari User Consent Page opens the page via deeplink, which exits the user from the Ayolari miniapp entirely and redirects them to MyTelkomsel. Unlike Android (which has a native back button to return to Ayolari), iOS users cannot return to the Consent Page because there is no back navigation button. The user must re-open Ayolari to continue the onboarding flow.

**Steps to Reproduce:**
1. Open Ayolari miniapp on iPhone for the first time.
2. On the User Consent Page, tap "Kebijakan Privasi" link.
3. Attempt to return to the Consent Page.

**Reproducibility Rate:** Always on iOS

**Actual Result:**  
Privacy Policy opens via deeplink. User is exited from Ayolari. No back button available on iOS to return to Consent Page. User must reopen Ayolari.

**Expected Result:**  
User can read the Privacy Policy and return to the Consent Page without losing their onboarding progress.

**Root Cause:** Privacy Policy implemented as a deeplink (browser-based), which behaves differently on iOS vs Android due to OS-level navigation differences. Android's native back button can return to the app; iOS has no equivalent.

**Recommended Fix:** Implement Privacy Policy as an in-app WebView instead of a deeplink, so navigation remains within the miniapp on both platforms.

---

## BUG-2024-007 — API Milov

**Title:** Scan Match result does not appear in Friend tab after successful scan from Explore page

| Field | Detail |
|---|---|
| **Severity** | 🟡 Medium |
| **Priority** | Medium |
| **Type** | Functional — API / Data Sync |
| **Status** | OK With Note |
| **Platform** | Android |
| **Device** | Realme 9 Pro — Android 13 |
| **App Version** | Milov v1.1.21 |
| **Test Environment** | Staging |

**Summary:**  
When User A scans a match with User B from the Explore page (costing 1 coin), the scan result popup appears correctly on Device 1. However, User B's account does not appear in the "Match" tab of the Friends page on Device 1. When retested with a different Milov account, the match result appeared correctly — suggesting an intermittent data synchronization issue.

**Steps to Reproduce:**
1. Log in to Milov on Device 1 (User A).
2. Navigate to Explore page.
3. Find User B's video profile.
4. Tap "Pindai" (Scan) to scan match.
5. Confirm scan result popup appears.
6. Navigate to Friends → Match tab.
7. Observe whether User B appears in the match list.

**Reproducibility Rate:** Intermittent — observed on first test account; did not reproduce on second account

**Actual Result:**  
Match result popup shown (1 coin deducted). User B does NOT appear in Friends → Match tab.

**Expected Result:**  
User B should appear in the Match tab immediately after a successful scan.

**Additional Note:**  
The "Pindai" button reactivates when the user encounters the same video again in Explore, causing unintended additional coin deductions if pressed again. Recommended to disable or hide the Pindai button after a match has already been scanned.

---

> All bug reports are based on real defects found during professional QA execution at PT Indonesia Satu Tujuh. Business-sensitive data, internal URLs, and credentials have been removed or anonymized.
