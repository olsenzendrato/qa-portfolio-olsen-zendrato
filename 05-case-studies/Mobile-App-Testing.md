# Case Study: Multi-Product Mobile Application Testing

**Role:** Software QA Engineer  
**Company:** PT Indonesia Satu Tujuh (PT INA 17)  
**Products:** Mvicall, Milov, Pantura  
**Platform:** Native Mobile — Android & iOS  
**Duration:** 2024 – 2026  

---

## Background

Alongside the MyTelkomsel Miniapp integration work, I was responsible for the end-to-end QA cycle of three standalone consumer mobile applications. Each product served a distinct user experience and had its own release cadence, creating a concurrent multi-product testing environment.

### Product Overview

**Mvicall** — A video ringtone application. When User A calls User B via WhatsApp, User A's active Mvicall video content plays on User B's incoming call screen — replacing the standard ringtone. This requires User B to have Mvicall installed and all required permissions (overlay, accessibility service, notification) enabled.

**Milov** — A fun Love Match game. Users discover their compatibility with others by scanning fingerprints via the app. Accuracy improves when users input their match partner's name, date of birth, and gender. Core social features include match discovery, friend invitations, in-app chat, and social sharing.

**Pantura** — A Dangdut music and quiz app. Users can listen to Dangdut music (MP3/MP4 collections) and participate in quizzes: Tebak Wajah (guess the artist from a photo), Tebak Lagu (guess the song), and Tebak Lirik (guess the lyrics). Points are awarded for correct answers and can be used in the Pesta Rewards program.

---

## The Challenge

**1. Concurrent multi-product testing**  
At any given time, each product was in a different development phase: one in active feature development, one receiving hotfixes, one in pre-release regression. Managing context-switching across three distinct apps while maintaining coverage required systematic prioritization.

**2. App Store submission deadlines**  
Both Apple App Store and Google Play Store review windows are fixed. A single unresolved Critical or High bug at submission time means a delayed release. Every regression cycle had a hard cutoff tied to these windows.

**3. Permission-dependent core features (Mvicall)**  
Mvicall's core video ringtone feature only works when multiple Android system permissions are active simultaneously (overlay, phone call, notification, accessibility service). Testing required dedicated permission matrix scenarios covering grant/deny combinations — and validating that the feature degrades gracefully without each permission.

**4. Physical multi-device coordination (Mvicall)**  
Testing the video ringtone feature required two physical devices (caller + receiver) operating simultaneously, with controlled phone number assignments. Some scenarios required up to 4 devices across Android and iOS.

**5. Real money transactions (Milov, Pantura)**  
Both apps support in-app purchases using phone credit (pulsa). Testing these flows required actual pulsa deductions on test SIM cards — with verification that coin/subscription balances updated correctly post-transaction.

---

## My Approach

### Test Planning from BRD

Before each release, I reviewed the BRD with the product team to identify:
- Core happy paths that must never fail
- Edge cases unique to each product's feature set
- Regression risk areas from recent development changes

### Tiered Regression Strategy

For each product, I maintained a tiered regression suite to balance speed and coverage:

| Tier | Scope | Execution Time | When Used |
|---|---|---|---|
| **P0 — Smoke** | App launch, login, single core feature | ~30 min | Every build |
| **P1 — Core Regression** | All High-priority flows | ~90 min | Pre-release |
| **P2 — Full Regression** | Complete test suite | ~3 hours | Major release |

This structure reduced smoke test time from ~90 minutes to ~30 minutes per product, enabling faster feedback loops without sacrificing critical coverage.

### Mvicall — Permission Matrix Testing

For Mvicall's permission-dependent core feature, I developed a dedicated permission matrix:

| Scenario | Overlay | Accessibility | Notification | Phone Call | Video Ringtone Works? |
|---|---|---|---|---|---|
| All granted | ✅ | ✅ | ✅ | ✅ | ✅ Yes |
| Overlay denied | ❌ | ✅ | ✅ | ✅ | ❌ No — video cannot display over WhatsApp |
| Accessibility denied | ✅ | ❌ | ✅ | ✅ | ❌ No — cannot intercept call |
| Notification denied | ✅ | ✅ | ❌ | ✅ | ✅ Yes (notification only) |
| Phone call denied | ✅ | ✅ | ✅ | ❌ | ❌ No — cannot verify number |

### Milov — API-Level Bug Discovery

During functional testing of Milov, I tracked API responses via Postman alongside UI testing. This revealed several bugs that were not surfaced by UI observation alone:

