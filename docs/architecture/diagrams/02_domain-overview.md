# FlowDock Domain Overview

This diagram shows the main business concepts within FlowDock.

```mermaid
flowchart TB

Customer[Customer]

Reservation[Reservation]

Product[Product]

Asset[Physical Asset]

Hub[Hub]

RentalLocation[Rental Location]

Driver[Driver]

Participant[Participant]

Incident[Incident]

Transaction[Transaction]


Customer -->|creates| Reservation

Reservation -->|contains| Product

Reservation -->|may have| Participant

Product -->|may require| Asset

Hub -->|owns| Asset

Hub -->|supplies assets to| RentalLocation

Driver -->|operates from| Hub

Driver -->|handles| Incident

Reservation -->|results in| Transaction

Incident -->|may result in| Transaction