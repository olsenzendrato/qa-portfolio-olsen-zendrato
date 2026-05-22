# Test Cases — MyTelkomsel Miniapp Integration

**Projects:** Miniapp Ayolari & Miniapp V-NSP (Video Nada Sambung Pribadi)  
**Platform:** Mobile Application Android & iOS — MyTelkomsel Super App Ecosystem  
**Scale:** National-level Telkomsel digital ecosystem  
**Tester:** Olsen Yeremia Zendrato  

---

# PART 1 — MINIAPP AYOLARI

**Version Tested:** 9.2.0-1006907623 (Android) | 9.2.0-1006878299 (iOS)  
**Testing Date:** March 2–9, 2026  
**Device:** Samsung Galaxy A23 (Android 14) | iPhone 11 Pro Max (iOS 16)  

**About:** Ayolari is a running tracker miniapp embedded inside MyTelkomsel super app. Users can record running activities, join challenges, claim rewards, and sync smartwatch data — all within the MyTelkomsel ecosystem.

---

## Device Matrix — Ayolari

| Device | OS | Platform |
|---|---|---|
| Samsung Galaxy A23 | Android 14 | Android (Primary) |
| iPhone 11 Pro Max | iOS 16 | iOS (Primary) |
| Oppo Reno 8T 5G | Android | Accuracy testing |
| Realme 9 Pro | Android | Accuracy testing |
| Samsung Galaxy S23 | Android 14 | Accuracy testing |
| Samsung Galaxy S24 | Android | Accuracy testing |
| iPhone 11 | iOS | Accuracy testing |

---

## Module A1: User Consent Page

| No | Test Case | Expected Result | Status | Note |
|---|---|---|---|---|
| 1 | New user opens Ayolari for the first time after fresh MyTelkomsel install — all permissions granted | User Consent Page displayed; Ayolari-specific permissions requested | OK | In v9.2, two consent pages exist: MyTelkomsel consent (shown every reinstall) and Ayolari consent (shown only once, persists after reinstall) |
| 2 | Tap Terms & Conditions link | User directed to Ayolari Terms & Conditions page | OK | — |
| 3 | Tap Privacy Policy link | User directed to Ayolari Privacy Policy page | OK | On iOS: Privacy Policy opens via deeplink, swipe back exits to MyTelkomsel. On Android: back button returns to Consent Page |
| 4 | New user taps "Setuju & Lanjutkan" (checkbox checked) | User directed to Onboarding → Register page | OK | — |
| 5 | Existing user taps "Setuju & Lanjutkan" | User directed directly to Beranda (home) | OK | — |
| 6 | Back navigation from Terms & Conditions page | Returns to User Consent Page | OK | — |
| 7 | Back navigation from Privacy Policy page | Returns to User Consent Page (Android) / Exits to MyTelkomsel (iOS) | OK | iOS behavior difference due to deeplink navigation; documented |
| 8 | New user reopens Ayolari after previously accepting consent | MyTelkomsel consent shown again; Ayolari consent NOT shown again | OK | — |
| 9 | Existing user reopens Ayolari after previously accepting consent | Ayolari consent NOT shown; user goes directly to beranda | OK | — |

### Negative Cases — User Consent

| No | Test Case | Expected Result | Status |
|---|---|---|---|
| 1 | Tap "Setuju & Lanjutkan" without checking checkbox | Button remains disabled; cannot proceed | OK |
| 2 | New user denies all MyTelkomsel permissions, then opens Ayolari | System requests additional permissions not yet granted; alert shown to enable Ayolari-required permissions | OK |

---

## Module A2: Register

| No | Test Case | Expected Result | Status | Note |
|---|---|---|---|---|
| 1 | Fill all registration fields correctly → tap "Selesai" | New Ayolari account created; user redirected to beranda | OK | Testing used dedicated tester number for repeat registration scenarios |
| 2 | Edit profile after registration | Profile updated successfully | OK | — |
| 3 | Change profile photo via gallery | Profile photo updated | OK | — |

### Negative Cases — Register

| No | Test Case | Expected Result | Status |
|---|---|---|---|
| 1 | Tap "Selesai" without filling all required fields | "Selesai" button disabled | OK |
| 2 | Enter username already registered in Ayolari | "Selesai" button disabled; error message shown for duplicate username | OK |
| 3 | Tap "Selesai" with some fields still empty | "Selesai" button disabled | OK |
| 4 | Enter height/weight with decimal format | Decimal input rejected; only integer allowed | OK |
| 5 | Enter unreasonable height/weight values | "Selesai" disabled; error message shown for out-of-range values | OK |
| 6 | Enter invalid birth year (outside 7–80 years range) | Input rejected; valid year range enforced | OK |
| 7 | Tap back button during registration | User directed back to Onboarding page | OK |

