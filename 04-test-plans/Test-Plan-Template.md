# 04 — Test Plans & STLC Documentation

Professional test planning documentation reflecting the Software Testing Life Cycle (STLC) process followed across multiple product releases at PT Indonesia Satu Tujuh.

---

# Test Plan Template

*(Based on test plans executed across Mvicall, Milov, Pantura, CMS Digipac, Ayolari Miniapp, and V-NSP)*

---

## 1. Project Overview

| Field | Detail |
|---|---|
| **Project Name** | [Project / Feature Name] |
| **Application** | [App Name & Version] |
| **Platform** | Web / Android / iOS / Miniapp (MyTelkomsel) |
| **Test Plan Version** | v1.0 |
| **Prepared By** | Olsen Yeremia Zendrato |
| **Date** | YYYY-MM-DD |
| **Release / Sprint** | [Release Name / Sprint Number] |
| **Test Environment** | Staging / Production / Internal DummyApp |

---

## 2. Scope of Testing

### In Scope
- [Feature 1 — brief description, e.g., User registration and login flow]
- [Feature 2 — e.g., Core feature: video ringtone display during WhatsApp call]
- [Feature 3 — e.g., Permission grant/deny matrix for all required permissions]
- [Feature 4 — e.g., API validation: auth token, payload structure, error responses]
- [Feature 5 — e.g., Cross-device: all devices in device matrix]
- [Feature 6 — e.g., Cross-platform: Android and iOS behavioral parity]

### Out of Scope
- [Excluded area — reason, e.g., Performance load testing (not in this sprint)]
- [Excluded platform — e.g., iOS for VNSP (Android-only feature)]
- [Backend unit tests (developer responsibility)]

---

## 3. Test Objectives

1. Verify all in-scope features meet requirements specified in BRD / Figma design.
2. Confirm no regression in stable existing features after new development changes.
3. Validate API responses are correct, properly structured, and handle errors gracefully.
4. Verify UI/UX matches approved Figma designs across all target devices and screen sizes.
5. Ensure platform-specific behaviors (Android vs iOS) are correctly implemented and documented.
6. Confirm zero Critical or High severity open bugs before UAT handoff or App Store submission.

---

## 4. Test Strategy

| Testing Type | Approach | Tools |
|---|---|---|
| Functional Testing | Black-box manual execution against BRD/PRD | ClickUp, Google Spreadsheet |
| Negative Testing | Dedicated negative case suite per feature module | Real devices |
| API Testing | Request/response validation per API spec | Postman, Charles Proxy |
| UI/UX Testing | Visual comparison against Figma; pixel-level on key elements | Real devices, screenshots |
| Regression Testing | Tiered suite (P0/P1/P2) re-executed after each build | Manual |
| Permission Matrix Testing | All grant/deny combinations for permission-dependent features | Real devices |
| Cross-Device Testing | Core flows on full device matrix | Physical Android & iOS devices |
| Cross-Platform Testing | Android vs iOS behavioral comparison per feature | Comparative execution |
| Accuracy Testing | Physical real-world testing for sensor-dependent features (Ayolari) | Physical devices + reference device |

---

## 5. Entry & Exit Criteria

### Entry Criteria (Testing can begin when:)
- [ ] BRD, PRD, or Figma design has been reviewed and clarified
- [ ] Development build deployed to staging / production environment
- [ ] API documentation available and endpoints accessible
- [ ] Test devices available and configured (correct build installed)
- [ ] Test cases written and reviewed

### Exit Criteria (Testing complete when:)
- [ ] All High and Critical priority test cases executed
- [ ] Zero open Critical or High severity bugs
- [ ] Regression suite passes ≥ 95% pass rate
- [ ] All UI/UX feedback implemented and re-verified
- [ ] Platform-specific behaviors (Android/iOS) documented
- [ ] Test summary report submitted

---

## 6. Test Environment

