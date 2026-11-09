# ADR-006 — Product Reservations and Asset Allocation

**Date:** 2026-07-28
**Status:** Accepted

---

## Context

FlowDock manages rental products and physical assets.

A product represents something a customer can reserve, for example:

* Electric Catamaran
* SUP without motor
* SUP with motor
* Drinks
* Food packages

An asset represents a specific physical item owned by FlowDock, for example:

* Catamaran #001
* Catamaran #002
* SUP #015

Customers are interested in reserving a product, not a specific physical asset.

The system must also support operational activities such as:

* Maintenance.
* Asset availability tracking.
* Moving assets between hubs and rental locations.
* Replacing unavailable assets.
* Preparing equipment for upcoming reservations.

A reservation describes what the customer needs, while operations determines how that request is fulfilled.

---

## Decision

Reservations will be made for products rather than specific physical assets.

Physical assets are allocated later during the operational process through Allocations.

An Allocation represents the assignment of one physical asset to a reservation line. A reservation line receives one allocation per asset.

Only products that require physical equipment receive allocations.

Consumable products, such as drinks or food packages, are fulfilled through stock availability rather than asset allocation.

Stock tracking for consumable products is deliberately deferred. This is not an oversight — it is out of scope for the first implementation. Consumable products are not allocated or availability-checked until this is decided.

---

## Rationale

Separating products from assets reflects how rental businesses operate.

A customer does not care which specific catamaran they receive. They care that a suitable product is available at the requested rental location and time.

Separating reservation and allocation provides flexibility for operations:

* Assets can be replaced when maintenance is required.
* Equipment can be redistributed between locations.
* Reservations do not need to change when physical assets change.
* Operations can review and adjust allocations before the rental begins.

---

## Consequences

### Positive

* More flexible reservation process.
* Clear separation between customer needs and operational processes.
* Easier maintenance handling.
* Better support for fleet management.
* Supports future automated allocation suggestions.

### Negative

* Requires an additional allocation process.
* Asset assignment logic becomes more complex.
* Availability calculations require additional business rules.
* The system must manage allocation status and lifecycle.

---

## Alternatives Considered

### Reserve specific physical assets

Advantages:

* Simple implementation.
* Direct relationship between reservation and equipment.

Reason not chosen:

Customers reserve a product, not a specific asset. Reserving specific assets creates unnecessary restrictions and makes operational changes harder.

---

### Treat products and assets as the same concept

Advantages:

* Simpler database model.
* Less initial development.

Reason not chosen:

The concepts have different meanings. Products represent what FlowDock offers to customers, while assets represent individually tracked physical equipment.

---

### Allocate assets immediately when creating a reservation

Advantages:

* Reservation availability is directly linked to physical assets.
* Simpler operational overview.

Reason not chosen:

This couples customer reservations too closely to operational decisions. Assets may change due to maintenance, location changes, or operational planning.