---

## Module A3: Running Record Activity

| No | Test Case | Expected Result | Status | Note |
|---|---|---|---|---|
| 1 | Start running record | Timer starts; distance, pace, and calorie tracking begins | OK | — |
| 2 | Pause and resume running record | Activity paused and resumed correctly; data preserved | OK | — |
| 3 | Stop and save running record | Activity saved to history with correct duration, distance, pace, and calories | OK | — |
| 4 | Running record accuracy — Duration | Duration accuracy within 0–30 second margin vs Garmin Watch reference | OK | Dependent on how quickly user ends the record |
| 5 | Running record accuracy — Distance | Distance accuracy within 0–0.03 km per 500m vs Garmin Watch reference | OK | ✅ Passed |
| 6 | Running record accuracy — Pace | Pace accuracy within avg 15 sec/km per 500m vs Garmin Watch reference | OK | ✅ Passed |
| 7 | Running record accuracy — Calories | Ayolari calorie reading consistently higher (~+16 kcal / +48%) vs Garmin Watch | OK with Note | 📝 Calorie calculation needs further tuning |

---

## Module A4: Smartwatch Sync

**Sync Accuracy Summary:**

| Smartwatch | Health App | Android Outdoor | Android Indoor | iOS Outdoor | iOS Indoor | Status | Note |
|---|---|---|---|---|---|---|---|
| Samsung Galaxy Watch 4 | Samsung Health | ✅ OK | ✅ OK | ❌ | — | OK | Wear OS not supported by Apple Health |
| Garmin Venu SQ | Garmin Connect | ✅ OK | ✅ OK | ✅ OK | ✅ OK | OK | Full cross-platform support |
| Huawei Watch GT 3 | Huawei Health | ✅ OK | ✅ OK | ✅ OK | ✅ OK | OK | Full cross-platform support |
| Oppo Watch FREE | OHealth | ✅ OK | ✅ OK | ❌ | — | OK | OHealth only syncs steps; no full workout sync to Apple Health |
| Amazfit Active | Zepp | ✅ OK | ✅ OK | ✅ OK | ✅ OK | OK | Full cross-platform support |
| Apple Watch (iWatch) | Apple Health | ❌ | — | ✅ OK | ✅ OK | OK | iWatch not supported by Google Health Connect |
| Xiaomi Watch Active 5 | Mi Fitness | ✅ OK | ❌ | ✅ OK | ❌ | OK | Indoor treadmill data not sent by Mi Fitness to Health Connect / Apple Health |
| Xiaomi Watch Pro 2 | Mi Fitness | ✅ OK | ✅ OK | ❌ | — | OK | Uses Wear OS; not supported by Apple Health |

**Sync Test Cases:**

| No | Test Case | Expected Result | Status |
|---|---|---|---|
| 1 | Sync completed outdoor run from Garmin to Ayolari | Duration, distance, pace, avg heart rate synced correctly | OK |
| 2 | Sync completed indoor (treadmill) run from Garmin to Ayolari | All data synced correctly | OK |
| 3 | Sync from Samsung Galaxy Watch 4 — Android | All workout data synced | OK |
| 4 | Sync from Samsung Galaxy Watch 4 — iOS | Sync not available (Wear OS incompatibility with Apple Health) | OK |
| 5 | Re-test sync after connection interruption | Data synced successfully on retry | OK |
| 6 | Verify synced data matches source health app data | Synced values (duration, distance, pace, heart rate) match source data within acceptable margin | OK |

---

## Module A5: Challenge & Reward

| No | Test Case | Expected Result | Status |
|---|---|---|---|
| 1 | View active challenges list | All active challenges displayed with correct details | OK |
| 2 | Join a running challenge | User successfully enrolled in challenge | OK |
| 3 | Complete challenge target | Challenge completed; reward claim option appears | OK |
| 4 | Claim reward | Reward claimed successfully; stock decremented in CMS | OK |
| 5 | View challenge leaderboard | Leaderboard displayed with correct user rankings | OK |

---

---

# PART 2 — MINIAPP V-NSP (VIDEO NADA SAMBUNG PRIBADI)

**Version Tested:** Production — Internal DummyApp WebView  
**Testing Date:** July 21–24, 2025  
**About:** V-NSP replaces the standard ringtone with a personalized video shown to the caller while waiting for the call to be answered. Currently supports data-based calls (WhatsApp). Deployed within MyTelkomsel ecosystem.

---

## Device Matrix — V-NSP

