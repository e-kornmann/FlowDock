# FlowDock Architecture Overview

## Purpose

This document describes how FlowDock is structured. What FlowDock is as a business is described in [vision.md](../project/vision.md).

The system manages:

- Customer reservations
- Rental products
- Physical assets
- Hubs
- Rental locations
- Drivers
- Operational incidents
- Financial transactions

The goal is to create a platform where customer interactions, operational workflows and fleet management are supported through a clear and maintainable architecture.

---

## High-level architecture

FlowDock consists of multiple applications communicating with shared backend services.

See [High Level Architecture](diagrams/01_high-level-architecture.md).

---

## Customer application (future)

A public reservation platform where customers can:

- Browse rental locations
- View available products
- Create reservations
- Complete payments

Technology:

- Next.js (future)

Why the customer application is separate from the operations application: [ADR-004](architecture-decisions/ADR-004-react-over-nextjs.md).

---

## Operations application

An internal platform for operations and drivers.

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

## Architecture principles and decisions

- [Architecture Principles](principles.md)
- [Architecture Decisions](architecture-decisions/)