# 01 — Test Cases

Folder ini berisi dokumentasi test case terstruktur berdasarkan pengalaman QA nyata di PT Indonesia Satu Tujuh (PT INA 17), mencakup pengujian multi-platform pada ekosistem digital skala nasional.

---

## Projects Covered

| Project | Platform | Type | Scale |
|---|---|---|---|
| **Mvicall** | Mobile Android & iOS | Video Ringtone App | Consumer Mobile |
| **Milov** | Mobile Android & iOS | Love Match Game App | Consumer Mobile |
| **Pantura** | Mobile Android & iOS | Dangdut Music & Quiz App | Consumer Mobile |
| **CMS Digipac (DPA)** | Web Back-End | Digital Partner Activation CMS | B2B Enterprise |
| **CMS Ayolari** | Web Back-End | Miniapp Traffic Monitoring CMS | Internal Dashboard |
| **Miniapp Ayolari** | Mobile Android & iOS (MyTelkomsel) | Running Tracker Miniapp | National Telecom Ecosystem |
| **Miniapp V-NSP** | Mobile Android (MyTelkomsel) | Video Nada Sambung Pribadi | National Telecom Ecosystem |

---

## Test Design Techniques Applied

| Technique | Description | Applied On |
|---|---|---|
| **Equivalence Partitioning (EP)** | Grouping inputs into valid and invalid partitions | Login forms, input fields, upload validations |
| **Boundary Value Analysis (BVA)** | Testing at exact boundary of valid/invalid ranges | Character limits, file size limits, date ranges |
| **Use Case Testing** | Tracing end-to-end user journeys (happy path + edge cases) | All projects — core user flows |
| **Negative Testing** | Deliberately invalid inputs to verify error handling | All projects — dedicated negative case suites |
| **Exploratory Testing** | Unscripted sessions targeting unexpected behavior | Mobile apps, miniapp integrations |
| **Cross-Device Testing** | Testing across multiple physical Android & iOS devices | All mobile projects |
| **Cross-Platform Testing** | Android vs iOS behavioral comparison | Ayolari, VNSP, Mvicall, Milov |

---

## Standard Test Case Format

| Field | Description |
|---|---|
| **Test ID** | Unique identifier per module (e.g., WP_1_1, LG_1_2) |
| **Feature / Module** | The feature being tested |
| **Preconditions** | State required before execution |
| **Test Scenario / Steps** | Step-by-step actions |
| **Expected Result** | What should happen |
| **Actual Result** | What actually happened |
| **Status** | OK / NOT OK / OK With Note |
| **Note** | Additional observations, known issues, or conditional behavior |
| **Device / Environment** | Device model, OS version, build version |

---

## Device Matrix Summary (Across All Projects)

### Android
| Device | OS | Used In |
|---|---|---|
| Samsung Galaxy A23 | Android 14 | Ayolari v9.2, VNSP |
| Samsung Galaxy S23 | Android 14 | Ayolari accuracy test |
| Samsung Galaxy A51 | Android 11 | Ayolari accuracy test |
| Vivo T1 Pro 5G | Android 13 | Mvicall, Milov, Pantura |
| Realme 9 5G | Android 13 | Mvicall |
| Realme 9 Pro | Android 13 | Milov, Ayolari accuracy test |
| Poco M3 | Android 13 | VNSP |
| OPPO Reno8 T | Android 15 | VNSP, Ayolari accuracy test |
| Xiaomi Redmi Note 12 | Android 13 | General |
| ITEL RS4 | Android 14 | VNSP |
| Techno Spark 30C | Android 14 | VNSP, Ayolari accuracy test |
| Infinix Hot 50i | Android 14 | VNSP |

### iOS
| Device | OS | Used In |
|---|---|---|
| iPhone X | iOS 16.7 | Mvicall |
| iPhone XI | iOS 16.3 | Mvicall |
| iPhone 11 Pro Max | iOS 16 | Ayolari v9.2 |
| iPhone 11 | iOS 16 | Ayolari accuracy test |

---

## Folder Structure

```
01-test-cases/
├── web-cms/
│   ├── CMS-Digipac-TestCases.md        ← Digital Partner Activation (DPA) CMS
│   └── CMS-Ayolari-TestCases.md        ← Ayolari monitoring & management CMS
├── mobile-apps/
│   ├── Mvicall-TestCases.md            ← Video Ringtone mobile app
│   ├── Milov-TestCases.md              ← Love Match Game mobile app
│   └── Pantura-TestCases.md            ← Dangdut Music & Quiz mobile app
└── miniapp/
    ├── MyTelkomsel-Miniapp-Ayolari-TestCases.md    ← Running tracker miniapp
    └── MyTelkomsel-Miniapp-VNSP-TestCases.md       ← Video Nada Sambung Pribadi
```

---

> All test cases are based on real QA work performed at PT Indonesia Satu Tujuh. Confidential business data, internal URLs, credentials, and proprietary system details have been removed or anonymized.
