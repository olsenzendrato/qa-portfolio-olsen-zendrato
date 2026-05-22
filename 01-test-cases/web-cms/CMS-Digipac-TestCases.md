# Test Cases — CMS Digipac (Digital Partner Activation — DPA)

**Project:** CMS Digipac — Digital Partner Activation (DPA)  
**Testing Date:** May 28, 2024  
**Environment:** Staging (staging.digipac.id/tsel/)  
**Testing Type:** Functional, Negative, UI/UX, Role-Based, End-to-End  
**Tester:** Olsen Yeremia Zendrato  

**About:** CMS Digipac (DPA) is a B2B web platform that bridges content provider companies with the MyTelkomsel ecosystem. Through DPA, a partner company registers their digital products — such as games or subscription services — so end users can subscribe via Telkomsel keywords (e.g., "REG BOLA2"), triggering automatic recurring billing and delivering subscription tokens to the product.

---

## Module 1: Partner Account Registration

### 1.1 Company Detail Registration

| No | Test Case | Test Steps | Expected Result | Actual Result | Status | Note |
|---|---|---|---|---|---|---|
| a | Register company detail — all valid fields | 1. Open DPA login page<br>2. Tap "Daftar"<br>3. Fill all company detail fields correctly<br>4. Tap "Lanjut" | User proceeds to Bank Account Detail page | As expected | OK | Back button hidden and browser back disabled per product decision |
| b | Register company detail — invalid inputs | 1. Upload document in non-PDF format<br>2. Upload document >2MB<br>3. Enter random/invalid email<br>4. Tap "Lanjut" | Validation errors shown per field; user cannot proceed | As expected | OK | Tested: non-PDF format, file >2MB, duplicate company name, duplicate email, wrong email format |

### 1.2 Bank Account Detail Registration

| No | Test Case | Test Steps | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|
| c | Fill all bank account fields correctly → tap "Lanjut" | All valid fields | User proceeds to Contact Detail page | As expected | OK |
| d | Leave some/all bank account fields empty → tap "Lanjut" | User cannot proceed; error messages shown per empty field | As expected | OK |

### 1.3 Contact Detail & Submission

| No | Test Case | Test Steps | Expected Result | Actual Result | Status | Note |
|---|---|---|---|---|---|---|
| e | Fill all contact fields + check agreement checkbox → tap "Kirim" | Submission successful; popup shown: "Pengajuan akun sukses, tunggu 2x24 jam via email" | As expected | OK | — |
| f | Fill some fields with wrong format + check checkbox → tap "Kirim" | Submission fails; validation errors shown | As expected | OK | — |
| g | Leave fields empty + do NOT check agreement checkbox → tap "Kirim" | Submission fails; errors shown on empty fields | As expected | OK | — |
| h | Tap back button during Bank Detail or Contact Detail entry | Returns to previous page; data previously entered still present | Data on previous page was cleared on back tap | OK WITH NOTE | Back button disabled per deadline workaround; permanent fix scheduled for next release |
| i | Tap Terms & Conditions or Privacy Policy link during Contact Detail step | Opens T&C or Privacy Policy page | Page opens in new tab; return to Contact Detail tab manually (data retained) | OK WITH NOTE | Opens in new tab to preserve form data |

---

## Module 2: Partner Login

| No | Test Case | Test Steps | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|
| a | Login with valid approved partner credentials | Enter registered email + password → Login | Partner successfully logs in; redirected to Dashboard | As expected | OK |
| b | Login with rejected/invalid credentials | Enter email + wrong password → Login | Login fails; error message shown | As expected | OK |

---

## Module 3: Dashboard

| No | Test Case | Expected Result | Actual Result | Status |
|---|---|---|---|---|
| 1 | Dashboard loads correctly | All widgets displayed: Last Transaction Table, Revenue Chart, Total Successful Transactions Today & This Month, Total Revenue Today & This Month, Trending Products Chart | As expected | OK |
| 2 | Revenue chart reflects correct data | Chart displays accurate revenue data for current period | Data up to date | OK |
| 3 | Total successful transactions (today) | Counter shows correct count of today's successful transactions | As expected | OK |
| 4 | Total successful transactions (this month) | Counter shows correct count of this month's successful transactions | As expected | OK |
| 5 | Total revenue today | Revenue figure correct for today | As expected | OK |
| 6 | Total revenue this month | Revenue figure correct for current month | As expected | OK |
| 7 | Trending products chart | Top trending products displayed and updated daily | As expected | OK |

---

## Module 4: Product Registration (Content Provider Product)

| No | Test Case | Expected Result | Status | Note |
|---|---|---|---|---|
| 1 | Register new product — all required fields filled | Product submitted for review; appears in product list with "Pending" status | OK | — |
| 2 | Register new product — missing required fields | Validation errors shown; product not submitted | OK | — |
| 3 | Upload product assets (logo, banner) — valid format & size | Assets uploaded and previewed correctly | OK | — |
| 4 | Upload product assets — invalid format or oversized | Upload rejected; error message shown | OK | — |
| 5 | Set subscription keyword (e.g., REG BOLA2) | Keyword associated with product; visible in product detail | OK | — |
| 6 | Set subscription price per billing cycle | Price saved; applied on subscription renewal/charging | OK | — |
| 7 | View product detail after submission | All submitted data displayed correctly | OK | — |

---

## Module 5: Transaction & Revenue Reports

| No | Test Case | Expected Result | Status |
|---|---|---|---|
| 1 | View transaction history with date filter | Transactions filtered correctly by selected date range | OK |
| 2 | Export transaction report | Report downloaded in correct format | OK |
| 3 | Transaction status breakdown | Successful, failed, and pending transactions shown accurately | OK |

---

## Cross-Browser Compatibility

| Browser | Test | Expected Result | Status |
|---|---|---|---|
| Chrome (latest) | Full registration + login + dashboard | All features functional; no layout issues | OK |
| Safari (latest) | Full registration + login + dashboard | All features functional; no layout issues | OK |
| Firefox (latest) | Full registration + login + dashboard | All features functional; no layout issues | OK |

---

> **Note:** Testing was conducted on staging environment. Production URLs, internal API endpoints, and actual partner credentials have been removed. All scenarios are based on real UAT execution at PT Indonesia Satu Tujuh.
