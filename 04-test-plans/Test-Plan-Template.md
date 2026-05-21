# 04 — Test Plans & STLC Documentation

Professional test planning documentation reflecting the Software Testing Life Cycle (STLC) process followed across multiple product releases.

---

# Test Plan Template

## 1. Project Overview

| Field | Detail |
|---|---|
| **Project Name** | [Project / Feature Name] |
| **Application** | [App Name & Version] |
| **Platform** | Web / Android / iOS / All |
| **Test Plan Version** | v1.0 |
| **Prepared By** | Olsen Yeremia Zendrato |
| **Date** | YYYY-MM-DD |
| **Sprint / Release** | Sprint [X] / Release [Y] |

---

## 2. Scope of Testing

### In Scope
- [Feature 1 — brief description]
- [Feature 2 — brief description]
- [Feature 3 — brief description]

### Out of Scope
- [Excluded feature or platform — reason]
- [Performance load testing (handled separately)]

---

## 3. Test Objectives

1. Verify all features meet the requirements specified in the BRD/PRD.
2. Ensure no regression in existing stable features after new changes.
3. Validate API responses are correct, secure, and performant.
4. Confirm UI/UX matches approved Figma designs across all target devices.
5. Ensure zero Critical or High severity bugs exist before UAT handoff.

---

## 4. Test Strategy

| Testing Type | Approach | Tools |
|---|---|---|
| Functional Testing | Black-box manual execution against BRD | Google Spreadsheet, ClickUp |
| API Testing | Request/response validation per spec | Postman |
| UI/UX Testing | Visual comparison against Figma | Real devices, screenshots |
| Regression Testing | Re-execute core test suite after each build | Manual |
| Exploratory Testing | Unscripted sessions targeting edge cases | Real devices |
| Cross-device Testing | Execute key flows on device matrix | Physical Android & iOS devices |

---

## 5. Entry & Exit Criteria

### Entry Criteria (Testing can begin when:)
- [ ] BRD / PRD has been reviewed and signed off
- [ ] Development build is deployed to staging environment
- [ ] API documentation is available and endpoints are accessible
- [ ] Test devices are available and configured
- [ ] Test cases have been reviewed by QA lead

### Exit Criteria (Testing is complete when:)
- [ ] All High and Critical priority test cases have been executed
- [ ] Zero open Critical or High severity bugs
- [ ] Regression suite passes with ≥ 95% pass rate
- [ ] All UI/UX feedback has been implemented and re-verified
- [ ] Test summary report has been submitted

---

## 6. Test Environment

| Environment | Detail |
|---|---|
| **Staging URL / Build** | [Staging URL or APK build version] |
| **Test Data** | [Source of test accounts and data] |
| **API Environment** | Staging — Base URL: `https://api-staging.[platform].id` |
| **Network** | WiFi + Throttled 3G simulation via Charles Proxy |

### Device Matrix

| Device | OS | Platform |
|---|---|---|
| Samsung Galaxy A54 | Android 13 | Android |
| Samsung Galaxy S23 | Android 14 | Android |
| Xiaomi Redmi Note 12 | Android 13 | Android |
| iPhone 13 | iOS 16.x | iOS |
| iPhone 14 Pro | iOS 17.x | iOS |
| iPhone SE (3rd Gen) | iOS 16.x | iOS |

---

## 7. Test Schedule

| Phase | Activity | Duration |
|---|---|---|
| Week 1 | Requirement review, test case authoring | 2 days |
| Week 1 | Test case review & sign-off | 1 day |
| Week 1–2 | Test execution (functional, API, UI) | 4 days |
| Week 2 | Bug reporting & developer fix cycle | 2 days |
| Week 2 | Regression & re-test | 1 day |
| Week 2 | UAT preparation & handoff | 1 day |

---

## 8. Defect Management

- All bugs logged in **ClickUp** with required fields: Title, Steps to Reproduce, Severity, Priority, Environment, Evidence
- Bug status workflow: `Open` → `In Progress` → `Fixed` → `Re-test` → `Closed` / `Rejected`
- Daily bug triage with development team during active testing phase
- Critical bugs require same-day response from developer

---

## 9. Risks & Mitigation

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Late delivery of staging build | Medium | High | Buffer 1 day in schedule; begin API test case prep early |
| Device not available for specific OS version | Low | Medium | Use Android Studio emulator as fallback |
| Incomplete BRD / requirements unclear | Medium | High | Early review session with PM before test case writing |
| Intermittent staging environment instability | Medium | Medium | Document environment issues separately from app bugs |

---

## 10. Deliverables

- [ ] Test Cases (Google Spreadsheet + Markdown)
- [ ] Bug Reports (ClickUp + documentation export)
- [ ] API Test Collection (Postman export)
- [ ] Test Execution Summary Report
- [ ] UAT Sign-off Document

---

---

# STLC Flow — Software Testing Life Cycle

```
┌─────────────────────────────────────────────────────────────┐
│               SOFTWARE TESTING LIFE CYCLE (STLC)            │
│                   as practiced at PT INA 17                  │
└─────────────────────────────────────────────────────────────┘

Phase 1: REQUIREMENT ANALYSIS
  Input  → BRD / PRD from Product Manager
  Action → QA reads and clarifies requirements
            Identify testable vs non-testable requirements
            Flag ambiguities early
  Output → Requirement Understanding Document / Clarification Log

Phase 2: TEST PLANNING
  Input  → Reviewed requirements
  Action → Define scope, strategy, tools, schedule
            Identify risk areas
            Estimate effort and timeline
  Output → Test Plan Document

Phase 3: TEST CASE DESIGN
  Input  → Test Plan + Requirements
  Action → Write test cases covering:
            • Happy paths (valid flows)
            • Edge cases (boundary values)
            • Negative scenarios (invalid inputs)
            • Integration flows (API + UI)
  Output → Test Case Document (Google Spreadsheet / Markdown)
  Technique → BVA, EP, Use Case, Decision Table, Exploratory

Phase 4: TEST ENVIRONMENT SETUP
  Input  → Staging build from development team
  Action → Configure test devices
            Set up Postman collections
            Configure Charles Proxy
            Verify API endpoints accessible
  Output → Ready-to-test environment confirmed

Phase 5: TEST EXECUTION
  Input  → Test Cases + Test Environment
  Action → Execute test cases systematically
            Log results (Pass / Fail / Blocked)
            Report bugs immediately with full documentation
            Daily sync with dev team on critical issues
  Output → Executed test cases with results
            Bug reports in ClickUp

Phase 6: BUG REPORTING & TRACKING
  Input  → Failed test cases
  Action → Write clear, reproducible bug reports
            Assign severity and priority
            Attach evidence (screenshot, video, Logcat)
            Track fix status with developer
  Output → Closed/Verified bugs

Phase 7: REGRESSION TESTING
  Input  → Fixed builds from developer
  Action → Re-test fixed bugs
            Run regression suite on core flows
            Verify no new bugs introduced by fixes
  Output → Regression test results
            Go/No-go recommendation for UAT

Phase 8: TEST CLOSURE
  Input  → Passed regression, UAT sign-off
  Action → Write Test Summary Report
            Archive test artifacts
            Document lessons learned
  Output → Test Summary Report
            UAT Sign-off Document
```

---

> This STLC flow was practiced across multiple product releases at PT Indonesia Satu Tujuh, including the MyTelkomsel Miniapp integration, CMS Digipac, and mobile app projects (Mvicall, Milov, Pantura).
