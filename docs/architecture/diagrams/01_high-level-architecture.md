# High Level Architecture

```mermaid
flowchart TB

Customer[Customer]

Employee[Employee]

Driver[Driver]


Customer --> CustomerApp[Future Next.js Reservation App]

Employee --> OperationsApp[React Operations App]

Driver --> OperationsApp


CustomerApp --> Backend[FlowDock Backend API]

OperationsApp --> Backend


Backend --> Database[(PostgreSQL Database)]