| Field | Detail |
|---|---|
| **Staging / Build** | [Staging URL or APK build version] |
| **Test Accounts** | [Roles / account types needed, e.g., new user, existing user, admin] |
| **API Environment** | Staging — Base URL: `[anonymized]` |
| **Network** | WiFi + Throttled simulation via Charles Proxy |
| **Monitoring Tools** | Android Studio Logcat (crash logs), Charles Proxy (network traffic) |

### Device Matrix

*(Actual devices used across projects at PT INA 17)*

| Device | OS | Platform | Used In |
|---|---|---|---|
| Samsung Galaxy A23 | Android 14 | Android | Ayolari v9.2, V-NSP |
| Vivo T1 Pro 5G | Android 13 | Android | Mvicall, Milov, Pantura |
| Realme 9 5G | Android 13 | Android | Mvicall |
| Realme 9 Pro | Android 13 | Android | Milov, Ayolari accuracy |
| POCO M3 | Android 13 | Android | V-NSP |
| OPPO Reno8 T | Android 15 | Android | V-NSP, Ayolari accuracy |
| ITEL RS4 | Android 14 | Android | V-NSP |
| Techno Spark 30C | Android 14 | Android | V-NSP, Ayolari accuracy |
| Infinix Hot 50i | Android 14 | Android | V-NSP |
| Samsung Galaxy S23/S24 | Android 14 | Android | Ayolari accuracy |
| iPhone X | iOS 16.7 | iOS | Mvicall |
| iPhone XI | iOS 16.3 | iOS | Mvicall |
| iPhone 11 Pro Max | iOS 16 | iOS | Ayolari v9.2 |
| iPhone 11 | iOS 16 | iOS | Ayolari accuracy |

---

## 7. Test Schedule

| Phase | Activity | Duration |
|---|---|---|
| Day 1 | Requirement review, clarification with PM/Dev | 0.5 day |
| Day 1–2 | Test case authoring (positive + negative cases) | 1.5 days |
| Day 2 | Test case review; environment & device setup | 0.5 day |
| Day 3–5 | Test execution (functional, API, UI/UX, permission matrix) | 2–3 days |
| Day 5–6 | Bug reporting, developer fix cycle, re-test | 1–2 days |
| Day 6–7 | Regression testing; UAT preparation | 1 day |
| Day 7 | Test summary report; sign-off | 0.5 day |

---

## 8. Defect Management

- All bugs logged in **ClickUp** with required fields: Title, Steps, Severity, Priority, Environment, Evidence
- Bug status workflow: `Open → In Progress → Fixed → Re-test → Closed` / `Rejected` / `OK With Note`
- **"OK With Note"** status used when a bug is accepted with a documented workaround due to deadline constraints
- Daily triage with development team during active testing phase
- Critical bugs require same-day developer acknowledgement
- Platform-specific behavioral differences (Android vs iOS) documented as notes, not bugs, unless behavior deviates from agreed spec

---

## 9. Risks & Mitigation

*(Based on risks encountered across actual projects)*

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Late delivery of staging build | Medium | High | Begin API test case preparation early; buffer 1 day in schedule |
| OEM-specific Android behavior (battery kill, permissions) | High for mobile | High | Always test on minimum 3 OEM brands; include Chinese OEM devices |
| iOS vs Android navigation differences in Miniapp | Medium | Medium | Explicitly test platform-specific flows; document differences |
| No formal requirement documentation | Medium | High | Run requirement gathering session with PM; screenshot chat discussions as spec |
| Real-money transaction testing (pulsa) | Low | High | Use dedicated test SIM cards with controlled balance; verify pre/post balances |
| Intermittent bugs difficult to reproduce | Medium | Medium | Document reproduction rate; attach screen recording; run 10 attempts minimum |
| Staging environment instability | Medium | Medium | Track environment issues separately from app bugs; document timestamps |

---

## 10. Deliverables

- [ ] Test Cases (positive + negative, per module)
- [ ] Bug Reports (ClickUp + exported documentation)
- [ ] API Test Collection (Postman export)
- [ ] Permission Matrix Results (for permission-dependent features)
- [ ] Platform Comparison Notes (Android vs iOS behavioral differences)
- [ ] Test Execution Summary Report
- [ ] UAT Sign-off Document

