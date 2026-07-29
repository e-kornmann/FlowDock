# FlowDock Business Rules

This document describes the business rules of FlowDock.

Business rules represent decisions from the rental business domain and are independent from technical implementation.

---

# Reservations

## Reservation ownership

A reservation has one main customer who is responsible for the booking.

A customer can reserve multiple rental products within one reservation.

---

## Participants

A reservation can contain multiple participants.

For each participant we store:

- Name
- Age

Participants do not manage the reservation unless they are the main customer.

---

# Rental Products

FlowDock supports different rental products.

Examples:

- Electric Catamaran
- SUP without motor
- SUP with motor

Each rental product can have different rules:

- Minimum age
- Maximum rental duration
- Weather restrictions
- Availability requirements

---

# Age restrictions

Current rules:

## SUP without motor

Minimum age:
- 10 years

Reason:

A non-motorized SUP can be affected by wind and water movement.

---

## SUP with motor

Minimum age:
- 7 years

Reason:

The motor provides more control, but supervision is still required.

---

# Weather conditions

Rental operations depend on weather conditions.

Rentals continue during:

- Light rain

Rentals may be cancelled during:

- Heavy rain
- Strong wind

Cancellation rules:

- Reservation payment is refunded when FlowDock cancels due to unsafe conditions.

---

# Reservation changes

Customers cannot directly modify reservations after confirmation.

Reservation changes are handled by:

- Headquarters / operations team

Drivers cannot modify reservations.

---

# Asset management

Physical assets must have a current status.

Examples:

- Available
- Assigned
- At rental location
- In use
- Maintenance
- Unavailable

---

# Drivers

Drivers are responsible for operational activities.

Examples:

- Transporting assets
- Managing rental locations
- Handling incidents
- Adding operational charges

Drivers cannot change core reservation data.

---

# Additional charges

Operational events may result in additional transactions.

Examples:

- Late return
- Customer pickup
- Additional drinks ordered at location
- Damage handling

---

# Rental duration

Current rental duration:

Minimum:
- 1.5 hours

Maximum:
- 4 hours

Reason:

Battery capacity and operational planning.