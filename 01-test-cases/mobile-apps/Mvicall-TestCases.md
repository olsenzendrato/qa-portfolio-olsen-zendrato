# Test Cases — Mvicall Mobile Application

**Project:** Mvicall  
**Version Tested:** 2.0.86 (Android)  
**Testing Date:** January 31, 2024  
**Platform:** Native Mobile — Android & iOS  
**Testing Type:** Functional, UI/UX, Integration, Regression, Cross-Device  
**Tester:** Olsen Yeremia Zendrato  

**About the App:** Mvicall is a video ringtone application. When User A calls User B via WhatsApp call, the active Mvicall content set by User A will be displayed on User B's screen — replacing the standard ringtone — provided User B has enabled all required Mvicall permissions.

---

## Device Matrix

| Device | OS | Role |
|---|---|---|
| Vivo T1 Pro 5G | Android 13 | Primary tester (Device 1) |
| Realme 9 5G | Android 13 | Secondary Android (Device 2) |
| iPhone X | iOS 16.7 | iOS tester (Device 3) |
| iPhone XI | iOS 16.3 | iOS tester (Device 4) |

---

## Module 1: Welcome Page

| Test ID | Test Case | Preconditions | Test Steps | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| WP_1_1 | Display welcome page on first launch | New user, fresh install | 1. Install Mvicall from Play Store<br>2. Open app for the first time | Welcome page displayed with brief app description; push notification permission popup appears; "Mulai Sekarang" button visible | As expected | OK |

---

## Module 2: Login & Authentication

| Test ID | Test Case | Preconditions | Test Steps | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| LG_1_1 | Login with valid phone number | New user, original number | 1. On login screen, grant phone call permission<br>2. Enter valid phone number<br>3. Accept T&C<br>4. Tap "Lanjut" | System verifies number; OTP field displayed | As expected | OK |
| LG_1_2 | Login with invalid phone number | New user | 1. Enter incorrect phone number<br>2. Accept T&C<br>3. Tap "Lanjut" | System rejects number with error message | As expected | OK |
| LG_2_1 | Enter correct OTP | OTP sent | Enter correct OTP received via SMS | User successfully logged in | As expected | OK |
| LG_2_2 | Enter incorrect OTP | OTP sent | Enter wrong OTP | Login rejected; error message shown | As expected | OK |
| LG_3_1 | Resend OTP | OTP expired | Tap "Kirim Ulang OTP" | New OTP sent; previous OTP invalidated | As expected | OK |

---

## Module 3: Page Friend — Sync Contact

| Test ID | Test Case | Preconditions | Test Steps | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| PF_1_1 | Sync contacts from phone | Logged in, contacts permission granted | Tap sync contacts | Phone contacts synced; Mvicall users in contact list appear as friends | As expected | OK |
| PF_1_2 | View friend list | Contacts synced | Open Friends page | Friends who use Mvicall displayed correctly | As expected | OK |
| PF_2_1 | Send friend request | Logged in | Find user → Tap "Add Friend" | Friend request sent; pending status shown | As expected | OK |
| PF_2_2 | Accept friend request | Friend request received | Open notification → Accept request | Friend added to list | As expected | OK |
| PF_2_3 | Reject friend request | Friend request received | Open notification → Reject request | Request removed; user not added to list | As expected | OK |
| PF_2_4 | Remove friend | Friend in list | Go to friend profile → Remove Friend | Friend removed from list | As expected | OK |

---

## Module 4: Caller — Video Ringtone Core Feature

| Test ID | Test Case | Preconditions | Test Steps | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| UV_1_1 | Caller's Mvicall video displayed on receiver's screen | Device 1 = caller, Device 2 = receiver. Both have Mvicall. Device 2 has all permissions enabled. | Device 1 calls Device 2 via WhatsApp call | Device 1's active Mvicall video content plays on Device 2's incoming call screen instead of standard ringtone | As expected | OK |
| UV_1_2 | Receiver without permissions sees standard ringtone | Device 2 has Mvicall but permissions NOT enabled | Device 1 calls Device 2 via WhatsApp call | Standard ringtone displayed on Device 2; no Mvicall video | As expected | OK |
| UV_1_3 | Caller without active content — receiver sees default | Device 1 has no active Mvicall content set | Device 1 calls Device 2 | Standard ringtone shown on Device 2 | As expected | OK |
| UV_1_4 | Video ringtone plays on iOS receiver | Device 3 (iPhone) is receiver | Device 1 (Android) calls Device 3 via WhatsApp | Mvicall video displayed on iOS incoming call screen | As expected | OK |

---

## Module 5: Caller Video — Video Management

| Test ID | Test Case | Preconditions | Test Steps | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| CV_1_1 | Upload video from camera | Logged in | Profile → Tambah video → Camera → Record → Upload → Save | New video added to profile video list | As expected | OK |
| CV_1_2 | Upload video from gallery | Logged in | Profile → Tambah video → Gallery → Select → Upload → Save | New video added to profile video list | Video from gallery cannot be edited and uploaded | NOT OK |
| CV_1_3 | Set video as default (active) ringtone | Video uploaded | Select video from list → Set As Default → Save | Selected video becomes active Mvicall content shown to callee | As expected | OK |

