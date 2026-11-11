# Roadmap

Each phase introduces new technology only when FlowDock needs it. Why the project exists and what I want to learn: [flowdock.md](../about/flowdock.md).

**Current phase:** 0, Discovery & Design (wrapping up)

---

## Phases

| Phase | Focus | Status |
| --- | --- | --- |
| 0. Discovery & Design | Vision, domain language, business rules, domain model, ADRs, diagrams. No code. | Wrapping up |
| 1. Foundation | Repository structure, TypeScript setup, PostgreSQL in Docker for local development, empty frontend and backend apps. No features. | Next |
| 2. Core domain | Customers, Reservations, Reservation Lines, Products, Participants. No login, no payments, no AI. | Planned |
| 3. Operations | Hubs, Rental Locations, Assets and Allocation, Drivers, Incidents, Transactions. | Planned |
| 4. Platform | Every service in Docker Compose, reverse proxy, health checks, logging, CI/CD with GitHub Actions, deployments. | Planned |
| 5. Cloud | Kubernetes, Helm, secrets, ingress, autoscaling. | Planned |
| 6. Intelligence | Weather data, demand forecasting, smarter logistics, an LLM assistant for staff. | Planned |

### AI workflow track

This track runs alongside the phases: after each phase, the Claude setup improves too.

| With phase | Claude setup |
| --- | --- |
| 0 | `CLAUDE.md`, `settings.json`, documentation, comments, commits and secrets rules, skills: `architecture-review`, `update-docs`, `new-adr` |
| 1 | Path-scoped rules for backend, frontend and database code. Install the `frontend-design` skill (Anthropic, user level) when the operations app is scaffolded |
| 2 | A feature workflow skill: read the docs, ask, design, implement, test, review, update docs. Try the superpowers `brainstorming` skill (user level) for designing features before code |
| 3 | A reviewer agent that critiques code and architecture but writes no code |
| 4 | A platform agent for Docker, CI and deployments |

---

## Next six weeks

Pace assumption: a few sessions per week alongside a full-time job. Adjust the dates to reality, not the other way around.

| Week | Dates | Goal |
| --- | --- | --- |
| 1 | 9–15 Nov | **Close Phase 0.** The docs are restructured and consistent, open domain questions are decided or explicitly deferred, and an implementation-readiness review has passed. |
| 2 | 16–22 Nov | **Foundation decisions.** ADRs for repository structure (monorepo or not, package manager), backend framework and data access. |
| 3 | 23–29 Nov | **Docker basics through FlowDock.** PostgreSQL running in Docker Compose for local development. Learn images, containers, volumes and networks. |
| 4 | 30 Nov–6 Dec | **Scaffold.** Backend API with a health endpoint, Vite operations app, shared TypeScript and lint setup. First path-scoped Claude rules. |
| 5 | 7–13 Dec | **First Phase 2 slice.** Products, plus Rental Locations as reference data: schema, migration, read endpoint, tests. |
| 6 | 14–20 Dec | **First business rule in code.** Create a reservation with reservation lines and enforce the rental duration rule in framework-independent domain logic with unit tests. Retrospective, then update this roadmap. |

---

## This week: 9–15 November

**Goal:** Phase 0 is closed. The repository is ready for Foundation work.

**Learning focus:** context engineering. Understand when information belongs in `CLAUDE.md`, a rule, a skill or `settings.json`, using this week's setup as the example.

1. **Re-entry.** The last commit was on 2 August. Re-read [domain-model.md](../domain/domain-model.md) and ADR-006, ADR-007 and ADR-008 before changing anything.
2. **Review and commit the restructure.** That covers `docs/about/`, this roadmap, `README.md`, `CLAUDE.md` and `.claude/` (rules, skills, settings). Suggested as two commits: `docs: restructure documentation ownership and add roadmap` and `chore(claude): add rules, skills and settings`.
3. **Run `/update-docs`.** Fix anything still stated in two places, broken links and stale references. Known item: "Drivers cannot modify reservation data." appears twice in [business-rules.md](../domain/business-rules.md).
4. **Decide the remaining domain questions**, or record them as deliberately deferred:
   - Does a Driver have a home Hub? Decided: yes, see [domain-model.md](../domain/domain-model.md#driver).
   - Do Allocations need their own properties yet? Deferred, see [Parked](#parked).
5. **Catch up the [learning journal](learning-journal.md).** Add an entry for the 29 July to 2 August work (Reservation Line, Allocation, Participant Assignment, the review workflow) and one for this week.
6. **Run `/architecture-review`** as the implementation-readiness check. Decide every question it raises. Phase 0 is closed when nothing blocking is left.
7. **Prepare week 2.** List the Foundation decisions, and for each one answer: why do we need it, what are the alternatives, and what do they cost? Don't decide yet.

**Done when:**

- [x] Restructure committed
- [x] `/update-docs` reports no duplicates or broken links
- [x] Domain questions decided or deferred in the docs
- [ ] Learning journal up to date
- [ ] `/architecture-review` has no blocking findings
- [ ] Week 2 decision list written

---

## Parked

Open questions live here and in this week's goal, nowhere else. Parked questions are deliberately left for later. When one is picked up, it moves into a week above, and the decision goes to its home (business rules, domain model or an ADR).

An item comes back only when its trigger happens, never just because it is on this list.

| Topic | Question | Where it stands | Comes back when |
| --- | --- | --- | --- |
| Shortage | What happens when a reservation line cannot be fully allocated before the [allocation deadline](../domain/business-rules.md#allocation-deadline)? Upgrade, contact the customer, or cancel with a cancellation reason? | New | Phase 3 (allocation) starts, or a line can't be fully allocated in practice |
| Spare equipment at rental locations | Should a rental location keep spare assets or parts (for example a spare battery or a spare SUP) so a breakdown doesn't need a trip to the hub? | New | Incidents show that breakdowns often need a trip to the hub |
| Alcohol and age | Consumables such as Aperol have no age rule, but Dutch law sets 18 as the minimum age. Do consumable lines need participant assignments too? | New | Consumables can be booked with a reservation in code (Phase 2) |
| Consumable stock | Tracking stock for drinks and food. | Deferred, see [ADR-006](../architecture/architecture-decisions/ADR-006-reserve-products-not-assets.md) | Consumables run out at a rental location |
| Asset transport | Transport between hub and rental location as its own concept. | Deferred, see [domain-model.md](../domain/domain-model.md#hub) | We need to track who transported which asset and when |
| Service separation | Should the backend be split into separate services beyond the frontend and backend split of [ADR-005](../architecture/architecture-decisions/ADR-005-separate-frontend-and-backend-services.md)? | New | Part of the backend needs to scale or deploy on its own |
| eFoil | Add an eFoil (electric hydrofoil board) as a product? It needs its own minimum age, maybe instruction before the first ride, and its battery may not last the minimum rental duration. | New | Products become reference data in code (week 5) |
| Allocation properties | Do allocations need their own properties, such as status, time or who made them? | Deferred | Phase 3 (allocation) starts |
| Domain layers | Customer, operational and financial layers as architectural boundaries. | Exploratory, see [04_domain-layers.md](../architecture/diagrams/04_domain-layers.md) | Implementation shows where the real boundaries are |
