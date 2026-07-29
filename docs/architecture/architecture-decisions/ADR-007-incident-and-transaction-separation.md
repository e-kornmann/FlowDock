# ADR-007 — Separate Incidents from Financial Transactions

**Date:** 2026-07-29  
**Status:** Accepted

---

## Context

FlowDock needs to handle operational events that happen during rentals.

Examples:

- A customer runs out of battery.
- A driver needs to pick up a stranded customer.
- A customer returns equipment late.
- Equipment is damaged.
- A customer orders additional drinks at a rental location.

Some of these events may result in additional costs or payments.

An operational event and a financial consequence are related, but they represent different concepts.

For example:

A customer runs out of battery.

Operational event:
- Driver performs a pickup.

Financial consequence:
- Customer pays a pickup fee.

These should not be stored as the same concept.

---

## Decision

FlowDock will separate operational incidents from financial transactions.

An Incident represents something that happened during operations.

A Transaction represents a financial event.

Incidents may result in transactions, but not every incident requires a financial transaction.

---

## Rationale

Separating these concepts keeps the domain model clear.

Examples:

### Incident

"Customer required assistance because the battery was empty."

Information:

- What happened?
- When did it happen?
- Who handled it?
- Which asset was involved?
- What action was taken?

---

### Transaction

"Customer was charged €60 for assistance."

Information:

- Amount
- Reason
- Payment status
- Related reservation

---

This separation also allows future expansion.

Examples:

- A battery pickup may be free as a goodwill action.
- A damage incident may require inspection before charging.
- A late return may automatically create a fee.

---

## Consequences

### Positive

- Clear separation between operational and financial concepts.
- Easier reporting and analytics.
- Better audit history.
- Future pricing rules can evolve without changing incident handling.
- Business rules remain easier to understand.

### Negative

- More domain objects to manage.
- Relationships between incidents and transactions need to be maintained.
- Additional implementation complexity.

---

## Alternatives Considered

### Option A

Store incidents directly as transactions.

Why not?

Not every operational event has a financial consequence.

This would mix operational history with financial records.

---

### Option B

Store all additional actions as "extra charges".

Why not?

This loses important context.

A pickup, damage report, or late return is more than just a price adjustment.

---

## Related Concepts

- Incident
- Transaction
- Reservation
- Asset
- Driver