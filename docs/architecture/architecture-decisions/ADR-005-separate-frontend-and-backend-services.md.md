# ADR-005 — Separate frontend and backend services

**Date:** 2026-07-28  
**Status:** Accepted

---

## Context

FlowDock consists of multiple applications that interact with the same business domain.

Examples:

- Internal operations platform for employees.
- Driver workflows.
- Future customer-facing reservation application.

These applications need access to shared business logic, data and operational processes.

Combining frontend logic and backend responsibilities into one application would make it harder to support multiple clients and maintain clear boundaries.

The system also aims to explore professional software engineering practices, including:

- HTTP communication.
- API design.
- Authentication.
- Docker.
- CI/CD.
- Platform engineering concepts.

---

## Decision

FlowDock will use separate frontend applications and backend services.

The frontend applications are responsible for:

- User interaction.
- Presentation logic.
- Client-side state.

The backend service is responsible for:

- Business rules.
- Data access.
- Authentication.
- Authorization.
- Communication with external services.

Frontend applications will communicate with backend services through HTTP APIs.

---

## Rationale

Separating frontend and backend creates clear boundaries between different responsibilities.

This allows:

- Multiple frontend applications to use the same backend.
- Independent development and deployment.
- Better understanding of distributed application architecture.
- A foundation for future containerization and platform engineering.

The backend becomes the central source of business rules instead of duplicating logic across different clients.

---

## Consequences

### Positive

- Clear separation of responsibilities.
- Multiple clients can use the same backend.
- Frontend and backend can evolve independently.
- Better foundation for Docker and CI/CD.
- Business logic remains centralized.

### Negative

- More initial setup.
- Requires API contracts between services.
- Authentication and authorization become more explicit.
- Local development requires running multiple applications.

---

## Alternatives Considered

### Full-stack application approach

Example:

- Next.js handling frontend and backend together.

Advantages:

- Faster initial development.
- Less infrastructure setup.
- Single deployment unit.

Reason not chosen:

FlowDock aims to learn and apply concepts around APIs, service boundaries and platform engineering. A separated architecture provides a better foundation for these goals.

### Microservices architecture from the beginning

Advantages:

- Maximum service separation.
- Independent scaling.

Reason not chosen:

The complexity is not justified at the current stage. FlowDock will start as a modular backend application and only introduce additional services when there is a real need.