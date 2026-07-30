# ADR-003 — Design the system for multiple hubs and rental locations

**Date:** 2026-07-28  
**Status:** Accepted

## Context

FlowDock starts with one central hub in Utrecht.

From this hub, equipment is transported to rental locations where customers collect and return the rented equipment.

Examples:

- Loosdrecht
- Other recreational waters
- Future locations in other regions or countries

Although the initial operation uses one hub, the system should support future expansion to multiple hubs and many rental locations.

## Decision

FlowDock will separate the concepts of Hub and Rental Location.

A Hub represents where assets are stored and managed.

A Rental Location represents where customers rent and use the equipment.

The first version will use one Hub but the model must support multiple hubs and rental locations.

## Rationale

Separating these concepts reflects the actual business process and prevents future limitations when FlowDock expands.