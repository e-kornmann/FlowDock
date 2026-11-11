# ADR-009 — A product requires one or more asset types

**Date:** 2026-11-11
**Status:** Accepted

---

## Context

[ADR-006](ADR-006-reserve-products-not-assets.md) decided that customers reserve products and that operations allocates physical assets later, one allocation per asset.

Until now, every product implicitly matched one kind of asset: an Electric Catamaran is fulfilled by a catamaran, a SUP with motor by a SUP with a motor on it.

FlowDock has decided to keep its stock flexible at the lowest cost. It buys SUP boards and separate electric motor kits that click into the fin box under a board. Any board can go out with or without a motor.

The same applies to the Electric Catamaran. An assembled catamaran is too large to transport in numbers from the hub to a rental location. FlowDock transports it as parts: two SUP boards, two motor kits and a catamaran kit (frame, crate and mounting material). A driver assembles the catamaran at the rental location.

The domain model cannot express this. A SUP with motor is now two physical things: one board and one motor kit. A catamaran is five. These parts are expensive and can break, so they need to be tracked as assets.

Product availability also depends on this: a product is only available when enough assets that can fulfil it are left.

---

## Decision

FlowDock will introduce the concept **Asset Type**.

Every asset is of exactly one asset type. A product requires one or more asset types, each with a number per unit of the product.

Current products:

| Product | Requires per unit |
| --- | --- |
| Electric Catamaran | 2 SUP boards, 2 motor kits, 1 catamaran kit |
| SUP without motor | 1 SUP board |
| SUP with motor | 1 SUP board, 1 motor kit |
| Consumable products | none, see ADR-006 |

A motor kit is one asset: the motor and its battery are a single unit. A catamaran kit is one asset: the frame, crate and mounting material are a single unit.

All SUP boards use the same fin box, so every motor kit fits every SUP board. Compatibility between assets is not modelled.

An allocation still assigns exactly one asset. A reservation line needs one allocation for every asset its product requires: 2 × SUP with motor needs two SUP board allocations and two motor kit allocations.

A product is available only when every asset type it requires has enough free assets.

---

## Rationale

The model now matches how operations thinks about stock: "we have 12 boards and 6 motor kits", not "we have 6 SUPs with motor".

Tracking motor kits as assets keeps availability correct. Without it, FlowDock could accept more reservations for SUP with motor than there are motor kits.

A broken motor is fixed by swapping the motor kit only. The board, and the reservation, stay the same.

Catamarans can be transported as parts and assembled at the rental location, so more catamarans fit in one transport.

This extends ADR-006 instead of reversing it. Products and assets stay separate concepts, and one allocation is still one asset.

---

## Consequences

### Positive

* Flexible stock at lower cost: one pool of boards serves three products.
* Catamarans are transported as parts, so transport capacity is no longer the limit.
* Motor failures are handled per motor kit, without replacing the board.
* Availability reflects every physical item a product needs.
* New products can combine existing asset types without new kinds of assets.

### Negative

* An additional concept to manage and persist.
* More allocations per reservation line.
* Availability must be checked per required asset type, not per product.
* SUPs and catamarans compete for the same boards and motor kits: every catamaran means two fewer SUPs.
* A driver has to assemble every catamaran at the rental location, which costs time during the setup.
* Purchasing is constrained: a board with a different fin box would force FlowDock to model compatibility between assets.

---

## Alternatives Considered

### Treat the motor kit as an accessory, not an asset

Advantages:

* Simplest model: SUP with motor needs one board.

Reason not chosen:

FlowDock would not know how many motor kits are free, so SUP with motor could be overbooked. A broken motor could not be recorded against a specific asset.

---

### Keep each motor fixed to its own board

Advantages:

* No change to the model: one product, one kind of asset.

Reason not chosen:

It contradicts the business choice. FlowDock would need more boards for the same number of rentals, at higher cost and with less flexibility.

---

### Keep the catamaran as one asset

Advantages:

* No assembly at the rental location.
* Simpler allocation: one asset per catamaran.

Reason not chosen:

Assembled catamarans are too large to transport in numbers, so FlowDock could offer only a few per rental location.

---

### Don't decide yet

Advantages:

* Assets are only implemented in Phase 3, so nothing needs to change now.

Reason not chosen:

The business decision has already been made, and the availability rule depends on it. Leaving it open means the documentation no longer describes how the business works.

---

## Related Concepts

- Product
- Asset
- Asset Type
- Allocation
- Reservation Line
