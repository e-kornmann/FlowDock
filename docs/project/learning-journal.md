# Learning Journal


> 2026-07-28


## Learned

### Architecture Decision Records (ADR)

Learned why important technical and domain decisions should be documented using ADRs.

Created ADRs for:

- Project vision and goals.
- Choosing PostgreSQL over MongoDB.
- Separating Hubs and Rental Locations.
- Choosing React + Vite for the internal application.
- Separating frontend and backend services.
- Reserving Products instead of Physical Assets.

Learned that ADRs are not documentation of code, 
but documentation of important decisions and the reasoning behind them.

---

### Architecture Documentation

Learned the difference between:

- Architecture overview
- Architecture principles
- Architecture decisions
- Domain documentation

Created documentation structure


---

### Domain Modelling

Learned that modelling the business domain should happen before implementation.

Important distinctions:

- Product ≠ Asset
- Hub ≠ Rental Location
- Incident ≠ Transaction

A customer reserves a product, while FlowDock operationally assigns physical assets.

---

### Architecture Diagrams

Learned how diagrams help communicate system architecture.

Created Mermaid diagrams for:

- High-level architecture
- Domain overview
- Reservation flow
- Domain layers
- Deployment overview
- Request flow

Learned that diagrams should explain the system, not replace architectural decisions.

---

### Frontend Architecture

Refined the decision around React and Next.js.

Learned that different applications can have different requirements:

- Internal operations platform → React + Vite
- Future customer reservation platform → Next.js

The choice should be based on the problem, not because one technology is more popular.

---

## Decisions Made

- FlowDock will be treated as a professional software project simulation.
- Architecture decisions will be documented using ADRs.
- Domain concepts will be defined before implementation.
- The system will start simple and avoid premature complexity.

---
---


> 2026-11-09


## Learned

### One home for every fact

Found the same information in several places: the architecture principles were listed in three files, and the learning goals in two. Copies drift apart over time, and then nobody knows which one is true.

Learned to give every kind of information exactly one home and to link to it everywhere else. The ownership table lives in `.claude/rules/documentation.md`, so Claude enforces it too.

Also learned not to hard-code lists that grow. The architecture review command said "ADR-001 through ADR-007" and silently skipped ADR-008. Pointing at the folder instead avoids that.

---

### CLAUDE.md vs rules vs skills vs settings

Learned what each part of the Claude Code setup is for:

- **CLAUDE.md**: instructions Claude reads every session. Advisory: Claude follows it, but nothing forces it.
- **Rules** (`.claude/rules/`): also loaded automatically, and they can be path-scoped. The comments rule only loads when Claude works on code files, so it costs no context while there is no code.
- **Skills** (`.claude/skills/`): loaded on demand or invoked with `/name`. Good for repeatable workflows.
- **settings.json**: enforced by the harness, not by Claude's judgement. Used for denying access to secret files and turning off the AI co-author line.
- **Commands** (`.claude/commands/`): the older form of skills. Moved `architecture-review` to a skill.

The mental model: CLAUDE.md is advisory, settings are enforced, skills load on demand.

---

### Skills with a clear purpose

Created three skills, each with one job:

- `/architecture-review`: substance. Are the domain docs, ADRs and diagrams consistent, and are we ready for the next phase?
- `/update-docs`: hygiene. Duplicates, broken links, stale references. Changes where things are written, never what was decided.
- `/new-adr`: interviews me about a decision first, then drafts the ADR as Proposed. The decision stays mine.

Learned that splitting review into "substance" and "hygiene" keeps each skill focused.

Third-party skills follow the same ground rule as technologies: only add one when it solves a problem FlowDock has now. Generic skills belong at user level, not in the repo, and a third-party skill should be read before installing it, because it is a set of instructions Claude will follow.

---

### Secrets

Learned that denying `Read` in `settings.json` only blocks Claude's file tools, not the shell or scripts. That's why there is also a rule that covers everything else.

The contract for secret files is a committed `.env.example` with placeholder values. `.env`, `*.local` and `.claude/settings.local.json` are git-ignored.

---

### Goals and roadmap

Learned that goals should not live in README or CLAUDE.md: they change every week. They live in the [roadmap](roadmap.md), and README and CLAUDE.md link to it.

Also learned not to write down undecided choices as if they were facts. An early stack sketch named Prisma, but data access is still an open decision for the Foundation phase.


---

## Decisions Made

- Every fact has one home. Other documents link to it.
- Generic third-party skills are installed at user level, only when needed.
- Claude is not listed as a co-author.