---

---

# STLC Flow — Software Testing Life Cycle

*(As practiced at PT Indonesia Satu Tujuh across all 7 products)*

```
┌─────────────────────────────────────────────────────────────────────┐
│                SOFTWARE TESTING LIFE CYCLE (STLC)                   │
│              PT Indonesia Satu Tujuh — QA Practice                  │
└─────────────────────────────────────────────────────────────────────┘

Phase 1: REQUIREMENT ANALYSIS
  Input  → BRD / Figma designs / chat discussions (when no formal doc)
  Action → Review and clarify requirements with PM and dev team
           Identify testable requirements
           Flag ambiguities; agree on expected behavior
           For Miniapp: review API contract between host app and Miniapp
  Output → Clarification log; agreed expected behavior per feature

Phase 2: TEST PLANNING
  Input  → Reviewed requirements
  Action → Define scope (in/out), strategy, tools, device matrix
           Identify risks (OEM fragmentation, real-money flows, iOS/Android diff)
           Estimate effort; align timeline with release deadline
  Output → Test Plan Document

Phase 3: TEST CASE DESIGN
  Input  → Test plan + requirements + Figma design
  Action → Write test cases covering:
             Positive (happy path) scenarios
             Negative / invalid input scenarios
             Permission matrix (for permission-dependent features)
             Platform-specific scenarios (Android vs iOS)
             API validation scenarios (Postman)
             Physical accuracy scenarios (for sensor-based features)
  Output → Test Case Document (Google Spreadsheet + Markdown)
  Techniques: EP, BVA, Use Case, Negative Testing, Exploratory, Cross-Platform

Phase 4: TEST ENVIRONMENT SETUP
  Input  → Staging build / production APK from dev team
  Action → Install build on all test devices
           Configure Postman collections with correct base URL and tokens
           Set up Charles Proxy for network traffic inspection
           Verify API endpoints accessible; health check all services
           Prepare test accounts (new user, existing user, admin, etc.)
  Output → Ready-to-execute environment; all devices confirmed working

Phase 5: TEST EXECUTION
  Input  → Test cases + environment
  Action → Execute test cases systematically per module
           Log results: OK / NOT OK / OK With Note per test case
           Report bugs immediately in ClickUp with full evidence
           For multi-device features: coordinate execution across devices
           For physical accuracy: conduct real-world test sessions
           Daily sync with dev team on critical issues
  Output → Executed test cases with results
           Bug reports in ClickUp

Phase 6: BUG REPORTING & TRACKING
  Input  → Failed test cases
  Action → Write clear, reproducible bug reports (see BUG-TEMPLATE)
           Attach evidence: screenshot, screen recording, Logcat, Charles log
           Classify severity and priority
           Track fix status in ClickUp; follow up with assigned developer
           Document "OK With Note" for accepted workarounds
  Output → Tracked and closed bugs; workaround documentation

Phase 7: REGRESSION TESTING
  Input  → Fixed builds from developer
  Action → Re-test fixed bugs (verify fix)
           Run P0 Smoke suite after every build
           Run P1 Core Regression before release
           Verify no new bugs introduced by fixes
           Cross-platform re-verification for critical fixes
  Output → Regression results; Go/No-go recommendation

Phase 8: TEST CLOSURE
  Input  → Passed regression; UAT sign-off
  Action → Write Test Summary Report
           Archive all test artifacts (test cases, bug reports, Postman collections)
           Document platform behavioral differences for future reference
           Lessons learned debrief with team
  Output → Test Summary Report; UAT Sign-off; archived artifacts
```

---

> This STLC process was applied across all 7 products at PT Indonesia Satu Tujuh: Mvicall, Milov, Pantura, CMS Digipac (DPA), CMS Ayolari, Miniapp Ayolari (including accuracy and smartwatch sync testing), and Miniapp V-NSP.
