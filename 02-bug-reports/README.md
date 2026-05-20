# 02 — Bug Reports

This folder contains standardized defect documentation following professional bug reporting practices used in production QA workflows.

## Why Good Bug Reports Matter

A well-written bug report is the QA engineer's primary deliverable. It must give developers everything they need to reproduce, understand, and fix the issue — without any back-and-forth. Poor bug reports slow down the entire development cycle.

## Bug Report Standards Used

| Field | Standard |
|---|---|
| **Title** | Action + Component + Condition (e.g., "App crashes when user double-taps CTA during slow network") |
| **Severity** | Critical / High / Medium / Low |
| **Priority** | High / Medium / Low |
| **Steps to Reproduce** | Numbered, precise, reproducible by any team member |
| **Actual vs Expected** | Always both — never just "it doesn't work" |
| **Environment** | OS version, device model, app version, network condition |
| **Evidence** | Screenshot, screen recording, or Logcat log |

## Severity vs Priority Matrix

| | High Priority | Low Priority |
|---|---|---|
| **High Severity** | Fix immediately — blocks release | Fix in current sprint |
| **Low Severity** | Fix before release if time allows | Fix in backlog |

## Files in This Folder

- [`BUG-TEMPLATE.md`](./BUG-TEMPLATE.md) — Standard template used for all bug reports
- [`sample-bug-reports.md`](./sample-bug-reports.md) — 5 real-scenario bug report examples across different platforms

---

> All bugs are simulated/anonymized versions based on real defects found during professional QA work at PT Indonesia Satu Tujuh.
