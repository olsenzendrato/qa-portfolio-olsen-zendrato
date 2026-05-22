# Bug Report Template

> Copy this template for every new bug report. Fill all fields completely before submitting.

---

## Bug ID: BUG-[YEAR]-[NUMBER]

**Title:** [Action] + [Component] + [Condition]  
*Examples:*  
*"Video upload from gallery fails — video cannot be edited or uploaded"*  
*"App crashes when user double-taps Confirm Payment during slow network"*  
*"Privacy Policy deeplink exits Miniapp on iOS — no return path available"*

---

### Classification

| Field | Value |
|---|---|
| **Severity** | 🔴 Critical / 🟠 High / 🟡 Medium / 🟢 Low |
| **Priority** | High / Medium / Low |
| **Type** | Functional / UI/UX / Performance / Content / Security / Regression / Integration |
| **Status** | Open / In Progress / Fixed / Verified / Closed / OK With Note |
| **Reported By** | Olsen Yeremia Zendrato |
| **Reported Date** | YYYY-MM-DD |
| **Assigned To** | [Developer Name / PIC] |

---

### Environment

| Field | Value |
|---|---|
| **Application** | [App Name & Version, e.g., Mvicall v2.0.86 / Ayolari v9.2.0] |
| **Platform** | Android / iOS / Web |
| **Device** | [Model, e.g., Vivo T1 Pro 5G / iPhone 11 Pro Max / Samsung Galaxy A23] |
| **OS Version** | [e.g., Android 13 / iOS 16 / Android 14] |
| **Network** | WiFi / 4G LTE / Throttled 3G / No Connection |
| **Test Environment** | Staging / Production / Internal DummyApp |
| **Build Version** | [e.g., 2.0.86 / 9.2.0-1006907623] |

---

### Description

**Summary:**  
[One or two sentences describing what the bug is, where it occurs, and its impact on the user or business.]

---

### Steps to Reproduce

1. [First action — be specific about the screen and element]
2. [Second action]
3. [Third action]
4. [Continue as needed...]

**Reproducibility Rate:** Always / Intermittent (X/10 attempts) / Rare

---

### Results

**Actual Result:**  
[Exactly what happens — include error messages verbatim. Be specific: "Button remains disabled" not "it doesn't work".]

**Expected Result:**  
[What should happen according to BRD, Figma design, or standard UX behavior.]

---

### Evidence

| Type | File / Description |
|---|---|
| Screenshot | [filename or description] |
| Screen Recording | [filename] |
| Logcat / Android Studio Log | [log snippet or filename] |
| Network Log (Charles Proxy / Fiddler) | [filename or description] |
| API Response (Postman) | [relevant response snippet] |

---

### Additional Context

*Fill any relevant context:*
- Does this only occur on specific devices or OS versions?
- Only in portrait / landscape mode?
- Only with specific permission states?
- Related to a recent code change or hotfix?
- Platform-specific (Android behaves differently from iOS)?
- Linked ticket ID in Jira / ClickUp: [ID]

---

### Fix Verification

| Field | Value |
|---|---|
| **Fixed in Version** | v[x.x.x] |
| **Fix Verification Date** | YYYY-MM-DD |
| **Verified By** | Olsen Yeremia Zendrato |
| **Verification Result** | Pass / Fail |
| **Regression Check** | Pass / Fail |

---

## Severity & Priority Reference

| Severity | Definition | Example |
|---|---|---|
| 🔴 Critical | System crash, data loss, security breach, core feature completely broken | App crashes on launch; payment double-charged |
| 🟠 High | Major feature broken, no workaround, many users affected | Upload from gallery fails; chat non-functional |
| 🟡 Medium | Feature partially broken, workaround exists | Horoscope loading indefinitely; wrong banner displayed |
| 🟢 Low | Minor visual/cosmetic issue, minimal user impact | Typo in label; minor alignment issue |

| Priority | Definition |
|---|---|
| High | Must fix before release |
| Medium | Should fix in current sprint |
| Low | Fix when capacity allows |

---

> Based on defect management practices used at PT Indonesia Satu Tujuh across Mvicall, Milov, Pantura, CMS Digipac, CMS Ayolari, Miniapp Ayolari, and V-NSP projects.
