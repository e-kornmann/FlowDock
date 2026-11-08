---
name: new-adr
description: Drafts a new Architecture Decision Record in docs/architecture/architecture-decisions/ using the FlowDock ADR format, after interviewing Elton about the decision. Use when a change needs an architectural or domain decision, or when Elton asks for an ADR. The ADR stays Proposed until Elton accepts it.
argument-hint: "[short title of the decision]"
---

# New ADR

Draft an ADR for `$ARGUMENTS`. No argument: ask what the decision is about.

The decision belongs to Elton. Your job is to make the trade-offs explicit, not to decide.

## 1. Interview first

Before writing anything, make sure these are clear. Ask about what is not:

1. **Why do we need this?** What problem in FlowDock forces the decision now?
2. **What are the alternatives?** At least two, including "don't decide yet" when that is realistic.
3. **Which one, and why?** Give your recommendation first, then the reasoning, then ask Elton to choose.
4. **What does the choice cost?** Its downsides and what becomes harder later.
5. **How does Claude help here?** Only when it matters for the decision.

Check the decision against `docs/architecture/principles.md` and the existing ADRs. Flag a conflict before writing.

If it turns out not to be architectural (a domain refinement or a wording fix), say so and suggest updating the domain docs instead. Not every decision needs an ADR.

## 2. Write the file

- Number: the next free number in `docs/architecture/architecture-decisions/`, three digits.
- File name: `ADR-NNN-short-kebab-title.md`.
- Follow the structure of the existing ADRs exactly:

```md
# ADR-NNN — Title

**Date:** YYYY-MM-DD
**Status:** Proposed

---

## Context

## Decision

## Rationale

## Consequences

### Positive

### Negative

---

## Alternatives Considered

### Alternative name

Advantages:

Reason not chosen:

---

## Related Concepts
```

`Related Concepts` is optional; use it when the ADR touches domain terms.

## 3. Afterwards

- Status stays `Proposed` until Elton says it is accepted.
- If it reverses an earlier ADR, set that ADR's status to `Superseded by ADR-NNN` and change nothing else in it.
- List the docs that must change because of this decision (domain model, business rules, overview, diagrams). Update them only after Elton accepts.
