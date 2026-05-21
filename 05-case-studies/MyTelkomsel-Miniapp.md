# Case Study: MyTelkomsel Miniapp Integration

**Role:** Lead QA Analyst  
**Company:** PT Indonesia Satu Tujuh (PT INA 17)  
**Duration:** 2024 – 2025  
**Platform:** Mobile Application (Android & iOS) + Web CMS  
**Scale:** National-level telecom digital ecosystem  

---

## Background

MyTelkomsel is Telkom Indonesia's primary mobile application — one of the most widely used telecom apps in Indonesia, serving tens of millions of active users. The platform operates as a super-app, managing data packages, billing, customer support, and a lifestyle ecosystem.

PT INA 17 was engaged to develop and integrate third-party Miniapps — **Ayolari** and **VNSP** — into the MyTelkomsel lifestyle section. These Miniapps allow users to access additional services without leaving the core MyTelkomsel app.

As the Lead QA Analyst, I was responsible for the entire quality gate of this integration — from requirement analysis through to successful deployment.

---

## The Challenge

Integrating a third-party Miniapp into a national-scale super-app presents unique QA challenges that differ significantly from testing a standalone product:

**1. Integration Stability**  
The Miniapp must not disrupt the core MyTelkomsel app in any way. A crash in the Miniapp that cascades to the host app would impact millions of users.

**2. Authentication Security**  
The Miniapp must receive and validate auth tokens from MyTelkomsel correctly. A broken token flow means users are either locked out or, worse, authenticated incorrectly.

**3. Cross-Platform Consistency**  
The integration needed to behave identically across a wide range of Android and iOS devices — fragmented screen sizes, OS versions, and OEM customizations.

**4. UI/UX Compliance**  
Ayolari and VNSP had to match MyTelkomsel's strict design guidelines. Visual inconsistencies in a super-app erode user trust.

**5. Network Resilience**  
The Indonesian mobile network environment includes significant 3G coverage, especially outside major cities. The integration needed to be graceful under poor network conditions.

---

## My Approach

### Phase 1: Requirement Analysis

Before writing a single test case, I reviewed the Business Requirement Document (BRD) in full with the product team. My focus was on identifying:

- **Happy paths** — the primary user journeys that must work flawlessly
- **Edge cases** — what happens at the boundaries (token expiry, network failure, double-taps)
- **Integration contract** — the API specification between MyTelkomsel and the Miniapp

Key questions I raised during this phase:
- What happens when the auth token expires while the user is inside the Miniapp?
- What is the expected behavior if the Miniapp server is down?
- Does the Miniapp back-navigation restore the user's previous state in MyTelkomsel?

### Phase 2: Test Case Design

I authored **150+ test cases** covering:

| Category | Test Count | Focus Areas |
|---|---|---|
| Entry Point & Launch | 18 | Banner display, loading states, error states |
| Authentication & Token | 22 | Valid token, expired token, session timeout |
| Core Miniapp Flows | 45 | User journeys, content fetch, interactions |
| UI/UX Compliance | 30 | Figma comparison, responsive layouts, dark mode |
| API Validation | 20 | Status codes, payloads, error responses |
| Device Matrix | 18 | Android (6 devices), iOS (6 devices), cross-device |
| Network Resilience | 12 | Slow 3G, no connection, intermittent signal |

**Test design techniques applied:**
- **Boundary Value Analysis** — token expiry timing, character limits on inputs
- **Equivalence Partitioning** — valid/invalid network states, valid/invalid tokens
- **Use Case Testing** — end-to-end user journeys from banner tap to task completion
- **Exploratory Testing** — unscripted sessions targeting unexpected interaction patterns

### Phase 3: API Validation

I used **Postman** to validate every API endpoint in the integration contract:

- `POST /miniapp/launch` — token exchange and session initialization
- `GET /miniapp/content` — content fetching with pagination
- `POST /miniapp/track` — event tracking and analytics
- Error scenarios: 401, 403, 404, 500 responses

I also used **Charles Proxy** to monitor actual network traffic from real devices, confirming that:
- Auth tokens were being passed in headers correctly (not in URL params)
- Sensitive user data was not exposed in unencrypted traffic
- API response times were within acceptable thresholds

### Phase 4: Real Device Testing

All execution was performed on **physical devices** — no emulators for final validation. Devices tested:

| Device | OS | Notes |
|---|---|---|
| Samsung Galaxy A54 | Android 13 | Most common mid-range segment |
| Samsung Galaxy A32 | Android 12 | Older OS — identified image rendering bug |
| Xiaomi Redmi Note 12 | Android 13 | Popular brand in Indonesia |
| iPhone 13 | iOS 16.x | Primary iOS target |
| iPhone 14 Pro | iOS 17.x | High-end iOS |
| iPhone SE (3rd Gen) | iOS 16.x | Small screen validation |

Using **Android Studio Logcat**, I captured crash logs and runtime errors that were not visible in the UI — enabling developers to pinpoint root causes significantly faster than error messages alone.

---

## Key Bugs Found

### Critical (2 bugs)

**BUG-MA-001 — App crashed on Miniapp launch when MyTelkomsel had no cached user data**  
Scenario: First launch after fresh MyTelkomsel install → Miniapp crashed immediately because the token generation assumed cached user data existed.  
Impact: 100% failure rate for new users.

**BUG-MA-002 — Auth token sent in plain URL parameter instead of Authorization header**  
Scenario: API traffic inspection via Charles Proxy revealed the token in the URL query string.  
Impact: Security vulnerability — tokens visible in server logs and browser history.

### High (5 bugs)

- Miniapp did not handle 503 server error gracefully (showed raw JSON error to user)
- Miniapp back button did not restore MyTelkomsel scroll position on Android
- Banner thumbnail failed to load on Samsung Android 12 devices (WebP format issue)
- Session timeout did not trigger re-auth flow — app went into silent broken state
- Double-tap on CTA triggered duplicate API calls leading to duplicate transactions

### Medium (8 bugs)

- Layout overflow on small screens (iPhone SE)
- Dark mode rendering issues on text elements
- Incorrect empty state message when content API returned 404
- Loading spinner not shown when content fetch takes >2 seconds

---

## Outcome

| Metric | Result |
|---|---|
| Total test cases executed | 150+ |
| Critical bugs found & resolved | 2 |
| High bugs found & resolved | 5 |
| Blocker bugs at UAT stage | 0 |
| Platforms covered | Android + iOS + Web CMS |
| Deployment result | Successful — zero post-deployment critical issues |

The Miniapp launched into the MyTelkomsel ecosystem on schedule, with **zero critical or high severity bugs** reaching the production environment.

---

## Lessons Learned

**1. API testing should start before UI testing.** Validating the integration contract early exposed the token security issue before a single UI test was run.

**2. Real devices reveal what emulators miss.** The Samsung Android 12 WebP rendering bug only appeared on physical devices — the emulator passed.

**3. Exploratory testing at edge network conditions is non-negotiable for Indonesian market.** 3G simulation via Charles Proxy consistently uncovered behavior that WiFi testing missed.

**4. Good bug reports accelerate developer velocity.** Providing Logcat logs alongside bug reports reduced average developer investigation time and improved fix-rate measurably.

---

## Artifacts

- [Test Cases — MyTelkomsel Miniapp](../01-test-cases/miniapp/MyTelkomsel-Miniapp-TestCases.md)
- [API Test Cases](../03-api-testing/README.md)
- [Bug Report Samples](../02-bug-reports/sample-bug-reports.md)

---

> *All proprietary business data, actual API endpoints, and production metrics have been anonymized in accordance with confidentiality obligations.*
