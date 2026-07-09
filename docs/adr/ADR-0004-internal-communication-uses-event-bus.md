# ADR-0004

# Internal Communication Uses Event Bus

Status

Accepted

Date

2026

Version

1.0

---

# Context

The KAVEEP ecosystem consists of numerous independent modules, agents, plugins, workflows, services, and future extensions.

As the ecosystem grows, direct communication between modules increases architectural coupling, making maintenance, testing, deployment, scalability, and future evolution increasingly difficult.

A communication model is required that enables loose coupling while preserving governance, observability, and extensibility.

---

# Decision

The Event Bus is designated as the official internal communication mechanism of the KAVEEP ecosystem.

Internal modules shall communicate through events by default.

Direct module-to-module communication is prohibited unless explicitly approved by architecture policy.

---

# Motivation

An event-driven architecture enables

• Loose Coupling

• Independent Development

• Plugin Extensibility

• Better Observability

• Replay

• Simulation

• Auditability

• Horizontal Scalability

---

# Communication Model

Default communication

Publisher

↓

Event Bus

↓

Subscribers

Publishers never know subscribers.

Subscribers never control publishers.

---

# Event Principles

Every important operation shall generate an event.

Events are

Immutable

Versioned

Observable

Traceable

Auditable

Replayable

Events represent facts.

Events do not represent commands.

---

# Event Categories

Supported categories include

Mission Events

Goal Events

Workflow Events

Task Events

Agent Events

Knowledge Events

Policy Events

Security Events

KCP Events

Audit Events

Marketplace Events

Plugin Events

API Events

Notification Events

Monitoring Events

Future Event Types

---

# Event Ownership

Each event shall define

Publisher

Timestamp

Correlation ID

Event Type

Entity

Version

Security Classification

Payload Reference

Every event has exactly one publisher.

An event may have multiple subscribers.

---

# Delivery Principles

Communication shall support

Broadcast

Topic Subscription

Priority Routing

Delayed Delivery

Scheduled Delivery

Replay

Dead Letter Queue

Filtered Delivery

Delivery technology remains implementation-independent.

---

# Exceptions

Direct communication is permitted only when

Performance requirements demand synchronous interaction.

Strong consistency cannot be achieved through asynchronous events.

Official architecture explicitly defines a synchronous interface.

Every exception requires an approved ADR.

---

# Relationship with API Gateway

The Event Bus governs internal communication.

The API Gateway governs external communication.

Internal communication shall never use external APIs directly.

---

# Relationship with Plugin System

Plugins publish events.

Plugins subscribe to events.

Plugins shall never directly manipulate Core services.

---

# Relationship with Audit

Every published event shall generate an immutable audit record.

Audit preserves

Publisher

Subscribers

Processing Result

Correlation

Delivery Status

Replay History

---

# Relationship with Monitoring

Monitoring observes

Event Rate

Subscriber Health

Queue Health

Latency

Failures

Dead Letter Queue

Replay Statistics

Monitoring never modifies event execution.

---

# Alternatives Considered

Alternative 1

Direct Service Calls

Rejected.

Reason

Creates tight coupling between modules.

---

Alternative 2

Shared Database Communication

Rejected.

Reason

Creates hidden dependencies and weak governance.

---

Alternative 3

Fully Synchronous Architecture

Rejected.

Reason

Reduces resilience and scalability.

---

# Consequences

Positive

• Loose Coupling

• Better Scalability

• Easier Testing

• Better Replay

• Better Monitoring

• Easier Plugin Development

• Better Auditability

• Independent Module Evolution

Negative

• Eventual consistency must be managed.

• Event versioning becomes important.

• Replay infrastructure is required.

---

# Architectural Rules

The following rules are mandatory.

Modules publish events.

Modules subscribe to events.

Modules remain independent.

Events remain immutable.

Events remain versioned.

Events remain auditable.

Events remain replayable.

Events shall never bypass Policy.

Events shall never bypass Security.

---

# Related Specifications

SPEC-018 Event Bus

SPEC-017 API Gateway

SPEC-014 Plugin System

SPEC-010 Audit Center

SPEC-019 Ecosystem Monitoring

ARCHITECTURE.md

---

# Related ADRs

ADR-0001

ADR-0002

ADR-0003

---

# Invariants

Unless superseded by a future ADR

• Event Bus remains the default communication mechanism.

• Internal communication remains event-driven.

• Events remain immutable.

• Publishers remain independent from subscribers.

• Every event remains observable.

• Every event remains auditable.

• Every event remains replayable.

---

# Approval

Approved by

KAVEEP Architecture

Version

1.0
