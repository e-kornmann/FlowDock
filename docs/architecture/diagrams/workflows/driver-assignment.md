# Daily Driver Assignment

```mermaid
flowchart LR

    Hub --> Driver

    Driver -->|Morning setup| RentalLocation

    RentalLocation -->|Check-in customers| Customers

    RentalLocation -->|Handle incidents| Incident

    RentalLocation -->|End of day| Hub
```