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


> 2026-08-02


## Learned

### Incidents and transactions are different things

An incident is something that happens operationally, a transaction is money. A late return is an incident, and the late fee is a transaction. Keeping them apart means the operational story and the financial story can each be told on their own. Recorded in [ADR-007](../architecture/architecture-decisions/ADR-007-incident-and-transaction-separation.md).

---

### Reservation lines

A reservation is not one product: it is a list of reservation lines, each with one product and a quantity. That turned out to be the place where most rules live, because rules differ per product.

---

### Participant Assignment and Allocation

Learned that a reservation line needs two separate connections:

- To the people using it (participant assignment), because age rules apply per product, not per reservation. Recorded in [ADR-008](../architecture/architecture-decisions/ADR-008-participant-assignment.md).
- To the physical equipment (allocation), because the customer reserves a product and operations picks the asset later. Refined in [ADR-006](../architecture/architecture-decisions/ADR-006-reserve-products-not-assets.md).

The customer decides the first at booking time, operations decides the second later. Same shape, different owner and different moment.

---

### Writing down what we deliberately don't model

A cancellation is not an incident: an incident happens during an active rental, a cancellation prevents the rental from happening. Asset transport and consumable stock are deliberately not modelled yet.

Learned that writing down a deliberate simplification is as important as writing down a concept. Otherwise it looks like an oversight.

---

### Reviewing the docs as a whole

Added an architecture review command that checks the domain docs, ADRs and diagrams against each other. Fixing terminology across the docs showed how quickly the same concept gets different names in different files.


---

## Decisions Made

- Incidents and transactions are separate concepts.
- A reservation consists of reservation lines.
- Participants are assigned to reservation lines at booking time. Assets are allocated to reservation lines by operations later.
- A cancellation reason is recorded on the reservation, not as an incident.
- Asset transport and consumable stock are deliberately not modelled yet.

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

---
---


> 2026-11-10


## Learned

### Examples make concepts click

Participant assignment and allocation only became really clear with one concrete reservation worked out in a table: who uses which product, and which asset goes to which line. That example also settled that one allocation means exactly one asset. Concrete examples now live in the [domain model](../domain/domain-model.md#participant-assignment).

---

### Rules with time in them

Added the first rules that depend on time: the booking cutoff, the allocation deadline and late reservations. Learned to write them with an example ("a rental on Saturday...") and to state which clock they use (local time at the rental location).

Capacity is checked the same way as age: per reservation line, by looking at the participants assigned to that line. 2 × Electric Catamaran needs exactly 4 people assigned to the catamaran line. Four people somewhere on the reservation is not enough, because some of them might be on a SUP.

---

### Parking is not building

Questions like shortage and spare equipment came up while modelling. Learned that parking a question with a clear trigger ("comes back when") does not conflict with "design for learning, not for millions of users". Parking costs nothing; building it now would.

---

### Open questions have one home

Open questions were kept both in this journal and in the roadmap. Now they only live in the [roadmap](roadmap.md#parked): the journal records what was learned and decided, the roadmap tracks what is still open.

Also found that ADR-002 said a reservation needs available assets, while ADR-006 says reservations are made for products. Accepted ADRs must never contradict each other or the business rules.

---

### Glossary for actors and rule terms

"Employee" and "operations" were both used for the same people. Picked operations. Rule terms such as booking cutoff and capacity now have a glossary entry that links to the rule, so the meaning lives in the glossary and the numbers live in the business rules.


---

## Decisions Made

- One allocation assigns exactly one asset.
- An Electric Catamaran takes exactly 2 participants.
- Booking and allocation deadlines are part of the business rules.
- A customer who joins the rental is also a participant.
- Each driver has a home hub. Each hub recruits its own drivers.
- Allocation properties are deferred until Phase 3.
- Open questions live in the roadmap, not in the journal.
- Accepted ADRs never contradict each other or the business rules.
- FlowDock starts with one hub and four rental locations.
