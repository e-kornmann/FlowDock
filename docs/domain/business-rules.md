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

Each allocation assigns exactly one asset. A reservation line that requires physical equipment needs exactly as many allocations as its quantity: 2 × SUP with motor means two allocations, one per SUP.

---

## Booking and allocation deadlines

All times are local time at the rental location.

### Booking cutoff

Customers can book online until 12:00, two days before the rental date.

Example: a rental on Saturday can be booked online until Thursday 12:00.

### Allocation deadline

Operations starts allocating after the booking cutoff.

Every reservation line that requires physical equipment must be fully allocated by 12:00, one day before the rental date.

Example: a rental on Saturday must be fully allocated by Friday 12:00.

What happens when a line cannot be fully allocated in time is not decided yet.

### Late reservations

After the booking cutoff, only operations can create a reservation, for example when a customer calls. This is possible until the allocation deadline.

Operations allocates the assets immediately when creating a late reservation. If that is not possible, the reservation is not accepted.

Example: for a rental on Saturday, a call on Thursday 15:00 can still be booked if the assets can be allocated on the spot. A call on Friday 13:00 is too late.

---

## Participants

A reservation can contain multiple participants.

For each participant we store:

- Name
- Age

Participants do not manage the reservation unless they are the main customer.

The customer is registered as a participant when they join the rental. When the customer stays ashore, one of the participants provides their contact details.

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

# Capacity

For products with a capacity, the number of participants assigned to a reservation line must equal the line's quantity times the product's capacity. Capacity is validated through participant assignments, not against the reservation as a whole.

## Electric Catamaran

Exactly 2 participants per catamaran.

A catamaran cannot be rented by one person alone. 2 × Electric Catamaran requires exactly 4 participant assignments.

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