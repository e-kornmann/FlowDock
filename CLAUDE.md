# FlowDock — Instructions for Claude

This file holds instructions only. Facts about the project live in `docs/`. Where each kind of information belongs is in `.claude/rules/documentation.md`. Follow it strictly: every fact has one home.

## Before Making Changes

Always read:

- README.md
- docs/about/flowdock.md
- docs/project/roadmap.md
- docs/architecture/overview.md
- docs/architecture/principles.md
- docs/domain/domain-language.md
- docs/domain/domain-model.md
- docs/domain/business-rules.md

For architectural changes also read:

- docs/architecture/architecture-decisions/

Who you are working with: docs/about/me.md.

A change is finished when it meets the Definition of Done in docs/about/flowdock.md.


## Coding Guidelines

Before creating new concepts, ask:
"Does this represent a real business concept?"

Use the terms from docs/domain/domain-language.md exactly. Do not invent synonyms.

Avoid:

- Generic names
- Over-engineered abstractions
- Duplicating domain concepts


## Decision Making

Do not silently change architecture.

When a change needs an architectural decision, propose it as an ADR with the `new-adr` skill and wait for my approval. ADRs live in docs/architecture/architecture-decisions/.


## AI Usage

AI should assist implementation, but architecture decisions must remain intentional.

Prioritize:

- Understanding
- Maintainability
- Clear boundaries
- Long-term project health


## Learning Mode

When introducing a new technology or pattern, explain:

1. What problem it solves.
2. Why FlowDock might need it.
3. What alternatives exist.
4. What trade-offs are involved.

Do not hide complexity behind abstractions.


## Working With Me

Always:

- Flag if something conflicts with my existing strategy.
- Give me your recommendation first, then the reasoning.
- Ask clarifying questions before jumping to solutions when I'm stuck.

Never:

- Write in a corporate tone.
