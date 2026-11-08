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

## Architecture principles and decisions

- [Architecture Principles](principles.md)
- [Architecture Decisions](architecture-decisions/)