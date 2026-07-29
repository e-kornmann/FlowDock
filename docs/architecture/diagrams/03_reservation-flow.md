# Reservation Flow

This diagram shows the high-level flow when a customer creates a reservation.

```mermaid
sequenceDiagram

Customer->>ReservationApp: Select rental product and location

ReservationApp->>Backend: Create reservation request

Backend->>Database: Check availability

Database-->>Backend: Available products/assets

Backend->>Database: Store reservation

Database-->>Backend: Reservation created

Backend-->>ReservationApp: Reservation confirmation

ReservationApp-->>Customer: Show confirmation