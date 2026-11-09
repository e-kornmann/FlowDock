# FlowDock Domain Language

## Customer

A person who creates a reservation and is responsible for it.

---

## Participant

A person who uses the rental product but is not necessarily the person who made the reservation.

See [domain-model.md](domain-model.md#participant) for an example, and how a customer can also be a participant.

---

## Reservation

A customer's request to rent one or more products for a specific period and rental location.

---

## Cancellation Reason

Why a reservation was cancelled. It is recorded on the reservation itself, see [domain-model.md](domain-model.md#reservation).

---

## Reservation Line

A single line within a reservation representing one product and its quantity.

---

## Participant Assignment

The assignment of a specific participant to a specific reservation line.

Why the concept exists: [ADR-008](../architecture/architecture-decisions/ADR-008-participant-assignment.md).

---

## Allocation

The assignment of one physical asset to a reservation line.

Who creates allocations and when: [business-rules.md](business-rules.md#reservation-availability).

---

## Booking Cutoff

The moment after which customers can no longer make a reservation online. When it is: [business-rules.md](business-rules.md#booking-cutoff).

---

## Late Reservation

A reservation that operations creates after the booking cutoff, for example when a customer calls. When it is accepted: [business-rules.md](business-rules.md#late-reservations).

---

## Allocation Deadline

The moment by which every reservation line that requires physical equipment must be fully allocated. When it is: [business-rules.md](business-rules.md#allocation-deadline).

---

## Product

Something FlowDock offers for rental or purchase.

The current products: [business-rules.md](business-rules.md#products).

---

## Capacity

The number of participants that one unit of a product takes. Which products have a capacity: [business-rules.md](business-rules.md#capacity).

---

## Asset

A physical item owned by FlowDock.

Examples:

- Catamaran #001
- SUP #015

---

## Hub

A central location where assets are stored and managed.

Example:

Utrecht Hub

---

## Rental Location

A location where customers start and finish their rental.

Example:

Loosdrecht Rental Location

---

## Operations

The FlowDock staff who manage reservations, allocations and assets. Operations handles reservation changes and late reservations. Drivers carry out the work on location and are not part of operations.

---

## Driver

A person who performs operational tasks for FlowDock, such as transporting assets and handling incidents.

What drivers may and may not do: [business-rules.md](business-rules.md#drivers).

---

## Incident

An operational event during an active rental that requires attention.

Examples:

- Battery failure
- Customer returned late
- Customer requires pickup
- Damage reported

---

## Transaction

A financial event.

Examples:

- Rental payment
- Late fee
- Pickup charge
- Additional drinks purchased

---
