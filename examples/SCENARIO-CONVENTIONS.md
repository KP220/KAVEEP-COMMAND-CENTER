# KAVEEP Scenario Conventions

Version: 1.0
Status: Foundation
Repository: KAVEEP-COMMAND-CENTER

---

# Purpose

This document defines the conventions for all example scenarios in the KAVEEP Command Center repository.

Scenario examples serve as:

* Documentation
* Integration examples
* Test fixtures
* Regression tests
* Codex implementation references

---

# Scenario Folder Naming

Use the following naming pattern:

```text
examples/scenario-XXX-short-description/
```

Examples:

```text
examples/scenario-001-kcp-verification/
examples/scenario-002-insufficient-evidence/
examples/scenario-003-conflicting-evidence/
examples/scenario-004-policy-block/
examples/scenario-005-human-approval-required/
```

---

# Required Files

Every scenario should contain:

```text
README.md
event.example.json
audit.example.json
kcp-session.example.json
```

Evidence:

```text
evidence.example.json
```

or

```text
evidence-a.example.json
evidence-b.example.json
evidence-c.example.json
evidence-d.example.json
```

Knowledge:

```text
knowledge.example.json
```

Only include this file when the KCP result is **verified**.

---

# ID Convention

Canonical format:

```text
<entity>_s<scenario-number>_<sequence>
```

Examples:

```text
evidence_s001_0001
kcp_s001_0001
knowledge_s001_0001
event_s001_0001
audit_s001_0001
```

Multiple evidence example:

```text
evidence_s003_a
evidence_s003_b
evidence_s003_c
evidence_s003_d
```

---

# Metadata Convention

Each example JSON should contain:

```json
{
  "metadata": {
    "scenario": "scenario-XXX-short-description",
    "schemaVersion": "1.0.0"
  }
}
```

Optional fields:

```json
{
  "expectedResult": "verified",
  "knowledgePublished": true
}
```

or

```json
{
  "expectedResult": "unverified",
  "knowledgePublished": false
}
```

---

# Verification Outcomes

Only these values should be used:

* verified
* unverified
* rejected
* deprecated
* superseded

---

# Core KCP Rules

Insufficient evidence:

```text
UNVERIFIED
```

Conflicting evidence:

```text
UNVERIFIED
```

Policy violation:

```text
BLOCKED
```

Human approval required:

```text
PENDING_APPROVAL
```

Knowledge is published only after successful KCP verification.

---

# Traceability

Successful verification:

```text
Evidence
    │
    ▼
KCP Session
    │
    ▼
Knowledge
    │
    ▼
Event
    │
    ▼
Audit
```

Unverified result:

```text
Evidence
    │
    ▼
KCP Session
    │
    ▼
Event
    │
    ▼
Audit
```

No Knowledge is published.

---

# Audit Requirements

Every scenario must include:

* actor
* target
* event reference
* evidence references
* policy references
* verification summary
* timestamps

---

# Event Requirements

Every event should include:

* correlationId
* relatedEntityId
* relatedEntityType
* auditRef

---

# Acceptance Criteria

A scenario is considered valid when:

* Every JSON validates against its schema.
* IDs follow the canonical naming convention.
* All cross references are valid.
* Event and Audit preserve traceability.
* Knowledge exists only for verified scenarios.
* The scenario demonstrates exactly one governance rule.

---

# Current Official Scenario Library

| Scenario     | Result                | Knowledge     |
| ------------ | --------------------- | ------------- |
| Scenario-001 | Verified              | Published     |
| Scenario-002 | Unverified            | Not Published |
| Scenario-003 | Unverified (Conflict) | Not Published |
| Scenario-004 | Policy Block          | Not Published |
| Scenario-005 | Human Approval        | Pending       |
