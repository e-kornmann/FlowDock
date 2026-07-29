# FlowDock Project Instructions

## Project Overview

FlowDock is a reservation and fleet management platform for rental operations.

The goal is to build the system as a professional software project while learning:

- Software architecture
- Domain-driven design
- Docker
- CI/CD
- Platform engineering concepts
- AI-assisted development workflows


## Before Making Changes

Always read:

- docs/architecture/overview.md
- docs/architecture/principles.md
- docs/domain/domain-language.md
- docs/domain/domain-model.md
- docs/domain/business-rules.md

For architectural changes also read:

- docs/architecture/architecture-decisions/


## Domain Rules

Respect these domain separations:

Product ≠ Asset

Product:
What the customer rents.

Asset:
The physical item FlowDock owns.


Hub ≠ Rental Location

Hub:
Where assets are stored and managed.

Rental Location:
Where customers start their rental.


Incident ≠ Transaction

Incident:
Something operational happened.

Transaction:
A financial consequence occurred.


## Architecture Principles

Follow these principles:

- Model the domain before implementation.
- Keep business logic independent from frameworks.
- Prefer simplicity over premature optimization.
- Document important decisions.
- Choose technology based on the problem.


## Coding Guidelines

Before creating new concepts:

Ask:
"Does this represent a real business concept?"

Avoid:

- Generic names
- Over-engineered abstractions
- Duplicating domain concepts


## Decision Making

When making architectural decisions:

Do not silently change architecture.

Create or update an ADR in:

docs/architecture/architecture-decisions/


## AI Usage

AI should assist implementation, but architecture decisions must remain intentional.

Prioritize:

- Understanding
- Maintainability
- Clear boundaries
- Long-term project health

## Learning Mode

When introducing a new technology or pattern:

Explain:

1. What problem it solves.
2. Why FlowDock might need it.
3. What alternatives exist.
4. What trade-offs are involved.

Do not hide complexity behind abstractions.