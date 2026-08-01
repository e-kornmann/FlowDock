# FlowDock Domain Language

## Customer

A person who creates a reservation and is responsible for the booking.

---

## Participant

A person who uses the rental product but is not necessarily the person who made the reservation.

Example:

A customer rents a catamaran for 4 people.

Customer:
- Elton

Participants:
- Person A
- Person B
- Person C

---

## Reservation Line

A single line within a reservation representing one product and its quantity.

---

## Participant Assignment

The assignment of a specific participant to a specific reservation line.

Needed because age restrictions apply per product, so validating them requires knowing which participant uses which reservation line, not just which participants are on the reservation as a whole.

---

## Allocation

The assignment of one or more physical assets to a reservation line.
Allocations are created by operations and may change before the rental begins.

---

## Product

Something FlowDock offers for rental or purchase.

Examples:

- Electric Catamaran
- SUP without motor
- SUP with motor
- Food items
- Drinks

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

A location where customers start their rental.

Example:

Loosdrecht Rental Location

---

## Incident

An operational event that requires attention.

Examples:

- Battery failure
- Customer returned late
- Damage reported

---

## Transaction

A financial event.

Examples:

- Rental payment
- Late fee
- Pickup charge

---