| Device | OS | Tester |
|---|---|---|
| Samsung Galaxy A23 | Android 14 | Olsen |
| POCO M3 | Android 13 | Dhafin |
| OPPO Reno8 T | Android 15 | Resta |
| Vivo T1 | Android 14 | Resta |
| ITEL RS4 | Android 14 | Dhafin |
| Techno Spark 30C | Android 14 | Marcel |
| Infinix Hot 50i | Android 14 | Dhafin |

---

## Module V1: Permission Page (DummyApp)

| No | Test Case | Expected Result | Status | Note |
|---|---|---|---|---|
| 1 | Open DummyApp V-NSP | Login page displayed | OK | — |
| 2 | Open DummyApp and tap "Lanjutkan" | Permission setup page displayed | OK | — |
| 3 | Enable all permissions — Samsung A23 (Android 14) | User enters MyTelkomsel landing page; startforeground service running | OK | After granting AutoStart Background + Notification, user must tap screen once to activate input fields |
| 5 | Enable all permissions — POCO M3 (Android 13) | User enters MyTelkomsel landing page; startforeground running | OK | AutoStart Background + Battery access needed for optimal V-NSP experience |
| 6 | Enable all permissions — OPPO Reno8 T (Android 15) | User enters MyTelkomsel landing page; startforeground running | OK | Battery access permission sufficient for Android 15 |

### Negative Cases — Permission Page

| No | Test Case | Expected Result | Status |
|---|---|---|---|
| 1 | Tap "Lewati" (skip) on permission page | MyTelkomsel landing page opens but startforeground does NOT run | OK |
| 2 | Skip first bottom sheet permission | startforeground does NOT run | OK |
| 3 | Skip overlay permission but grant notification | startforeground does NOT run | OK |
| 4 | Skip notification permission | startforeground does NOT run | OK |
| 5 | Skip AutoStart Background & battery optimize (Chinese OEM devices) | startforeground runs normally — these are optional permissions | OK |
| 6 | Multi-language on Permission Page — change to English | All permission pages displayed in English | OK |

---

## Module V2: Onboarding V-NSP

| No | Test Case | Expected Result | Status | Note |
|---|---|---|---|---|
| 1 | Enter correct MSISDN + custparam + custtype | User successfully enters V-NSP Onboarding page | OK | — |
| 2 | View Terms & Conditions V-NSP | T&C page opens | OK | — |
| 3 | Change device language (Indonesian → English) | Multilanguage active; all onboarding text in English | OK | — |

### Negative Cases — Onboarding

| No | Test Case | Expected Result | Status |
|---|---|---|---|
| 1 | Enter onboarding without MSISDN and custparam | Cannot enter V-NSP onboarding | OK |
| 2 | Enter MSISDN with incorrect format | Cannot enter V-NSP onboarding | OK |
| 3 | Enter custparam only, no MSISDN | Cannot enter V-NSP onboarding | OK |
| 4 | Enter MSISDN only, no custparam | Enters onboarding page but cannot reach landing page | OK |
| 5 | Use pre-production custparam in production environment | Enters onboarding but cannot reach landing page | OK |
| 6 | Use custparam belonging to different MSISDN | Enters onboarding but cannot reach landing page | OK |

---

## Module V3: Koleksi Video (Video Collection)

| No | Test Case | Expected Result | Status | Note |
|---|---|---|---|---|
| 1 | View all video collection | New page opens with full list of user's V-NSP video collection | OK | "Lihat Semua" button appears only when user has ≥5 videos |
| 2 | Open video from collection | V-NSP content detail page opens | OK | — |
| 3 | Deactivate active video toggle → confirm "Nonaktifkan" | Toggle switches to inactive; video playback status = inactive | OK | — |
| 4 | Activate inactive video toggle → confirm "Ya, Aktifkan" | Toggle switches to active; video playback status = active | OK | — |

---

## Module V4: Core V-NSP Feature — Video Ringtone During Call

| No | Test Case | Expected Result | Status | Note |
|---|---|---|---|---|
| 1 | Caller with active V-NSP calls recipient via WhatsApp | V-NSP video plays on caller's side while waiting for answer | OK | — |
| 2 | V-NSP video displays correctly across all 7 test devices | Video renders without visual artifacts on all devices | OK | — |
| 3 | V-NSP displays during slow network (throttled connection) | Video loads with graceful buffering; no crash | OK | — |
| 4 | Deactivate V-NSP then make WhatsApp call | Standard ringtone plays; no V-NSP video displayed | OK | — |

---

> **Note:** DummyApp was an internal test harness used by PT INA 17 to validate V-NSP behavior before deployment into the production MyTelkomsel environment. All internal credentials, custparam tokens, and MSISDN identifiers have been removed. All test cases are based on real QA execution.