---

## Module 6: Video Activation (VA) — Permissions

| Test ID | Test Case | Preconditions | Test Steps | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| VA_1_1 | Enable notification permission | Fresh install | Follow permission setup flow → Grant notification | Permission granted; app can send notifications | As expected | OK |
| VA_1_2 | Enable phone call permission | Fresh install | Follow permission setup flow → Grant phone call access | Permission granted; number verification possible | As expected | OK |
| VA_1_3 | Enable overlay permission | Fresh install | Follow permission setup → Grant display over apps | Permission granted; Mvicall video can appear over other apps | As expected | OK |
| VA_1_4 | Enable accessibility service | Fresh install | Follow permission setup → Enable Mvicall in Accessibility | Accessibility service enabled; WhatsApp call interception active | As expected | OK |
| VA_1_5 | Deny all permissions | Fresh install | Deny all permissions during setup | App guides user to enable permissions; core feature unavailable without them | As expected | OK |
| VA_1_6 | Permission revoked mid-use | All permissions previously granted | Revoke overlay permission from Settings → Make call | Mvicall video no longer displayed; app prompts user to re-enable permission | As expected | OK |
| VA_1_7 | Re-enable revoked permission | Permission was revoked | Follow in-app prompt → Re-enable permission in Settings | Feature restored after re-enabling | As expected | OK |

---

## Module 7: Page Profile

| Test ID | Test Case | Test Steps | Expected Result | Actual Result | Status | Note |
|---|---|---|---|---|---|---|
| PS_1_1 | View profile | Open Profile page | All user data displayed correctly | As expected | OK | — |
| PS_1_2 | Change profile photo from camera | Profile → Ubah Profile → Change Photo → Camera → Upload → Save | Profile photo updated | As expected | OK | — |
| PS_1_3 | Change profile photo from gallery | Profile → Ubah Profile → Change Photo → Gallery → Upload → Save | Profile photo updated | As expected | OK | — |
| PS_1_4 | Change display name | Profile → Ubah Profile → Change name → Save | Name saved as entered | As expected | OK | — |

---

## Module 8: Shortcut Menu

| Test ID | Test Case | Expected Result | Actual Result | Status |
|---|---|---|---|---|
| SM_1_1 | All shortcut menu items functional | Each shortcut opens correct destination | As expected | OK |

---

## Module 9: Explore

| Test ID | Test Case | Expected Result | Actual Result | Status | Note |
|---|---|---|---|---|---|
| EX_1_1 | Browse content in Explore | List of Mvicall videos from other users displayed | As expected | OK | — |
| EX_1_2 | Scroll and discover new content | New content loads on scroll | As expected | OK | — |
| EX_1_3 | Report content from Explore | Reported content disappears from Explore feed | As expected | OK | — |
| EX_1_4 | Report profile from Explore | Reported profile disappears from Explore | As expected | OK | — |
| EX_1_5 | Block user from Explore | Blocked profile no longer visible in Explore | As expected | OK | — |

---

## Module 10: Pesta Rewards

| Test ID | Test Case | Expected Result | Actual Result | Status |
|---|---|---|---|---|
| PR_1_1 | View leaderboard | Leaderboard page with rankings displayed | As expected | OK |
| PR_1_2 | View best deals | Best deals page displayed | As expected | OK |
| PR_1_3 | Access redeem page | Redeem page displayed | As expected | OK |

---

## Module 11: Marketplace

| Test ID | Test Case | Expected Result | Actual Result | Status |
|---|---|---|---|---|
| MP_1_1 | Browse marketplace content | Marketplace items displayed correctly | As expected | OK |
| MP_1_2 | Purchase item from marketplace | Purchase flow completes; item added to collection | As expected | OK |

---

## Module 12: Sidebar Menu

| Test ID | Test Case | Expected Result | Actual Result | Status |
|---|---|---|---|---|
| SB_1_1 | Cara Pakai / How to Use | Page with usage instructions displayed | As expected | OK |
| SB_1_2 | Contact Customer Service | Mvicall CS contact information displayed | As expected | OK |
| SB_1_3 | Terms & Conditions | T&C page displayed | As expected | OK |
| SB_1_4 | Privacy Policy | Privacy policy page displayed | As expected | OK |
| SB_1_5 | Logout | User logged out; redirected to login screen | As expected | OK |

---

## Known Bugs Found During Testing

| Bug | Description | Severity | Status |
|---|---|---|---|
| Video upload from gallery fails | Selecting video from gallery cannot be edited and uploaded | High | Reported |
| Horoscope loading issue | Horoscope page loads indefinitely even with stable connection | Medium | Reported |

---

> **Note:** All test data, phone numbers, and device identifiers have been anonymized. Testing was conducted on real physical devices at PT Indonesia Satu Tujuh.
