# FlowDock Domain Layers

This diagram shows the separation between customer, operational and financial concepts.

```mermaid
flowchart TB

CustomerDomain[Customer Domain]

OperationalDomain[Operational Domain]

FinancialDomain[Financial Domain]


CustomerDomain --> OperationalDomain

CustomerDomain --> FinancialDomain

OperationalDomain --> FinancialDomain