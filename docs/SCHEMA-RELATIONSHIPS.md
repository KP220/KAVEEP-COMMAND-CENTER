# KAVEEP Schema Relationships

Version: 1.0  
Status: Foundation  
Repository: KAVEEP-COMMAND-CENTER  
Classification: Enterprise Data Architecture

---

## Purpose

This document defines the official relationships between shared KAVEEP schemas.

It explains how core entities connect across Mission, Workflow, Task, Agent, Policy, Knowledge, Evidence, KCP Session, Event, and Audit.

---

## Core Rule

Every important entity must be traceable.

```text
Entity
↓
Event
↓
Audit
↓
Policy
↓
Evidence
↓
KCP
↓
Knowledge

Mission
├── goals → Goal
├── workflows → Workflow
├── assignedAgents → Agent
├── requiredPolicies → Policy
├── requiredKnowledge → Knowledge
└── auditRefs → Audit

Workflow
├── missionId → Mission
├── goalId → Goal
├── tasks → Task
├── assignedAgentIds → Agent
├── requiredCapabilities → Capability
├── requiredPolicies → Policy
├── approvalIds → Approval
├── auditRefs → Audit
└── eventRefs → Event

Task
├── missionId → Mission
├── workflowId → Workflow
├── goalId → Goal
├── ownerAgentId → Agent
├── assignedAgentId → Agent
├── requiredCapabilityId → Capability
├── approvalId → Approval
├── dependencies → Task
├── auditRefs → Audit
└── eventRefs → Event

Agent
├── passportId → Passport
├── identityId → Identity
├── capabilities → Capability
└── auditRefs → Audit

Knowledge
├── evidenceRefs → Evidence
├── kcpSessionId → KCP Session
├── requiredPolicies → Policy
├── usedByAgentIds → Agent
├── auditRefs → Audit
└── eventRefs → Event

Evidence
├── knowledgeRefs → Knowledge
├── kcpSessionRefs → KCP Session
├── submittedByAgentId → Agent
├── submittedByUserId → User
├── auditRefs → Audit
└── eventRefs → Event

KCP Session
├── evidenceRefs → Evidence
├── knowledgeRefs → Knowledge
├── policyRefs → Policy
├── missionId → Mission
├── taskId → Task
├── participantAgentIds → Agent
├── auditRefs → Audit
└── eventRefs → Event

Audit
├── target → Any Entity
├── policyRefs → Policy
├── evidenceRefs → Evidence
├── knowledgeRefs → Knowledge
├── agentRefs → Agent
├── eventRefs → Event
├── kcpSessionRef → KCP Session
└── previousAuditRef → Audit

Event
├── relatedEntityId → Any Entity
├── relatedEntityType → Entity Type
├── correlationId → Mission / Workflow / Task / Audit / KCP Chain
└── auditRef → Audit

Knowledge Claim
↓
Evidence Collection
↓
Evidence Review
↓
KCP Session
↓
Independent Agent Evaluation
↓
Conflict Analysis
↓
Consensus Evaluation
↓
Policy Check
↓
Verification Result
↓
Audit Record
↓
Knowledge Publication

Canonical ID Prefixes
Entity	Prefix
Agent	agent_
Approval	approval_
Audit	audit_
Capability	capability_
Event	event_
Evidence	evidence_
Goal	goal_
Identity	identity_
Knowledge	knowledge_
KCP Session	kcp_
Mission	mission_
Passport	passport_
Policy	policy_
Task	task_
User	user_
Workflow	workflow_
Risk Levels

The canonical risk levels are:

low
moderate
high
critical

All schemas that define risk must use these values exactly.

Governance Rules

Execution requires Policy.

Policy requires Audit.

Knowledge requires Evidence.

Verified Knowledge requires KCP.

KCP requires Evidence, Agent Review, Conflict Analysis, and Policy.

High-risk execution requires Human Approval.

Insufficient evidence must result in unverified.

Insufficient evidence must never automatically result in verified.

Insufficient evidence must never automatically result in rejected.

Acceptance Criteria

This relationship model is valid when:

Every major schema can reference Audit.
Knowledge references Evidence and KCP Session.
Evidence links back to Knowledge and KCP Session.
KCP Session references Evidence, Policy, Agents, and Audit.
Events can be correlated with Audit.
Risk levels are consistent across schemas.
Entity IDs follow canonical prefixes.
Insufficient evidence results in unverified.
No important entity exists outside traceability.
