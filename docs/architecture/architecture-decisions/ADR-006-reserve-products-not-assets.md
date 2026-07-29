# ADR-006 — Reserve products instead of physical assets

**Date:** 2026-07-28  
**Status:** Accepted

---

## Context


FlowDock manages rental products and physical assets.

A product represents something a customer can rent, for example:

- Electric catamaran
- SUP without motor
- SUP with motor

An asset represents a specific physical item owned by FlowDock, for example:

- Catamaran #001
- Catamaran #002
- SUP #015

Customers are interested in reserving a product type, not a specific physical asset.

The system must also support operational activities such as:

- Maintenance.
- Asset availability tracking.
- Allocation of equipment to rental locations.
- Replacement of unavailable assets.

FlowDock also offers additional items such as food and drinks.

These items are products, but they do not represent physical assets that require individual allocation.

---

## Decision

Reservations will be made for products rather than specific physical assets.

Physical assets will be assigned to reservations during the operational planning process.

---

## Rationale

Separating products from assets reflects how rental businesses operate.

A customer does not care which specific catamaran they receive. They care that a suitable catamaran is available at the requested rental location and time.

This separation provides flexibility for operations:

- Assets can be replaced when maintenance is required.
- Equipment can be redistributed between locations.
- Reservations do not need to change when the physical asset changes.

---

## Consequences

### Positive

- More flexible reservation process.
- Easier maintenance handling.
- Better support for fleet management.
- Clear separation between customer needs and operational processes.

### Negative

- Requires an additional allocation process.
- Asset assignment logic becomes more complex.
- Availability calculations require more business rules.

---

## Alternatives Considered

### Reserve specific physical assets

Advantages:

- Simple implementation.
- Direct relationship between reservation and equipment.

Reason not chosen:

This creates unnecessary restrictions. A customer does not need a specific asset and operational changes become harder to manage.

### Treat products and assets as the same concept

Advantages:

- Simpler database model.
- Less initial development.

Reason not chosen:

The concepts have different meanings. Products represent what is offered to customers, while assets represent physical inventory.