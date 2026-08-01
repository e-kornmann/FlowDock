# FlowDock Architecture Review

You are acting as a senior software engineer reviewing the current project foundation before implementation starts.

Please review the consistency between:

- `README.md`
- `CLAUDE.md`
- `docs/domain/business-rules.md`
- `docs/domain/domain-language.md`
- `docs/domain/domain-model.md`
- `docs/architecture/overview.md`
- `docs/architecture/principles.md`
- `docs/architecture/diagrams/`
- `docs/architecture/architecture-decisions/ADR-001` through `ADR-007`

## Goal

Find contradictions, missing concepts, unclear decisions, or places where the documentation does not represent the same domain understanding.

Do not write code yet.

## Review areas

### 1. Domain consistency

Check whether concepts are consistently defined:

- Customer
- Participant
- Reservation
- Reservation Line
- Participant Assignment
- Product
- Allocation
- Asset
- Hub
- Rental Location
- Driver
- Incident
- Transaction

Look for:

- Different meanings for the same term.
- Missing relationships.
- Incorrect responsibilities.

Check whether Allocation and ParticipantAssignment follow the same modeling pattern and whether any other relationships should become explicit domain concepts.

---

### 2. Business rules vs domain model

Check whether every important business rule has a place in the domain model.

Examples:

- Age restrictions
- Weather rules
- Reservation ownership
- Asset availability
- Driver permissions
- Additional charges

Identify rules that are unclear or impossible to implement.

---

### 3. ADR consistency

Review ADR-001 through ADR-007.

For each ADR:

- Does the decision match the current domain?
- Is the rationale still valid?
- Are there consequences missing?
- Are there decisions that conflict with another ADR?

---

### 4. Diagram consistency

Review all architecture diagrams:

- high-level-architecture.md
- domain-overview.md
- reservation-flow.md
- domain-layers.md
- deployment-overview.md
- request-flow.md

Check:

- Do diagrams represent the same architecture described in the documentation?
- Are relationships between domain concepts correct?
- Are any concepts missing?
- Are any diagrams too detailed or making assumptions that are not decided yet?

Identify differences between diagrams and documentation.

Pay special attention to diagrams that introduce architectural concepts not backed by ADRs.

### 5. Architecture readiness

Evaluate if FlowDock is ready to start implementation.

Check:

- Are the boundaries between frontend, backend and database clear?
- Are the domain concepts stable enough?
- Are we missing an important architectural decision?
- Are we introducing unnecessary complexity too early?

---

## Output format

Please provide:

## Summary

Overall assessment.

## Issues Found

For each issue:

- File/location
- Problem
- Why it matters
- Suggested improvement

## Recommended Changes

List only changes that are necessary before implementation.

## Questions To Decide

List unresolved decisions that require a human choice.

Do not make changes automatically. Explain first and wait for approval.