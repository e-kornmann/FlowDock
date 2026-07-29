# FlowDock Domain Model

This document describes the main business concepts within FlowDock and their relationships.

The model focuses on business concepts rather than database implementation details.

The domain model evolves as new business decisions are made.

---

# Core Concepts

## Customer

A customer is the person responsible for a reservation.

A customer can create multiple reservations.

---

## Participant

A participant is a person who uses a rental product but is not necessarily responsible for the reservation.

Example:

A customer reserves a catamaran for four people.

Customer:
- Elton

Participants:
- Person A
- Person B
- Person C

---

## Reservation

A reservation represents a customer's request to rent one or more products for a specific period and rental location.

A reservation:

- Belongs to one customer.
- Contains one or more products.
- May have multiple participants.
- Can result in payments.
- Can have operational incidents.

---

## Product

A product represents something FlowDock offers for rental or purchase.

Examples:

- Electric Catamaran
- SUP without motor
- SUP with motor
- Drinks
- Food packages

A product describes what is offered to customers.

A product does not represent a physical item.

---

## Asset

An asset represents a physical item owned by FlowDock.

Examples:

- Catamaran #001
- SUP #015

Assets have:

- Current status
- Location
- Maintenance history
- Assignment history

Assets may be allocated to reservations.

---

## Hub

A hub is a central operational location where assets are stored and managed.

Example:

Utrecht Hub

A hub:

- Owns assets.
- Supplies rental locations.
- Coordinates transport.

---

## Rental Location

A rental location is where customers start and finish their rental.

A rental location:

- Receives assets from a hub.
- Has operational activities.
- Has drivers assigned.

---

## Driver

A driver performs operational tasks.

Examples:

- Transporting assets.
- Preparing rental locations.
- Handling incidents.
- Supporting customers.

Drivers do not modify core reservation data.

---

# Operational Concepts

## Incident

An incident represents an operational event that happens during the rental process.

Examples:

- Battery empty.
- Customer requires pickup.
- Equipment damage.
- Late return.

An incident records:

- What happened.
- When it happened.
- Which reservation or asset was involved.
- Which driver handled it.
- What actions were taken.

An incident may result in a transaction.

---

## Transaction

A transaction represents a financial event.

Examples:

- Initial rental payment.
- Pickup fee.
- Late return charge.
- Additional drinks purchased.

A transaction records:

- Amount.
- Reason.
- Payment status.
- Related reservation.

A transaction does not replace the operational event that caused it.

---

# High-level relationships

```mermaid
flowchart TB

Customer --> Reservation

Reservation --> Product

Reservation --> Participant

Product --> Asset

Hub --> Asset

Hub --> RentalLocation

Driver --> Incident

Reservation --> Incident

Reservation --> Transaction

Incident --> Transaction