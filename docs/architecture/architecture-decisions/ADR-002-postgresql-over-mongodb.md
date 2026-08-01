# ADR-002 — Choose PostgreSQL over MongoDB

**Date:** 2026-07-28
**Status:** Accepted

---
## Context

FlowDock is a reservation and fleet management platform.

The domain contains many related entities, including:

- Customers
- Reservations
- Participants
- Products
- Physical assets
- Hubs
- Rental locations
- Drivers
- Incidents
- Transactions

The system needs to maintain relationships between assets, hubs, rental locations and reservations.

For example:

- A product represents something a customer can rent.
- A physical asset represents a specific item owned by FlowDock.
- An asset belongs to a hub.
- A rental location receives assets from a hub.
- A reservation is made for a specific rental location.
- A driver performs transport between locations.

Many business operations require strong consistency. For example:

- A reservation should not be created if no assets are available.
- Transactions and reservation updates should remain synchronized.
- Operational incidents may result in financial transactions.
- Assets may move between hubs and rental locations, requiring reliable tracking of state changes over time.

## Decision

PostgreSQL will be used as the primary database for FlowDock.

---

## Rationale

A relational database models the FlowDock domain naturally.

PostgreSQL provides:

- Strong ACID transactions.
- Excellent support for relationships.
- Foreign key constraints.
- Mature indexing and query capabilities.
- Reliability for reservation and inventory systems.
- Broad industry adoption.

Because the domain is highly relational, PostgreSQL reduces the amount of application logic needed to maintain data consistency.

---

## Consequences

### Positive

- Strong data consistency.
- Clear modelling of business relationships.
- Better fit for reservation workflows.
- Easier reporting and analytics.
- Widely used in production environments.

### Negative

- Requires schema migrations.
- Less flexible for rapidly changing document structures.
- More upfront database design.

---

## Alternatives Considered

### MongoDB

Advantages

- Flexible document model.
- Rapid prototyping.
- Easy to store nested data.

Reason not chosen

FlowDock contains many interconnected entities and transactional business rules. Modelling these relationships in MongoDB would increase application complexity and make consistency harder to guarantee.

### SQLite

Advantages

- Extremely simple setup.
- Excellent for prototypes.
- No database server required.

Reason not chosen

SQLite is ideal for small local applications, but FlowDock is designed as a multi-user platform that will later explore Docker, CI/CD and Kubernetes. PostgreSQL better represents a production environment.