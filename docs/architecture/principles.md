# FlowDock Architecture Principles

## Model the domain before implementation

We first understand the business problem before deciding on technical solutions.

Examples:

- Product ≠ Asset
- Hub ≠ Rental Location
- Incident ≠ Transaction


## Keep business logic independent from frameworks

Frameworks are tools, not the foundation of the domain.

Business rules should remain understandable without depending on specific technologies.


## Prefer simplicity over premature optimization

We build what the business needs today while keeping future growth possible.

We avoid complexity without a clear reason.


## Choose technologies based on the problem, not popularity

Technology decisions are documented through ADRs.

A popular technology is not automatically the right choice.


## Document important decisions

Architectural decisions should be understandable for future developers.

Important choices are recorded through ADRs.