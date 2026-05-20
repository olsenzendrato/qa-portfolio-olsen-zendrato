# Test Cases — Mvicall Mobile Application

**Project:** Mvicall  
**Platform:** Native Mobile — Android & iOS  
**Testing Type:** Functional, UI/UX, Regression, Performance  
**Techniques:** Use Case Testing, BVA, Exploratory, EP  

---

## Module 1: User Registration & Onboarding

| Test ID | Scenario | Preconditions | Test Steps | Test Data | Expected Result | Technique | Priority |
|---|---|---|---|---|---|---|---|
| TC-MVC-001 | Register with valid phone number | Fresh app install | 1. Open app<br>2. Tap Register<br>3. Enter valid phone number<br>4. Request OTP | Phone: +6281234567890 | OTP SMS received within 60 seconds. Input field enabled for OTP entry. | Use Case | High |
| TC-MVC-002 | Register with invalid phone format | Fresh app install | 1. Tap Register<br>2. Enter phone number with letters | Phone: 0812-abc-xyz | Validation error: "Please enter a valid phone number." OTP not requested. | EP (Invalid) | High |
| TC-MVC-003 | OTP expires and user requests resend | OTP sent but expired | 1. Wait for OTP timeout (60s)<br>2. Tap "Resend OTP" | — | New OTP sent. Previous OTP no longer valid. Resend button has 60s cooldown. | Use Case | High |
| TC-MVC-004 | Register with already-used phone number | Number already registered | 1. Enter registered phone number<br>2. Request OTP | Existing number | Error: "This number is already registered. Please login instead." | EP (Invalid) | High |
| TC-MVC-005 | Complete registration with valid profile data | OTP verified | 1. Enter name, profile photo<br>2. Tap Complete Registration | Name: "Olsen Test"<br>Photo: JPG < 5MB | Profile created. User lands on app home screen. Welcome notification shown. | Use Case | High |

---

## Module 2: Core App Features — Functional Testing

| Test ID | Scenario | Preconditions | Test Steps | Test Data | Expected Result | Technique | Priority |
|---|---|---|---|---|---|---|---|
| TC-MVC-010 | Browse and open content item | Logged in | 1. Scroll home feed<br>2. Tap any content card | — | Content detail page opens. Title, description, media load correctly. | Use Case | High |
| TC-MVC-011 | Search for specific content | Logged in | 1. Tap search icon<br>2. Type keyword<br>3. View results | Keyword: "promo" | Results returned within 3 seconds. Relevant items displayed. | Use Case | High |
| TC-MVC-012 | Search with no results | Logged in | 1. Search for nonexistent keyword | Keyword: "xyzabc123" | Empty state shown: "No results found for 'xyzabc123'". No crash. | EP (Invalid) | Medium |
| TC-MVC-013 | Pull-to-refresh updates feed | Logged in, feed loaded | 1. Pull down on home feed | — | Loading indicator shown. Feed refreshed with latest content. | Use Case | Medium |
| TC-MVC-014 | App handles incoming call during use | Active session in app | 1. Receive phone call while using app<br>2. End call and return to app | — | App state preserved after call ends. No crash or data loss. | Exploratory | High |

---

## Module 3: UI/UX — Visual Regression Testing

| Test ID | Screen | Device | Check Points | Expected Result | Priority |
|---|---|---|---|---|---|
| TC-UI-001 | Home Screen | Samsung Galaxy A54 (Android 13) | Layout, card spacing, navbar, typography | Matches Figma design. No overflow or overlap. | High |
| TC-UI-002 | Home Screen | iPhone 13 (iOS 16) | Layout, card spacing, navbar, typography | Matches Figma design. Safe area insets correct. | High |
| TC-UI-003 | Profile Screen | Both platforms | Avatar, edit fields, CTA alignment | All elements correctly spaced. No truncation. | Medium |
| TC-UI-004 | Notification Screen | Both platforms | Notification list, read/unread state | Correct badge count. Read state visually distinct. | Medium |
| TC-UI-005 | Empty states (no content, no internet) | Both platforms | Illustration, message text, CTA | Illustration visible. Message clear and friendly. | Medium |

---

## Module 4: Regression Test Suite (Pre-Release)

Executed before every App Store / Google Play deployment.

| Test ID | Feature | Regression Scope | Priority |
|---|---|---|---|
| TC-REG-001 | Login / Logout | Full flow re-test | High |
| TC-REG-002 | Home feed loads | Content visible on launch | High |
| TC-REG-003 | Deep links functional | External links open correct screen | High |
| TC-REG-004 | Push notifications received | Tap notification opens correct screen | High |
| TC-REG-005 | App does not crash on launch | Cold start on Android & iOS | High |
| TC-REG-006 | In-app navigation | All bottom tabs functional | Medium |
| TC-REG-007 | Media playback | Video/audio plays without buffering issues | Medium |
| TC-REG-008 | Form submissions | All forms submit without errors | Medium |

---

> **Note:** All test data is anonymized. Real device testing was performed on physical Android and iOS devices as documented in the device matrix.
