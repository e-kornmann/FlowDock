# ADR-004 — Choose frontend architecture for FlowDock applications

**Date:** 2026-07-28  
**Status:** Accepted

---

## Context

FlowDock consists of different user-facing applications with different requirements.

The customer-facing reservation experience requires:

- Public accessibility.
- SEO-friendly pages.
- Fast loading times.
- Potential marketing content.

The internal operations platform requires:

- Rich interaction.
- Dashboards.
- Fleet management.
- Reservation management.
- Internal workflows.

These applications have different priorities and should not necessarily use the same frontend architecture.

---

## Decision

The internal FlowDock operations platform will be built using React with Vite.

A future customer-facing reservation application may be built using Next.js to support SEO, server-side rendering and public content.

Both applications will communicate with the same backend services.

---

## Rationale

React with Vite is a good fit for an internal operational application where SEO is not a primary requirement.

It allows us to build a lightweight frontend while focusing on explicit communication with backend services through APIs.

Next.js provides valuable features such as server-side rendering and static generation, but these benefits are more relevant for public-facing applications.

---

## Consequences

### Positive

- Different applications can evolve independently based on their users and requirements.
- SEO requirements do not influence the internal platform architecture.
- Better alignment with platform engineering learning goals.
- Existing React knowledge can be applied directly.

### Negative

- Multiple frontend applications increase maintenance.
- More responsibility for API design and communication.
- Additional deployment considerations.

---

## Alternatives Considered

### Next.js as the primary framework

Advantages:

- Built-in routing.
- Server-side rendering.
- Strong ecosystem.
- Excellent for public websites.

Reason not chosen:

The first version of FlowDock is an internal platform where SEO and server-rendered content provide limited value.

### React + Next.js for everything

Advantages:

- One framework for all applications.

Reason not chosen:

Customer-facing and internal applications have different requirements and should be allowed to evolve independently.