# FlowDock Domain Model

This document describes the main business concepts within FlowDock and their relationships. What each term means is defined in [domain-language.md](domain-language.md). The rules that apply to the concepts are in [business-rules.md](business-rules.md).

The model focuses on business concepts rather than database implementation details.

The domain model evolves as new business decisions are made.

---

# Core Concepts

## Customer

Definition: [Customer](domain-language.md#customer).

A customer can create multiple reservations.

A customer who joins the rental is also a participant.

---

## Participant

Definition: [Participant](domain-language.md#participant).

For each participant we store:

- Name
- Age

Example:

A customer reserves two catamarans for four people and joins the rental.

Customer:
- Elton

Participants:
- Elton
- Person A
- Person B
- Person C

---

## Reservation

Definition: [Reservation](domain-language.md#reservation).

A reservation:

- Belongs to one customer.
- Is for one rental location.
- Has one period: a start and end time.
- Contains one or more reservation lines.
- May have multiple participants.
- May result in one or more financial transactions.
- Can have operational incidents.
- May be cancelled, with a cancellation reason recorded directly on the reservation (for example: weather, unknown).

A reservation's cancellation reason is not modeled as an incident. Incidents represent events that happen during an active rental; a cancellation prevents the rental from happening at all.


---

## Reservation Line

Definition: [Reservation Line](domain-language.md#reservation-line).

Examples:

- 2 × Electric Catamaran
- 4 × Aperol
- 2 × Chorizo Sandwich

A reservation line:

- References exactly one product.
- Stores the requested quantity.
- May receive one or more allocations.
- May receive one or more participant assignments.
- Represents what the customer has requested.

---

## Participant Assignment

Definition: [Participant Assignment](domain-language.md#participant-assignment).

Participants are not linked to reservation lines directly. Product-specific rules, such as [age restrictions](business-rules.md#age-restrictions) and [capacity](business-rules.md#capacity), are validated through participant assignments. Why: [ADR-008](../architecture/architecture-decisions/ADR-008-participant-assignment.md).

When participant assignments are made: [business-rules.md](business-rules.md#participants).

Example, Reservation #1042 (Saturday 14:00–17:00, Loosdrechtse Plassen, customer Elton):

| Reservation line | Participant assignments |
| --- | --- |
| 1 × Electric Catamaran | Elton (38), Sanne (36) |
| 2 × SUP with motor | Daan (9), Mila (7) |
| 4 × Aperol | none |

If Elton changes the SUP line to SUP without motor (minimum age 10), FlowDock can tell exactly who is affected: Daan and Mila. Without participant assignments, FlowDock would only know that the reservation includes a 7-year-old, not which product she uses.

---

## Allocation

Definition: [Allocation](domain-language.md#allocation).

Assets are not linked to reservation lines directly. Why: [ADR-006](../architecture/architecture-decisions/ADR-006-reserve-products-not-assets.md).

Which reservation lines receive allocations, how many, and who makes them: [business-rules.md](business-rules.md#reservation-availability).

Example, Reservation #1042 again. Operations plans the allocations from Utrecht Hub:

| Reservation line | Allocations |
| --- | --- |
| 1 × Electric Catamaran | SUP board #003, SUP board #004, Motor kit #001, Motor kit #002, Catamaran kit #001 |
| 2 × SUP with motor | SUP board #015, SUP board #016, Motor kit #005, Motor kit #006 |
| 4 × Aperol | none (consumable) |

The next morning Motor kit #005 is broken and goes into maintenance. Operations replaces that one allocation with Motor kit #009. The board stays, and the reservation itself does not change: Elton booked 2 × SUP with motor and still gets exactly that.

### Participant assignment vs allocation

| | Participant Assignment | Allocation |
| --- | --- | --- |
| Connects a reservation line to | Participant | Asset |
| Decided by | Customer | Operations |
| When | [At booking](business-rules.md#participants) | After the [booking cutoff](business-rules.md#booking-cutoff), before the [allocation deadline](business-rules.md#allocation-deadline) |
| Applies to | Lines where rules per person apply | Lines that require physical equipment |

---

## Product

Definition: [Product](domain-language.md#product). The current products: [business-rules.md](business-rules.md#products).

A product describes what is offered to customers.

A product does not represent a physical item.

A product requires one or more [asset types](#asset-type) to fulfil a reservation, or none when it is fulfilled directly from stock. Which asset types: [business-rules.md](business-rules.md#asset-types-per-product).

---

## Asset

Definition and examples: [Asset](domain-language.md#asset).

Assets have:

- Current status
- Location
- Maintenance history
- Allocation history

Each asset is of exactly one asset type.

Assets are assigned through allocations.

---

## Asset Type

Definition: [Asset Type](domain-language.md#asset-type). Why: [ADR-009](../architecture/architecture-decisions/ADR-009-products-require-asset-types.md).

An asset type:

- Groups assets that are interchangeable for operations.
- Is required by one or more products.

Availability is counted per asset type, see [business-rules.md](business-rules.md#reservation-availability).

---

## Hub

Definition and example: [Hub](domain-language.md#hub).

A hub:

- Owns assets.
- Supplies rental locations.
- Coordinates transport.

Asset transport between a hub and a rental location is not modeled as its own concept. This is a deliberate simplification to keep the model simple for now — the `Hub --> Rental Location` relationship is sufficient until a real operational need (for example, tracking who transported which asset and when) justifies introducing a dedicated concept.

---

## Rental Location

Definition and example: [Rental Location](domain-language.md#rental-location).

A rental location:

- Receives assets from a hub.
- Has operational activities.
- Has drivers assigned during operational shifts.

---

## Driver

Definition: [Driver](domain-language.md#driver). What drivers do and may not do: [business-rules.md](business-rules.md#drivers).

Each driver belongs to one hub: their home hub. Each hub recruits its own drivers.

Drivers are assigned to a rental location during operational shifts.

---

# Operational Concepts

## Incident

Definition and examples: [Incident](domain-language.md#incident).

A cancellation before the rental begins is not an incident, see [Reservation](#reservation).

An incident records:

- What happened.
- When it happened.
- Which reservation or asset was involved.
- Which driver handled it.
- What actions were taken.

An incident may result in a transaction.

---

## Transaction

Definition and examples: [Transaction](domain-language.md#transaction).

A transaction records:

- Amount.
- Reason.
- Payment status.
- Related reservation.

A transaction does not replace the operational event that caused it.

---

# High-level relationships

See the [domain overview diagram](../architecture/diagrams/02_domain-overview.md).
