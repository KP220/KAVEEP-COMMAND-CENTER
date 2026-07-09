# Scenario Template — KAVEEP Example Coverage

## Purpose

This template defines the standard structure for all KAVEEP example scenarios.

Each scenario should demonstrate one clear KAVEEP behavior, rule, or governance outcome.

---

## Scenario Overview

Describe what happens in this scenario.

Explain:

* What evidence exists
* What KCP evaluates
* Whether Knowledge is published
* What Event is created
* What Audit records

---

## Expected Outcome

| Item                | Expected Result                                                                  |
| ------------------- | -------------------------------------------------------------------------------- |
| Evidence            | Replace with expected state                                                      |
| KCP Session         | Replace with expected state                                                      |
| Verification Result | Replace with `verified`, `unverified`, `rejected`, `deprecated`, or `superseded` |
| Knowledge Published | Yes / No                                                                         |
| Event Created       | Yes / No                                                                         |
| Audit Created       | Yes / No                                                                         |

---

## Verification Chain

```text
Evidence
        │
        ▼
KCP Session
        │
        ▼
Verification Result
        │
        ├──────────────► Knowledge, if verified
        ├──────────────► Event
        └──────────────► Audit
```

---

## Files

* `evidence.example.json`
* `kcp-session.example.json`
* `knowledge.example.json` if Knowledge is published
* `event.example.json`
* `audit.example.json`

---

## Rules Being Tested

List the KAVEEP governance rules tested by this scenario.

---

## Acceptance Criteria

This scenario passes when:

* All required files exist.
* All JSON files match their schemas.
* All entity references are internally consistent.
* The scenario outcome matches the intended KAVEEP rule.
* Audit and Event records preserve traceability.
