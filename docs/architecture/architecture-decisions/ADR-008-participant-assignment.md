# ADR-008 — Introduce Participant Assignment

**Date:** 2026-08-02
**Status:** Accepted

---

## Context

FlowDock records participants on a reservation, but a reservation can contain multiple reservation lines, each referencing a different product.

Some products have product-specific rules, such as minimum age restrictions:

* SUP without motor: minimum age 10.
* SUP with motor: minimum age 7.

Validating these rules requires knowing which participant is actually using which reservation line. A participant linked only to the reservation as a whole does not carry enough information to know which product-specific rules apply to them.

---

## Decision

FlowDock will introduce a Participant Assignment concept.

A Participant Assignment represents a specific participant using a specific reservation line.

Participants will not be linked to reservation lines directly. The relationship is expressed through this explicit assignment concept instead.

Participant Assignments are created at booking time, together with the reservation.

---

## Rationale

This follows the same modeling pattern already established for Allocation (ADR-006): rather than a direct link between two concepts, an explicit assignment concept records which specific participant belongs to which specific reservation line.

Unlike Allocation, which is deliberately deferred to the operational process, Participant Assignments are known by the customer at the time of booking and can be captured immediately. There is no operational planning step required to determine which participant uses which product.

---

## Consequences

### Positive

* Product-specific rules (such as minimum age) can be validated against the correct reservation line.
* Follows an established, consistent modeling pattern (assignment concepts) rather than introducing a new one.
* Clear separation between "who is on this reservation" (Participant) and "who is using this specific product" (Participant Assignment).

### Negative

* An additional concept to manage and persist.
* Reservation creation must capture participant assignments per line, not just a flat list of participants.

---

## Alternatives Considered

### Link Participant directly to Reservation Line

Advantages:

* Simpler model, one fewer concept.

Reason not chosen:

A direct link does not clearly separate "the participant is part of this reservation" from "the participant is using this specific product." An explicit assignment makes this distinction, and the intent behind it, clear.

### Validate age restrictions against the reservation as a whole

Advantages:

* No additional concept required.

Reason not chosen:

Age restrictions are defined per product. Validating against the reservation as a whole cannot express "this 8-year-old participant is using the SUP without motor," which is exactly the case the rule needs to catch.

---

## Related Concepts

- Participant
- Reservation Line
- Allocation
- Product
