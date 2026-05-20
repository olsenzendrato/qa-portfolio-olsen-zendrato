# Test Cases — MyTelkomsel Miniapp Integration

**Project:** Ayolari & VNSP Miniapp Integration into MyTelkomsel  
**Platform:** Mobile Application (Android & iOS) + Web CMS  
**Testing Type:** Functional, UI/UX, Integration, API, Regression  
**Techniques:** BVA, Equivalence Partitioning, Use Case, Exploratory  
**Scale:** National-level telecom digital ecosystem  

---

## Module 1: Miniapp Entry Point & Launch

| Test ID | Scenario | Preconditions | Test Steps | Test Data | Expected Result | Technique | Priority |
|---|---|---|---|---|---|---|---|
| TC-MA-001 | Miniapp banner displays on MyTelkomsel home | App installed & logged in | 1. Open MyTelkomsel app<br>2. Scroll to lifestyle section | — | Ayolari/VNSP banner visible with correct image, title, and CTA button | Use Case | High |
| TC-MA-002 | Tap banner successfully opens Miniapp | App installed & logged in | 1. Tap Ayolari banner | — | Miniapp loads within 5 seconds. Loading state (spinner/skeleton) shown during load. | Use Case | High |
| TC-MA-003 | Miniapp loads under slow network | App installed, network throttled to 3G | 1. Set network to Slow 3G via Charles Proxy<br>2. Tap Miniapp banner | — | Miniapp loads with graceful loading state. No crash. Max load time: 10 seconds. | Exploratory | High |
| TC-MA-004 | Miniapp fails to load on no internet | No internet connection | 1. Disable WiFi & mobile data<br>2. Tap Miniapp banner | — | Error state displayed with message "No internet connection. Please try again." Back button functional. | EP (Invalid) | High |
| TC-MA-005 | Miniapp back button returns to MyTelkomsel | Inside Miniapp | 1. Open Miniapp<br>2. Press device back button | — | User returned to MyTelkomsel home. MyTelkomsel state (scroll position, tab) preserved. | Use Case | High |

---

## Module 2: Authentication Token & Session Handling

| Test ID | Scenario | Preconditions | Test Steps | Test Data | Expected Result | Technique | Priority |
|---|---|---|---|---|---|---|---|
| TC-MA-010 | Miniapp receives valid auth token from host app | User logged into MyTelkomsel | 1. Open Miniapp<br>2. Monitor network via Charles Proxy | — | Auth token passed in request header. Token format matches specification. Status 200 OK received. | Use Case | High |
| TC-MA-011 | Miniapp behaves correctly with expired token | Token manually expired | 1. Expire token via test environment<br>2. Open Miniapp | Expired token | Miniapp triggers re-authentication flow OR displays session expired message gracefully. No raw error shown to user. | EP (Invalid) | High |
| TC-MA-012 | Session timeout after 30 minutes idle | User inside Miniapp | 1. Open Miniapp<br>2. Leave idle for 30+ minutes<br>3. Attempt interaction | — | User prompted to re-login OR session refreshed silently. No data loss on return. | Use Case | Medium |
| TC-MA-013 | Token not shared across different Miniapps | Both Ayolari & VNSP installed | 1. Login to Ayolari<br>2. Open VNSP Miniapp | — | VNSP requires separate authentication. Ayolari token not reused by VNSP. | Exploratory | High |

---

## Module 3: UI/UX Compliance Validation

| Test ID | Scenario | Preconditions | Test Steps | Expected Result | Technique | Priority |
|---|---|---|---|---|---|---|
| TC-MA-020 | Miniapp matches approved Figma design | Figma spec available | 1. Open Miniapp on test device<br>2. Compare each screen vs Figma spec | All typography, colors, spacing, padding, and button states match the approved design. Pixel deviation < 2px for key elements. | Use Case | High |
| TC-MA-021 | Miniapp responsive on small screen (5-inch) | Samsung Galaxy A series device | 1. Open Miniapp<br>2. Navigate all screens | No element overflow, no truncated text, no overlapping buttons | Use Case | High |
| TC-MA-022 | Miniapp responsive on large screen (6.7-inch) | iPhone 14 Pro Max or equivalent | 1. Open Miniapp<br>2. Navigate all screens | Layout scales correctly. No excessive whitespace. Content fills screen appropriately. | Use Case | Medium |
| TC-MA-023 | Miniapp renders correctly in dark mode | Device dark mode enabled | 1. Enable dark mode on device<br>2. Open Miniapp | Text readable, icons visible, no white-on-white or black-on-black elements | Exploratory | Medium |
| TC-MA-024 | CTA buttons have correct tap target size | — | 1. Open Miniapp<br>2. Inspect all primary buttons | All interactive buttons are minimum 44x44pt tap target per iOS HIG / Android Material guidelines | Use Case | Medium |

---

## Module 4: API Integration Validation (Postman)

| Test ID | Endpoint | Method | Scenario | Expected Status | Expected Behavior | Priority |
|---|---|---|---|---|---|---|
| TC-API-001 | `/miniapp/launch` | POST | Valid launch with token | 200 OK | Response includes `miniapp_url`, `session_id`, `user_context` | High |
| TC-API-002 | `/miniapp/launch` | POST | Launch with missing token | 401 Unauthorized | Response body: `{"error": "Unauthorized", "message": "Token missing or invalid"}` | High |
| TC-API-003 | `/miniapp/content` | GET | Fetch homepage content | 200 OK | Response array contains at least 1 content item with `id`, `title`, `thumbnail_url`, `deeplink` | High |
| TC-API-004 | `/miniapp/content` | GET | Fetch with invalid miniapp_id | 404 Not Found | Response: `{"error": "Miniapp not found"}` | Medium |
| TC-API-005 | `/miniapp/track` | POST | Track user click event | 200 OK | Event logged. Response: `{"status": "tracked", "event_id": "..."}` | Medium |

---

## Module 5: Cross-Platform Device Matrix

| Test ID | Device | OS | Scenario | Expected Result |
|---|---|---|---|---|
| TC-DEV-001 | Samsung Galaxy A54 | Android 13 | Full Miniapp user journey | All features functional, no layout breaks |
| TC-DEV-002 | Samsung Galaxy S23 | Android 14 | Full Miniapp user journey | All features functional, no layout breaks |
| TC-DEV-003 | Xiaomi Redmi Note 12 | Android 13 | Full Miniapp user journey | All features functional, no layout breaks |
| TC-DEV-004 | iPhone 13 | iOS 16.x | Full Miniapp user journey | All features functional, no layout breaks |
| TC-DEV-005 | iPhone 14 Pro | iOS 17.x | Full Miniapp user journey | All features functional, no layout breaks |
| TC-DEV-006 | iPhone SE (3rd Gen) | iOS 16.x | Full Miniapp user journey | Layout correct on small 4.7-inch screen |

---

> **Note:** Test scenarios are based on real integration work performed in MyTelkomsel environment. All proprietary data, API endpoints, and business logic have been anonymized for confidentiality.
