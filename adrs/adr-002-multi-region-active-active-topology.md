# ADR-002: Multi-Region Active/Active Deployment Topology for Tier-1 Services

## Status

Accepted — ratified by the Architecture Review Board during Phase D.

## Context

The target architecture must meet a 99.9% availability SLA with a 15-minute Recovery Time Objective (RTO) during regional cloud incidents for dealer- and customer-facing tier-1 services (Inventory, Sales Workflow, Cross-Dealer Read Model), per Principle 12 (Resilience) and the success metrics in [vision-and-scope.md](../01-phase-a-vision-and-scope/vision-and-scope.md). A deployment topology decision was required before Phase E vendor evaluation and solution building block design could proceed, since it materially affects both cost and application design (specifically, conflict-resolution logic per Principle 4).

## Decision

Tier-1 services deploy in an **active/active multi-region topology** across at least two cloud regions within the approved cloud platform, with the Cross-Dealer Inventory Read Model using the eventual-consistency conflict-resolution pattern described in [to-be-business-architecture.md](../02-phase-b-business-architecture/to-be-business-architecture.md) to reconcile concurrent writes across regions.

## Alternatives Considered

1. **Single-region active/passive (standby region, manual or automated failover).** Rejected. Modeling of failover time for a passive standby — including DNS propagation, database promotion, and cache warm-up — put realistic RTO in the 25–45 minute range under regional incident conditions, exceeding the 15-minute budget. Meeting a tighter RTO with active/passive would have required a "hot standby" configuration whose cost approached that of active/active without delivering active/active's additional benefit of distributing steady-state load.
2. **Hybrid edge-plus-core model (lightweight edge caching at dealer-adjacent points of presence, single-region authoritative core).** Rejected for the initial architecture, though not permanently ruled out. This model could reduce latency for read-heavy dealer queries, but it does not solve the core availability problem — a core-region outage still fails writes network-wide — and it introduces a third architectural pattern (edge cache invalidation) on top of the eventual-consistency model already required for multi-region writes, judged to add complexity disproportionate to its benefit given that read latency was not among the program's binding success metrics.
3. **Single-region with a strict synchronous-consistency data model (no eventual consistency at all).** Rejected. This would have simplified application logic considerably but cannot satisfy the RTO/availability target without active/passive or active/active infrastructure, and combining a synchronous-consistency data model with multi-region active/active would reintroduce the cross-region distributed-transaction problem Principle 4 was specifically written to avoid.

## Consequences

**Positive:** The RTO and availability targets are achievable with standard cloud-provider multi-region capabilities rather than bespoke high-availability engineering; load is distributed across regions in steady state, providing headroom against unexpected demand spikes (e.g., EV fleet growth exceeding projections).

**Negative — quantified trade-off:** Active/active multi-region increases estimated monthly infrastructure spend by approximately 18% versus a single-region active/passive baseline (reflected in the cloud infrastructure line item of [business-case.md](../01-phase-a-vision-and-scope/business-case.md)), and requires the conflict-resolution logic described in the to-be business architecture, adding an estimated 6 weeks to the relevant Phase F wave's timeline (Wave 2, Cross-Dealer Inventory Read Model) versus a design that could assume single-region consistency.

**Affected governance bodies:** This decision is binding on all tier-1 service designs reviewed at the Pre-Integration Checkpoint ([governance-framework.md](../07-phase-g-implementation-governance/governance-framework.md)); any team proposing a single-region design for a tier-1 service requires an ARB waiver with an explicit justification for why the availability target does not apply to that service.

*Fictional case study — see [README](../README.md) for full disclaimer.*
