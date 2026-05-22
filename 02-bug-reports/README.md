# 02 — Bug Reports

Professional defect documentation from real QA work at PT Indonesia Satu Tujuh, covering 7 distinct digital products across mobile, web CMS, and Miniapp platforms.

---

## Projects Covered

| Project | Platform | Bug Report Examples |
|---|---|---|
| **Mvicall** | Android & iOS | Gallery video upload failure, permission edge cases |
| **Milov** | Android & iOS | Chat non-functional, API-level scan sync issue, coin deduction bug |
| **Pantura** | Android | Campaign content not updated, banner issues |
| **CMS Digipac (DPA)** | Web | Form data cleared on back navigation |
| **Miniapp Ayolari** | Android & iOS (MyTelkomsel) | iOS Privacy Policy deeplink exit, calorie accuracy deviation |
| **Miniapp V-NSP** | Android (MyTelkomsel) | startforeground behavior per permission state |
| **API — Milov** | Backend / Postman | Data sync mismatch between API response and UI state |

---

## Bug Documentation Standards

Every bug report includes:

| Field | Standard |
|---|---|
| **Title** | Action + Component + Condition (precise, searchable) |
| **Severity** | Critical / High / Medium / Low — based on user impact |
| **Priority** | High / Medium / Low — based on release urgency |
| **Type** | Functional / UI/UX / Performance / Content / Security / Regression |
| **Environment** | App version, device model, OS version, network condition |
| **Steps to Reproduce** | Numbered, precise, executable by any team member |
| **Actual vs Expected** | Always both — never "it doesn't work" |
| **Evidence** | Screenshot, screen recording, or Logcat / Charles Proxy log |
| **Platform Note** | Android vs iOS behavior differences explicitly documented |

---

## Severity & Priority Matrix

| | High Priority | Low Priority |
|---|---|---|
| **High Severity** | Fix immediately — blocks release | Fix in current sprint |
| **Low Severity** | Fix before release if time allows | Fix in backlog |

**Special case — OK With Note:**  
Some bugs were accepted with documented workarounds due to deadline constraints. These are tracked with "OK With Note" status and a clear description of the workaround and recommended permanent fix.

---

## Bug Status Workflow

```
Open → In Progress → Fixed → Re-test → Verified → Closed
                                    ↘ Fail → Back to In Progress
                         ↘ Rejected (with reasoning)
                         ↘ OK With Note (workaround documented)
```

---

## Files in This Folder

| File | Contents |
|---|---|
| [`BUG-TEMPLATE.md`](./BUG-TEMPLATE.md) | Standard template used for all bug reports across all projects |
| [`sample-bug-reports.md`](./sample-bug-reports.md) | 7 real-scenario bug reports spanning mobile apps, CMS, Miniapp, and API testing |

---

## Tools Used for Bug Evidence

| Tool | Purpose |
|---|---|
| **Android Studio Logcat** | Crash logs, runtime errors, stack traces — attached to all crash/freeze bugs |
| **Charles Proxy** | Network traffic logs — used to confirm API call behavior independent of UI |
| **Postman** | API response inspection — verifying data state vs UI state discrepancies |
| **Screen Recording** | Device-level recording — attached to intermittent or multi-step bugs |
| **ClickUp** | Primary defect tracking system used at PT INA 17 |

---

> All bug reports are based on real defects found during professional QA work at PT Indonesia Satu Tujuh. Business-sensitive data, internal URLs, credentials, and personally identifiable information have been removed or anonymized.
