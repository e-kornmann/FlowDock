# High Level Architecture

```mermaid
flowchart TB

Customer[Customer]

Operations[Operations]

Driver[Driver]


Customer --> CustomerApp[Future Next.js Reservation App]

Operations --> OperationsApp[React Operations App]

Driver --> OperationsApp


CustomerApp --> Backend[FlowDock Backend API]

OperationsApp --> Backend


Backend --> Database[(PostgreSQL Database)]
```
