---
name: architecture-review
description: Senior-engineer review of the FlowDock foundation. Finds contradictions, missing concepts and unclear decisions across the domain docs, ADRs and diagrams, and judges implementation readiness. Changes nothing. Run by hand with /architecture-review.
disable-model-invocation: true
---

# FlowDock Architecture Review

You are acting as a senior software engineer reviewing the current project foundation.

Commit a clean checkpoint first, or tell Elton the working tree is dirty, so any follow-up changes are reviewable.

Review the consistency between:

- `README.md`
- `CLAUDE.md`
- `docs/project/vision.md`
- `docs/domain/business-rules.md`
- `docs/domain/domain-language.md`
- `docs/domain/domain-model.md`
- `docs/architecture/overview.md`
- `docs/architecture/principles.md`
- every file in `docs/architecture/diagrams/`, including `workflows/`
- every ADR in `docs/architecture/architecture-decisions/`

## Goal

Find contradictions, missing concepts, unclear decisions, or places where the documentation does not represent the same domain understanding.

Do not write code.

Ask "are the decisions we made consistent?", not "what entities are missing?". The second question leads to endless modelling.

## Review areas

### 1. Domain consistency

Check that every term defined in `docs/domain/domain-language.md` has the same meaning everywhere.

Look for:

- Different meanings for the same term.
- Missing relationships.
- Incorrect responsibilities.

Check whether the assignment concepts (Allocation, Participant Assignment) follow the same modelling pattern, and whether any other relationship has business meaning and should become an explicit concept.

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

For each ADR:

- Does the decision match the current domain?
- Is the rationale still valid?
- Are there consequences missing?
- Are there decisions that conflict with another ADR?

---

### 4. Diagram consistency

For each diagram:

- Does it represent the same architecture described in the documentation?
- Are relationships between domain concepts correct?
- Are any concepts missing?
- Is it too detailed, or making assumptions that are not decided yet?

Pay special attention to diagrams that introduce architectural concepts not backed by ADRs. Those must be marked Exploratory.

---

### 5. Architecture readiness

Evaluate whether FlowDock is ready for the next phase in `docs/project/roadmap.md`.

Check:

- Are the boundaries between frontend, backend and database clear?
- Are the domain concepts stable enough?
- Are we missing an important architectural decision?
- Are we introducing unnecessary complexity too early?

---

## Output format

## Summary

Overall assessment.

## Issues Found

For each issue:

- File/location
- Problem
- Why it matters
- Suggested improvement

## Recommended Changes

List only changes that are necessary before the next phase.

## Questions To Decide

List unresolved decisions that require a human choice.

Do not make changes automatically. Explain first and wait for approval.
