# Scenario-002 — Insufficient Evidence

## Purpose

This scenario demonstrates one of the core principles of the KAVEEP Consensus Protocol (KCP):

> **Insufficient evidence must result in `UNVERIFIED`.**

The absence of sufficient evidence is **not** evidence that a claim is false.

Likewise, an unsupported claim must **never** be automatically promoted to `VERIFIED`.

---

# Scenario Overview

Only one weak external reference is available.

No independent corroboration exists.

Three independent reviewer agents evaluate the available evidence.

All reviewers independently conclude that the available evidence is **insufficient for verification**.

The KCP session therefore produces the result:

```text
UNVERIFIED
```

No Knowledge record is published.

---

# Expected Outcome

| Item                | Expected Result |
| ------------------- | --------------- |
| Evidence            | Present         |
| KCP Session         | Completed       |
| Verification Result | `unverified`    |
| Knowledge Published | No              |
| Event Created       | Yes             |
| Audit Created       | Yes             |

---

# Verification Chain

```text
Evidence
        │
        ▼
KCP Session
        │
        ▼
UNVERIFIED
        │
        ├──────────────► Event
        │
        └──────────────► Audit

(No Knowledge Published)
```

---

# Files

* `evidence.example.json`
* `kcp-session.example.json`
* `event.example.json`
* `audit.example.json`

---

# Rules Being Tested

This scenario validates the following KAVEEP governance rules:

* Insufficient evidence must result in `unverified`.
* Absence of evidence is not evidence of absence.
* No Knowledge may be published without successful KCP verification.
* Every KCP session must remain fully traceable through Event and Audit records.
* Independent reviewer convergence is required before knowledge publication.

---

# Acceptance Criteria

This scenario passes when:

* Evidence exists but is insufficient.
* All reviewer agents independently conclude that the claim remains `unverified`.
* The KCP Session result is `unverified`.
* No Knowledge record is created.
* Event and Audit records are successfully generated.
* All entity references remain internally consistent.

---

# Future Extension

Additional independent evidence may be submitted later.

If sufficient independent corroboration becomes available, a new KCP Session should be created.

The original session remains immutable for historical traceability.
