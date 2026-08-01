# Reservation Flow

This diagram shows the high-level flow when a customer creates a reservation.

```mermaid
sequenceDiagram

Customer->>CustomerApp: Select rental product and location

CustomerApp->>Backend: Create reservation request

Backend->>Database: Check availability

Database-->>Backend: Available products

Backend->>Database: Store reservation

Database-->>Backend: Reservation created

Backend-->>CustomerApp: Reservation confirmation

CustomerApp-->>Customer: Show confirmation