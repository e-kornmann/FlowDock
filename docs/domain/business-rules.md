# FlowDock Business Rules

This document describes the business rules of FlowDock.

Business rules represent decisions from the rental business domain and are independent from technical implementation.

---

# Reservations

## Reservation ownership

A reservation has one main customer who is responsible for the reservation.

A customer can reserve multiple products within one reservation.

---

## Reservation Lines

What a reservation line holds: [domain-model.md](domain-model.md#reservation-line).

Only reservation lines that require physical equipment receive allocations.

---

## Reservation availability

Reservations are created based on product availability.

A product is available at a rental location for a period when, for every [asset type](domain-language.md#asset-type) the product requires, enough assets are left: all assets of that type at the hub that supplies the rental location, minus what is already reserved for overlapping periods. A reservation counts as soon as it is made, not only once it is allocated.

Availability is per period, not per day. An asset can serve several reservations on the same day, as long as their periods do not overlap.

Between two reservations, an asset needs a turnaround buffer before it can go out again, for example to charge a motor kit or check a board. The length of the buffer per asset type is not decided yet, see [roadmap.md](../project/roadmap.md#parked).

Example: SUP board #015 can go out 10:00–13:00 and again 14:00–17:00 on the same day, if its buffer fits between 13:00 and 14:00.

A reservation does not require physical assets to be allocated immediately.

Physical assets are allocated later by FlowDock operations.

FlowDock may suggest suitable assets, while operations can review or change the allocation before the rental begins.

A reservation line that requires physical equipment needs one [allocation](domain-language.md#allocation) for every asset its product requires: 2 × SUP with motor means four allocations, two SUP boards and two motor kits.

---

## Booking and allocation deadlines

All times are local time at the hub. A hub and the rental locations it supplies are always in the same time zone.

### Booking cutoff

Customers can book online until 12:00, two days before the rental date.

Example: a rental on Saturday can be booked online until Thursday 12:00.

### Allocation deadline

Operations starts allocating after the booking cutoff.

Every reservation line that requires physical equipment must be fully allocated by 12:00, one day before the rental date.

Example: a rental on Saturday must be fully allocated by Friday 12:00.

What happens when a line cannot be fully allocated in time is not decided yet, see [roadmap.md](../project/roadmap.md#parked).

### Late reservations

After the booking cutoff, only operations can create a reservation, for example when a customer calls. This is possible until the allocation deadline.

Operations allocates the assets immediately when creating a late reservation. If that is not possible, the reservation is not accepted.

Example: for a rental on Saturday, a call on Thursday 15:00 can still be booked if the assets can be allocated on the spot. A call on Friday 13:00 is too late.

---

## Participants

Participants do not manage the reservation unless they are the main customer.

When the customer stays ashore and so is not a [participant](domain-model.md#customer), one of the participants provides their contact details.

Participants are assigned to reservation lines at booking time, since the customer already knows who is using which product when the reservation is created. This is unlike asset allocation, which is deferred to operations.

---

# Products

FlowDock offers different products.

Examples:

### Rental products

- Electric Catamaran
- SUP without motor
- SUP with motor

### Asset types per product

What one unit of each rental product requires:

| Product | Asset types per unit |
| --- | --- |
| Electric Catamaran | 2 SUP boards, 2 motor kits, 1 catamaran kit |
| SUP without motor | 1 SUP board |
| SUP with motor | 1 SUP board, 1 motor kit |

Every motor kit fits every SUP board: all boards use the same fin box. Why products are built from asset types: [ADR-009](../architecture/architecture-decisions/ADR-009-products-require-asset-types.md).

### Consumable products

- Drinks
- Food packages

Stock tracking for consumable products is deferred, see [ADR-006](../architecture/architecture-decisions/ADR-006-reserve-products-not-assets.md).

Each product can have different business rules, such as:

- Minimum age
- Capacity
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

## SUP without motor and SUP with motor

Exactly 1 participant per SUP.

Reason: age restrictions only work when every person using a SUP is assigned to its reservation line. 2 × SUP with motor requires exactly 2 participant assignments.

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

How a cancellation is recorded: [domain-model.md](domain-model.md#reservation).

---

# Reservation changes

Customers cannot directly modify confirmed reservations.

Reservation changes are handled by operations.

---

# Asset management

Physical assets must always have a current status.

Examples:

- Available
- Allocated
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
- Assembling catamarans at the rental location
- Preparing and managing rental locations
- Handling incidents
- Supporting customers
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