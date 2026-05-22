# Case Study: MyTelkomsel Miniapp Integration — Ayolari & V-NSP

**Role:** Lead QA Analyst  
**Company:** PT Indonesia Satu Tujuh (PT INA 17)  
**Duration:** 2024 – 2026  
**Platform:** Mobile Application (Android & iOS) — MyTelkomsel Super App Ecosystem  
**Scale:** National-level Telkomsel digital ecosystem  

---

## Background

MyTelkomsel is Telkom Indonesia's primary super-app, serving tens of millions of active users. PT INA 17 was engaged to develop, integrate, and maintain two Miniapps within the MyTelkomsel lifestyle ecosystem:

**Ayolari** — A running tracker Miniapp where users can record running activities, join challenges, claim rewards, and sync smartwatch data — all within the MyTelkomsel app. (Source: Telkomsel official blog)

**V-NSP (Video Nada Sambung Pribadi)** — A service that replaces the standard call waiting tone with a personalized video. When User A calls User B via WhatsApp, User A sees a custom V-NSP video while waiting for the call to be answered. (Source: Telkomsel official V-NSP page)

As Lead QA Analyst, I was responsible for the entire quality gate of both integrations — from requirement analysis and test planning through to production deployment across multiple release cycles.

---

## The Challenge

### Ayolari — Running Tracker Miniapp

**1. Sensor Accuracy Validation**  
Beyond standard functional testing, Ayolari required physical accuracy testing — real outdoor runs and treadmill sessions comparing Ayolari's recorded data against reference smartwatches (Garmin). This was unique QA work: I had to physically run while monitoring test variables.

**2. Smartwatch Compatibility Matrix**  
Ayolari syncs with multiple smartwatch brands via Google Health Connect (Android) and Apple Health (iOS). Each combination of watch brand, health app, and OS platform needed to be individually tested — creating a complex compatibility matrix.

**3. Cross-Platform Navigation Differences**  
iOS and Android behave differently for deeplink-based navigation within Miniapps. Privacy Policy links opened via deeplink exit the Miniapp entirely on iOS (no back button available), while Android's native back button allows return. This required careful documentation and a recommended architectural fix.

**4. Multi-Version User Consent Flow**  
In v9.2, two separate consent pages were introduced — one for MyTelkomsel and one for Ayolari — with different persistence behaviors. The Ayolari consent is shown only once and persists even after MyTelkomsel reinstallation. Testing and documenting this behavior clearly was critical to prevent regression.

### V-NSP — Video Nada Sambung Pribadi

**1. Background Service Reliability Across OEM Devices**  
V-NSP relies on a foreground service (`startforeground`) running in the background to intercept incoming WhatsApp calls and display the video. Different Android OEM manufacturers (Samsung, OPPO, Xiaomi, POCO, ITEL, Techno, Infinix) have aggressive battery optimization and background kill behaviors that could prevent this service from running — making cross-OEM testing critical.

**2. Permission Architecture Complexity**  
V-NSP requires multiple system permissions: notification access, overlay (display over other apps), AutoStart Background (Chinese OEM specific), and battery optimization exemption. Each combination of granted/skipped permissions produces different behavior, requiring a dedicated permission matrix test suite.

**3. Multi-Tester Coordination**  
V-NSP testing involved a team of 5 testers (Olsen, Dhafin, Resta, Marcel, Hasbi) across 7 devices simultaneously. Coordinating execution, tracking results per device, and maintaining consistent documentation required structured test management.

---

## My Approach

### Test Planning & Requirement Analysis

For each release, I began with a full review of available requirements — BRDs, Figma designs, and internal chat discussions (especially for features with no formal spec). I mapped:
- Happy paths and core user journeys
- Negative scenarios and edge cases
- Platform-specific behavioral differences (Android vs iOS)
- Integration boundaries (token handoff, API contracts, health data sync)

### Ayolari — Accuracy Testing (Real-World Physical Testing)

For running accuracy validation, I designed a structured physical test protocol:

**Outdoor accuracy test:**
- Conducted real outdoor runs using multiple Android devices simultaneously
- Reference device: Garmin Watch (Garmin Connect app)
- Measured: Duration, Distance, Pace, Calories per 500m intervals

**Results:**
| Metric | Accuracy vs Garmin | Result |
|---|---|---|
| Duration | 0–30 second margin | ✅ Passed |
| Distance | 0–0.03 km per 500m | ✅ Passed |
| Pace | avg ±15 sec/km per 500m | ✅ Passed |
| Calories | ~+16 kcal higher (+48%) | 📝 Needs tuning |

