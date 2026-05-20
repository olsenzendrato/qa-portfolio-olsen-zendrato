# 01 — Test Cases

This folder contains structured test case documentation created from real project experience, using industry-standard test design techniques.

## Techniques Used

| Technique | Description |
|---|---|
| **Boundary Value Analysis (BVA)** | Testing at the exact boundary of valid/invalid input ranges |
| **Equivalence Partitioning (EP)** | Grouping inputs into valid and invalid partitions |
| **Use Case Testing** | Tracing end-to-end user journeys (happy path + edge cases) |
| **Exploratory Testing** | Unscripted testing to discover unexpected behavior |
| **Decision Table** | Mapping combinations of inputs to expected outputs |

## Folder Structure

```
01-test-cases/
├── web-cms/
│   ├── CMS-Digipac-TestCases.md
│   └── CMS-Ayolari-TestCases.md
├── mobile-apps/
│   ├── Mvicall-TestCases.md
│   └── Milov-TestCases.md
└── miniapp/
    └── MyTelkomsel-Miniapp-TestCases.md
```

## Test Case Format

All test cases follow this standard format:

| Field | Description |
|---|---|
| **Test ID** | Unique identifier (e.g., TC-CMS-001) |
| **Feature / Module** | The feature being tested |
| **Test Scenario** | What is being validated |
| **Preconditions** | State required before execution |
| **Test Steps** | Step-by-step actions |
| **Test Data** | Input values used |
| **Expected Result** | What should happen |
| **Actual Result** | What actually happened (filled during execution) |
| **Status** | Pass / Fail / Blocked |
| **Technique** | BVA / EP / Use Case / Exploratory |
| **Priority** | High / Medium / Low |

---

> All test cases are simulated/anonymized versions based on real project experience. Confidential business data has been removed.
