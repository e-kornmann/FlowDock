# Why FlowDock Exists

FlowDock is the case, not the goal.

The real project is **learning how to build professional software with AI as a teammate**. FlowDock gives that learning a realistic business to work on: a rental company with reservations, logistics, fleet and money, complex enough that every new technology has a real reason to be there.

The business itself is described in [vision.md](../project/vision.md). The decision to run FlowDock like a professional product is recorded in [ADR-001](../architecture/architecture-decisions/ADR-001-project-vision.md). Who is behind it: [me.md](me.md).

---

## What I want to learn

**Software engineering**

- Software architecture and recording decisions (ADRs)
- Domain-driven design: modelling the business before the code
- Building and testing a full-stack TypeScript application

**Platform engineering**

- Docker and Docker Compose
- HTTP and networking: what happens after `fetch("/api")`
- CI/CD
- Kubernetes
- Logging, monitoring and health checks

**AI-assisted development**

- Context engineering: giving Claude the context it needs through `CLAUDE.md`, rules, skills and agents
- Claude as a teammate in specialised roles (architect, reviewer, platform engineer) instead of a code generator
- Later: AI as a feature inside FlowDock itself

When each of these comes in is in the [roadmap](../project/roadmap.md).

---

## Ground rules

1. **We build a company, not a tutorial.** Not "today we build a login", but "who actually needs an account?" The business question comes first, the feature follows.
2. **Every new technology must solve a problem FlowDock has.** Docker comes in when starting the project by hand becomes a problem, not because Docker is popular.
3. **Design for learning, not for millions of users.** Start as small as the [business starts](../project/vision.md#starting-point). Design so growth is possible, build only what is needed now.
4. **Claude grows with the project.** After each phase we improve the AI workflow too, not only the application.
5. **I make the decisions.** Claude advises, reviews and implements. Architecture, domain and quality choices are mine.

---

## Definition of Done

A change is done when:

- The business rule is clear.
- The domain model reflects it.
- The architectural decision is recorded, if one was made.
- Claude has the context it needs for the next change.
- The code works.
- There are tests.
- The documentation is updated.
- There is a clean commit.

Until implementation starts, the last four apply to documentation only.