**Indoor (treadmill) accuracy test:**
- Same protocol on treadmill, comparing with Garmin
- Identified that Xiaomi Mi Fitness does not send treadmill workout data to Health Connect — causing indoor sync failure for Xiaomi watches

**Smartwatch Sync Matrix (12 devices x 2 platforms):**
Tested 8 distinct smartwatch models across Android and iOS, using their native health apps as the sync bridge. Documented specific incompatibilities (e.g., Samsung Wear OS watches not supported by Apple Health; Oppo Watch OHealth app only syncs steps on iOS — no full workout sync).

### V-NSP — OEM Permission Matrix Testing

For V-NSP, I structured the permission testing into a matrix covering:
- 3 permission categories: Notification, Overlay (display over apps), AutoStart Background + Battery Optimize
- 7 OEM devices with different Android skins
- 4 negative scenarios: skipping each permission type individually

**Key finding:** AutoStart Background and Battery Optimize permissions are optional on most devices — startforeground still runs without them. However, without these permissions, the service is more likely to be killed by aggressive battery management on Chinese OEM devices (OPPO, Xiaomi, POCO), degrading the V-NSP experience.

### Multi-Device Coordination (V-NSP)

For the 5-tester, 7-device V-NSP test execution:
- I created a structured result sheet with per-device columns for each test case
- Each tester's results were tracked by tester name + device in the result columns
- A cross-check final column validated consistency across all testers before sign-off
- Daily sync with the development team on any inter-device behavioral differences

---

## Key Bugs Found & Impact

### Ayolari

| Bug | Severity | Impact | Resolution |
|---|---|---|---|
| iOS Privacy Policy deeplink exits Miniapp — no return path | Medium | All iOS new users affected during onboarding | Documented with architectural fix recommendation (use in-app WebView) |
| Calorie tracking consistently higher than reference by ~48% | Medium | Data accuracy for health-conscious users | Flagged for algorithm adjustment |
| Xiaomi Watch indoor treadmill sync not working | Medium | Affects all Xiaomi Watch users on treadmill mode | Root cause: Mi Fitness does not forward treadmill data to Health Connect |

### V-NSP

| Bug | Severity | Impact | Resolution |
|---|---|---|---|
| startforeground does not run when user skips any required permission | High | V-NSP feature completely non-functional without correct permissions | Expected behavior documented; user guided to grant all permissions |
| Custparam from pre-production environment accepted in onboarding but blocks landing page | Medium | Could confuse internal testers using wrong config | Documented; env isolation recommended |

---

## Outcome

### Ayolari (v9.2 — March 2026)

| Metric | Result |
|---|---|
| Test cases executed | 50+ (positive + negative) |
| Smartwatch models validated | 8 (Android + iOS) |
| Devices tested — accuracy | 12 physical devices |
| Running sessions conducted | Multiple (outdoor + treadmill) |
| Critical blockers at UAT | 0 |
| Production deployment | Successful |

### V-NSP (July 2025)

| Metric | Result |
|---|---|
| Test cases executed | 80+ (positive + negative) |
| Devices tested | 7 across 5 Android OEMs |
| Testers coordinated | 5 |
| Permission scenarios covered | 10+ |
| Critical blockers at UAT | 0 |
| Production deployment | Successful |

---

## Lessons Learned

**1. Physical accuracy testing requires its own test protocol.**  
Standard software testing methods don't apply to sensor-based features. I had to design a repeatable physical test procedure — fixed distances, reference devices, multiple devices run simultaneously — to produce meaningful accuracy data.

**2. OEM fragmentation on Android is a real and significant testing challenge.**  
A test that passes on Samsung may fail on POCO or ITEL due to OEM-specific battery management and background process policies. Device diversity in the test matrix is non-negotiable for products targeting the Indonesian market.

**3. Platform differences (Android vs iOS) must be explicitly tested, documented, and communicated.**  
What works seamlessly on Android may behave completely differently on iOS at the navigation and permission level. These differences need clear documentation and architectural recommendations — not just bug reports.

**4. Multi-tester coordination requires clear structure upfront.**  
When coordinating 5 testers across 7 devices, an unstructured result sheet creates confusion fast. Building a per-tester, per-device result tracking format before execution begins saves significant time during analysis.

---

## Artifacts

- [Test Cases — Ayolari & V-NSP Miniapp](../01-test-cases/miniapp/)
- [Bug Report Samples](../02-bug-reports/sample-bug-reports.md)
- [Test Plan Template](../04-test-plans/Test-Plan-Template.md)

---

> *All proprietary business data, internal API endpoints, MSISDN identifiers, authentication tokens, and production metrics have been anonymized in accordance with confidentiality obligations to PT Indonesia Satu Tujuh.*
