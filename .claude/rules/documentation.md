# Documentation

Every piece of information has exactly one home. Other places link to it and never restate it. When the same fact appears in two places, keep it in its home and replace the other copy with a link.

| Information | Home |
| --- | --- |
| One-line description, documentation index, AI usage disclosure | `README.md` |
| Instructions for Claude | `CLAUDE.md`, `.claude/rules/`, `.claude/skills/` |
| Who Elton is: background, direction, how he learns | `docs/about/me.md` |
| Why FlowDock exists, learning goals, ground rules, Definition of Done | `docs/about/flowdock.md` |
| The business FlowDock simulates: purpose, future direction | `docs/project/vision.md` |
| Phases, goals for the coming weeks, this week's goal, open and parked questions | `docs/project/roadmap.md` |
| What was learned and decided, by date | `docs/project/learning-journal.md` |
| Meaning of domain terms | `docs/domain/domain-language.md` |
| Domain concepts and their relationships | `docs/domain/domain-model.md` |
| Business rules | `docs/domain/business-rules.md` |
| How the system is structured | `docs/architecture/overview.md` |
| Architecture principles | `docs/architecture/principles.md` |
| Decisions and their reasoning | `docs/architecture/architecture-decisions/ADR-*.md` |
| Diagrams | `docs/architecture/diagrams/` |

- Documentation goes in `docs/` and nowhere else, except `README.md` and `CLAUDE.md` at the root. No `README.md` or other `.md` files in code folders.
- A new topic gets its own file in the matching `docs/` folder, a row in the table above and a link in the root `README.md` Documentation list.
- Don't hard-code lists that grow, such as "ADR-001 through ADR-007" or a list of diagram files. Point at the folder instead.
- Links inside `docs/` are relative: `[domain-model.md](../domain/domain-model.md)`. From code, refer to a doc by its path from the repo root: `see docs/domain/business-rules.md`.
- When a change alters what a doc says, update the doc in the same change.
- Learning journal entries are history: never rewrite a past entry, add a new one. Open questions never go in the journal, they go in the roadmap.
- Accepted ADRs never contradict each other or the business rules. When they do, fix the wording or write a new ADR that supersedes the older one.
- An accepted ADR may get wording fixes or a missed consequence. Reversing a decision means a new ADR, and the old ADR's status becomes `Superseded by ADR-NNN`.
- A diagram illustrates what the docs already say. A diagram that introduces a concept not backed by the domain model or an ADR must be marked **Exploratory**, like `04_domain-layers.md`.