- The "Pindai" (scan) button reactivating when a user re-encounters the same profile in Explore — causing unintended coin deductions
- Friend scan result not appearing in the Match tab despite API returning a successful response — indicating a client-side state sync issue
- Chat API returning success but messages not appearing in the chat thread — confirmed by API response inspection via Charles Proxy

### Pantura — Content & Campaign Validation

Pantura required a specific QA practice unique among the three apps: verifying that campaign content (Pesta Reward banners, share link copy, quiz content) was correctly updated in sync with each reward cycle. During the v1.0.61 UAT:

- The Pesta Reward banner was still showing content from the previous cycle (not yet updated to "Pesta Reward Sembilan")
- The share link generated text still referenced the old campaign name
- A non-relevant banner appeared in the home page carousel slider

These were content/configuration bugs rather than functional bugs — caught only because I validated campaign-specific content as part of the test suite, not just UI functionality.

---

## Key Bugs Found Per Product

### Mvicall

| Bug | Severity | Status |
|---|---|---|
| Video upload from gallery fails — cannot edit or upload | High | Reported |
| Permission flow unclear for first-time users on some Android OEMs | Medium | Reported |

### Milov

| Bug | Severity | Status |
|---|---|---|
| In-app chat completely non-functional — messages cannot be sent | High | Reported |
| Horoscope page loads indefinitely on stable WiFi connection | Medium | Reported |
| Match result from Explore scan not appearing in Friends → Match tab (intermittent) | Medium | OK With Note |
| "Pindai" button reactivates on same profile — double coin deduction risk | Medium | OK With Note |
| Video from gallery cannot be selected and uploaded | High | Reported |
| Explore scroll resets video order when scrolling back up | Low | OK With Note |

### Pantura

| Bug | Severity | Status |
|---|---|---|
| Pesta Reward banner not updated to current campaign (Pesta Reward 9) | Medium | Reported |
| Share link text references outdated reward campaign | Medium | Reported |
| Non-relevant banner in home page slider | Low | Reported |
| Wrong number login allowed to proceed to OTP page (no validation error shown) | Medium | OK With Note |

---

## Device Matrix Used

| Device | OS | Products |
|---|---|---|
| Vivo T1 Pro 5G | Android 13 | Mvicall, Milov, Pantura |
| Realme 9 5G / 9 Pro | Android 13 | Mvicall, Milov |
| iPhone X | iOS 16.7 | Mvicall |
| iPhone XI | iOS 16.3 | Mvicall |

---

## Outcome

| Metric | Result |
|---|---|
| Products managed concurrently | 3 (Mvicall, Milov, Pantura) |
| App Store submissions with zero critical blockers | 100% during tenure |
| Smoke test time reduction (per product) | ~67% (90 min → 30 min) |
| Real transactions tested (pulsa deduction) | Verified on physical SIM cards |
| API-level bugs identified via Postman + Charles Proxy | Multiple per release cycle |
| Regression bugs caught before production | Multiple per release cycle |

---

## Lessons Learned

**1. Permission-dependent features need their own dedicated test matrix.**  
For Mvicall, standard functional testing was insufficient. A structured permission grant/deny matrix was essential to fully cover the feature's behavior under all realistic user conditions — especially on Android where permission flows vary by OEM.

**2. Campaign content validation should be a first-class part of the test suite.**  
For Pantura, content bugs (wrong banner, outdated share text) would have reached production if I hadn't explicitly included campaign content checks in the test plan. Content bugs are invisible to automated tests and require human review.

**3. API-level inspection catches bugs that UI testing misses.**  
Several Milov bugs — including the duplicate scan issue and chat sync failure — were discovered through API response monitoring via Postman and Charles Proxy. UI observation alone showed "success" while the underlying data behavior was incorrect.

**4. Multi-device feature testing requires structured coordination upfront.**  
Testing Mvicall's core ringtone feature with 4 devices required assigning specific roles (caller / receiver), phone numbers, and test sequences before execution. Without that structure, coordination errors become a source of false test failures.

---

## Artifacts

- [Mvicall Test Cases](../01-test-cases/mobile-apps/Mvicall-TestCases.md)
- [API Testing — Milov](../03-api-testing/README.md)
- [Bug Report Samples](../02-bug-reports/sample-bug-reports.md)
- [Test Plan Template](../04-test-plans/Test-Plan-Template.md)

---

> *All proprietary product data, phone numbers, and business-specific metrics have been anonymized.*
