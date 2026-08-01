# FlowDock Business Rules

This document describes the business rules of FlowDock.

Business rules represent decisions from the rental business domain and are independent from technical implementation.

---

# Reservations

## Reservation ownership

A reservation has one main customer who is responsible for the booking.

A customer can reserve multiple products within one reservation.

---

## Reservation Lines

A reservation contains one or more reservation lines.

Each reservation line represents:

- One product
- The requested quantity

Only reservation lines that require physical equipment receive allocations.

---

## Reservation availability

Reservations are created based on product availability.

A reservation does not require physical assets to be allocated immediately.

Physical assets are allocated later by FlowDock operations.

FlowDock may suggest suitable assets, while operations can review or change the allocation before the rental begins.

---

## Participants

A reservation can contain multiple participants.

For each participant we store:

- Name
- Age

Participants do not manage the reservation unless they are the main customer.

Participants are assigned to reservation lines at booking time, since the customer already knows who is using which product when the reservation is created. This is unlike asset allocation, which is deferred to operations.

---

# Products

FlowDock offers different products.

Examples:

### Rental products

- Electric Catamaran
- SUP without motor
- SUP with motor

### Consumable products

- Drinks
- Food packages

Consumable inventory (stock) tracking is deliberately deferred and out of scope for the first implementation.

Each product can have different business rules, such as:

- Minimum age
- Maximum rental duration
- Weather restrictions
- Availability requirements

---

# Age restrictions

Age restrictions are validated against the participant assigned to the relevant reservation line, via a participant assignment, not against the reservation as a whole.

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

- Reservation payments are refunded when FlowDock cancels due to unsafe conditions.

A weather-triggered cancellation, or a cancellation with an unknown reason, is recorded as a cancellation reason directly on the reservation. It is not modeled as an incident — incidents represent events that happen during an active rental, not reasons a rental never started.

---

# Reservation changes

Customers cannot directly modify confirmed reservations.

Reservation changes are handled by the operations team.

Drivers cannot modify reservation data.

---

# Asset management

Physical assets must always have a current status.

Examples:

- Available
- Assigned
- At rental location
- In use
- Maintenance
- Unavailable

Assets are individually tracked throughout their lifecycle.

---

# Drivers

Drivers are responsible for operational activities.

Examples:

- Transporting assets
- Managing rental locations
- Handling incidents
- Adding operational charges

Drivers cannot modify reservation data.

---

# Additional charges

Operational events may result in additional transactions.

Examples:

- Late return
- Customer pickup
- Additional drinks ordered at a rental location
- Damage handling

---

# Rental duration

Current rental duration:

Minimum:

- 1.5 hours

Maximum:

- 4 hours

Reason:

Operational planning.

Some products may have additional duration limits due to technical constraints, such as battery capacity.