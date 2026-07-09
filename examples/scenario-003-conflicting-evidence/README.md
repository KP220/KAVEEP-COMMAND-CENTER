# Scenario-003 — Conflicting Evidence

## Purpose

This scenario demonstrates how the KAVEEP Consensus Protocol (KCP) handles conflicting evidence.

Unlike Scenario-002, sufficient evidence exists.

However, the available evidence reaches contradictory conclusions.

The KCP Engine must not choose a side automatically.

Instead, it performs conflict analysis.

Because consensus cannot be reached, the final result remains:

```text
UNVERIFIED
```

No Knowledge record is published.

---

# Scenario Overview

Four evidence records are available.

Two support the claim.

Two contradict the claim.

Three independent reviewer agents evaluate every evidence record.

The reviewers agree that the evidence set contains unresolved conflicts.

The claim therefore remains unverified.

---

# Expected Outcome

| Item                | Expected Result |
| ------------------- | --------------- |
| Evidence            | Present         |
| Conflict Analysis   | Performed       |
| Consensus           | Not Reached     |
| Verification Result | `unverified`    |
| Knowledge Published | No              |
| Event Created       | Yes             |
| Audit Created       | Yes             |

---

# Verification Flow

```text
Evidence A ─────┐
Evidence B ─────┤
Evidence C ─────┤
Evidence D ─────┘
        │
        ▼
Conflict Analysis
        │
        ▼
Consensus Not Reached
        │
        ▼
UNVERIFIED
        │
        ├──────────────► Event
        └──────────────► Audit

(No Knowledge Published)
```

---

# Files

* evidence-a.example.json
* evidence-b.example.json
* evidence-c.example.json
* evidence-d.example.json
* kcp-session.example.json
* event.example.json
* audit.example.json

---

# Rules Being Tested

* Conflicting evidence must not automatically produce a verified result.
* Conflicting evidence must not automatically produce a rejected result.
* Consensus requires convergence of independent evidence.
* Conflict analysis must occur before any publication decision.
* No Knowledge may be published while unresolved conflicts remain.
* Every KCP session must remain fully traceable through Event and Audit.

---

# Acceptance Criteria

This scenario passes when:

* Multiple evidence records exist.
* Evidence contains unresolved contradictions.
* Conflict analysis is executed.
* Consensus is not reached.
* Verification result is `unverified`.
* No Knowledge record is published.
* Event and Audit records are created.
* All entity references remain internally consistent.

---

# Future Extension

If additional independent evidence resolves the conflict, a new KCP Session should be created.

The current session remains immutable for historical traceability.
