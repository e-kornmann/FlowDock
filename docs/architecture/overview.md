# FlowDock Architecture Overview

## Purpose

FlowDock is a reservation and fleet management platform for rental operations.

The system manages:

- Customer reservations
- Rental products
- Physical assets
- Hubs
- Rental locations
- Drivers
- Operational incidents
- Payments

The goal is to create a platform where customer interactions, operational workflows and fleet management are supported through a clear and maintainable architecture.

---

## High-level architecture

FlowDock consists of multiple applications communicating with shared backend services.

![High Level Architecture](diagrams/01_high-level-architecture.md)

---

## Customer application (future)

A public reservation platform where customers can:

- Browse rental locations
- View available products
- Create reservations
- Complete payments

Technology:

- Next.js (future)

The customer application is separated from internal operations because it has different requirements, such as SEO and public accessibility.

---

## Operations application

An internal platform for FlowDock employees and drivers.

Responsibilities:

- Reservation management
- Fleet management
- Asset tracking
- Driver operations
- Incident handling

Technology:

- React + Vite

---

## Backend API

The backend is the central point for business logic and data access.

Responsibilities:

- Business rules
- Authentication
- Authorization
- Reservation processing
- Asset allocation
- Data access

Multiple applications can communicate with the same backend through HTTP APIs.

---

## Database

Technology:

- PostgreSQL

Responsible for:

- Relational domain data
- Transactions
- Data consistency
- Persistence of business entities

---

## Architecture principles

FlowDock follows these principles:

- Model the domain before implementation.
- Keep business logic independent from frameworks.
- Prefer simplicity over premature optimization.
- Document important decisions.
- Choose technologies based on the problem, not popularity.

See:

- [Architecture Principles](principles.md)
- [Architecture Decisions](architecture-decisions/)