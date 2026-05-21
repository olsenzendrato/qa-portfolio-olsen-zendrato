# Case Study: Multi-Product Mobile Application Testing

**Role:** Software QA Engineer  
**Company:** PT Indonesia Satu Tujuh (PT INA 17)  
**Products:** Mvicall, Milov, Pantura  
**Platform:** Native Mobile — Android & iOS  
**Duration:** 2024 – 2026  

---

## Background

Alongside the MyTelkomsel Miniapp integration, I was responsible for the ongoing QA cycle of three standalone mobile applications: **Mvicall**, **Milov**, and **Pantura**. Each product served a distinct user base and had its own release cadence, creating a concurrent multi-product testing environment that required strong prioritization and systematic regression management.

---

## The Challenge

**Concurrent testing across 3 active products**  
Each product was in a different development phase at any given time — one in active feature development, one receiving hotfixes, one in pre-release regression. Managing context-switching without missing coverage required disciplined test planning.

**App Store submission deadlines**  
Both Apple App Store and Google Play Store have review cycles that cannot be extended. A missed deadline means a delayed release. Every regression test cycle had a hard cutoff tied to submission windows.

**OS fragmentation on Android**  
The Indonesian market has high diversity in Android versions and OEM customizations (Samsung One UI, Xiaomi MIUI, OPPO ColorOS). Bugs that appeared on one OEM were often invisible on another.

**Hotfix validation speed**  
When a production bug required an emergency hotfix, I had to validate the fix rapidly — often within 2–4 hours — without introducing new regressions.

---

## My Approach

### Structured Regression Suites

For each product, I maintained a **tiered regression suite**:

| Tier | Scope | When Executed |
|---|---|---|
| **Smoke (P0)** | App launch, login, core feature | Every build |
| **Core Regression (P1)** | All high-priority flows | Pre-release |
| **Full Regression (P2)** | Complete test suite | Major release |

This meant I could run a focused 30-minute Smoke test on every new build, escalating to Full Regression only when truly needed — saving significant time across a 3-product environment.

### Android Logcat as a Diagnostic Tool

For every crash or unexpected behavior, I used **Android Studio Logcat** to capture the exact stack trace at the moment of failure. This practice meant bug reports included not just "what happened" but "where in the code it happened" — reducing developer investigation time significantly.

Example workflow:
1. Reproduce bug on physical device connected to Android Studio
2. Filter Logcat by application package name
3. Capture log at exact moment of crash
4. Include filtered log snippet in bug report

### Cross-Device Fragmentation Strategy

Rather than testing on every possible device, I developed a **representative device matrix** covering:
- Low-end Android (Xiaomi Redmi series) — performance and memory constraints
- Mid-range Android (Samsung Galaxy A series) — highest market share segment
- High-end Android (Samsung Galaxy S series) — latest OS version
- Standard iOS (iPhone 13) — most common iOS device in Indonesia
- Latest iOS (iPhone 14+) — newest OS features and API changes
- Small screen iOS (iPhone SE) — layout edge cases

### Defect Communication

All bugs were logged in **ClickUp** with a standardized format I enforced across the team:
- **Title formula:** [Action] + [Component] + [Condition]
- **Required fields:** Steps to Reproduce, Actual vs Expected, Severity, Priority, Device + OS, App Version, Evidence
- **Logcat evidence** attached for all crashes and performance issues

This consistency meant developers could begin investigating without any clarification needed.

---

## Key Testing Highlights

### Mvicall — Double-Submission Bug

During exploratory testing of the payment flow, I discovered that rapidly double-tapping the "Confirm" CTA during slow network conditions triggered duplicate API calls — potentially resulting in duplicate charges. This was a High severity bug that would have reached production undetected if not for deliberate network throttling during testing.

**Finding method:** Exploratory testing + Charles Proxy network throttling + Logcat monitoring simultaneously

### Milov — Pagination Duplication

Search result pagination was showing duplicate content items when the user scrolled quickly to trigger the next page load. The bug was intermittent (6/10 reproducibility) and tied to a race condition in the pagination API call timing.

**Finding method:** Exploratory testing with rapid scroll behavior on slow 4G network

### Pantura — iOS 17 Background State Bug

After an iOS 17 update, Pantura stopped properly restoring its state when returning from background. The home feed would either be blank or show stale data. This regression was caught in the post-update smoke test before any user reported it.

**Finding method:** Regression testing triggered by OS version update

---

## Process Improvement: Regression Grouping

Early in my time managing three concurrent products, regression cycles were taking too long — running every test case for every build was unsustainable. I reorganized the test suites into the tiered P0/P1/P2 structure described above, grouping test cases by functional module rather than by feature addition date.

**Result:** Smoke test execution time reduced from ~90 minutes to ~30 minutes per product, enabling faster developer-QA feedback loops without sacrificing coverage on critical flows.

---

## Outcome

| Metric | Result |
|---|---|
| Products managed concurrently | 3 (Mvicall, Milov, Pantura) |
| Platforms covered | Android (4+ devices) + iOS (3+ devices) |
| App Store submissions with zero critical blockers | 100% during my tenure |
| Regression efficiency improvement | ~67% reduction in smoke test execution time |
| Critical bugs caught before production | Multiple per release cycle |

---

## Artifacts

- [Mvicall Test Cases](../01-test-cases/mobile-apps/Mvicall-TestCases.md)
- [Bug Report Samples](../02-bug-reports/sample-bug-reports.md)
- [Test Plan Template](../04-test-plans/Test-Plan-Template.md)

---

> *All proprietary product data, user metrics, and business-specific details have been anonymized.*
