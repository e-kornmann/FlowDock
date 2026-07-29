# Learning Journal


> 2026-07-28


## Learned

### Architecture Decision Records (ADR)

Learned why important technical and domain decisions should be documented using ADRs.

Created ADRs for:

- Project vision and goals.
- Choosing PostgreSQL over MongoDB.
- Separating Hubs and Rental Locations.
- Choosing React + Vite for the internal application.
- Separating frontend and backend services.
- Reserving Products instead of Physical Assets.

Learned that ADRs are not documentation of code, 
but documentation of important decisions and the reasoning behind them.

---

### Architecture Documentation

Learned the difference between:

- Architecture overview
- Architecture principles
- Architecture decisions
- Domain documentation

Created documentation structure


---

### Domain Modelling

Learned that modelling the business domain should happen before implementation.

Important distinctions:

- Product ≠ Asset
- Hub ≠ Rental Location
- Incident ≠ Transaction

A customer reserves a product, while FlowDock operationally assigns physical assets.

---

### Architecture Diagrams

Learned how diagrams help communicate system architecture.

Created Mermaid diagrams for:

- High-level architecture
- Domain overview
- Reservation flow
- Domain layers
- Deployment overview
- Request flow

Learned that diagrams should explain the system, not replace architectural decisions.

---

### Frontend Architecture

Refined the decision around React and Next.js.

Learned that different applications can have different requirements:

- Internal operations platform → React + Vite
- Future customer reservation platform → Next.js

The choice should be based on the problem, not because one technology is more popular.

---

## Decisions Made

- FlowDock will be treated as a professional software project simulation.
- Architecture decisions will be documented using ADRs.
- Domain concepts will be defined before implementation.
- The system will start simple and avoid premature complexity.

---

## Open Questions

- How should incidents and financial transactions be modelled?
- How should asset allocation work?
- When should services be separated?
- How will Docker, CI/CD and Kubernetes fit into the future architecture?