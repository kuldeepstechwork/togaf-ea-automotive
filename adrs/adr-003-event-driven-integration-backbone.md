# ADR-003: Event-Driven Integration Backbone as the Default Cross-Domain Integration Pattern

## Status

Accepted — ratified by the Architecture Review Board during Phase C/D.

## Context

The as-is architecture's dominant integration pattern is batch file exchange and undocumented point-to-point connections (see [as-is-business-architecture.md](../02-phase-b-business-architecture/as-is-business-architecture.md)), directly implicated in the inventory visibility, telemetry scaling, and parts latency problems driving this program. A default cross-domain integration pattern needed to be selected before Phase C data architecture and Phase D technology architecture could be finalized, since it affects every subsequent solution building block.

## Decision

Torvane adopts an **event-driven integration backbone** (durable, partitioned event streaming platform with a schema registry) as the default pattern for cross-domain data propagation, layered with an API gateway for synchronous on-demand queries. Full pattern detail, applicability conditions, and — critically — explicit conditions under which this pattern should **not** be used are documented in [reference-architecture.md](../04-phase-d-technology-architecture/reference-architecture.md).

## Alternatives Considered

1. **Shared database access across domains.** Rejected outright. This is architecturally identical to the as-is pattern that caused the current master data fragmentation (four independent vehicle identifiers, ~3% unresolved match rate per [data-architecture.md](../03-phase-c-information-systems-architecture/data-architecture.md)). Continuing this pattern in the target architecture would reproduce the root cause the program exists to eliminate.
2. **Synchronous API-only integration (request/response for all cross-domain needs, no event backbone).** Rejected as the sole pattern. While simpler operationally (no streaming platform to run), it creates temporal coupling — a downstream consumer's availability becomes dependent on the real-time availability of every upstream producer it queries, directly conflicting with Principle 12 (Resilience) and the multi-region availability target in [ADR-002](./adr-002-multi-region-active-active-topology.md). APIs remain part of the architecture but as a complement to, not a replacement for, the event backbone.
3. **A commercial Enterprise Service Bus (ESB) with centralized orchestration logic.** Rejected. An ESB centralizes integration logic (transformation, routing rules) in a way that concentrates both operational risk (a single component mediating all integration) and organizational bottleneck risk (a small central team becomes a required intermediary for every new integration), which runs counter to Principle 6 (loosely coupled, independently deployable services) and the multi-team, multi-domain ownership model established in the data architecture.

## Consequences

**Positive:** Producers and consumers evolve independently; the pattern directly supports the eventual-consistency and resilience principles; audit/replay of historical events has standalone value for diagnosing issues like the inventory conflict scenario in the to-be business architecture.

**Negative — quantified trade-off:** Adopting an event backbone as default requires standing up a net-new operational capability (Cloud Platform Operations, rated 1/5 maturity as-is per the capability map) essentially from zero, budgeted within the Wave 0 foundation phase of the migration roadmap at an estimated 150-day build-out. It also requires every integrating team to build idempotent, replay-safe consumers — a skill and design discipline not currently present across Torvane engineering, addressed via the technology standards catalogue and Phase G compliance checkpoints rather than assumed to happen organically.

**Explicit boundary condition:** This decision is deliberately not absolute — [reference-architecture.md](../04-phase-d-technology-architecture/reference-architecture.md) names specific conditions (strict consistency requirements, low-volume single-consumer integrations, regulatory point-to-point mandates) where a different pattern is the correct choice, to prevent this ADR from being read as "use events for everything."

**Affected governance bodies:** Binding on all Phase E solution building block designs; enforced at the Pre-Integration Checkpoint per [governance-framework.md](../07-phase-g-implementation-governance/governance-framework.md).

*Fictional case study — see [README](../README.md) for full disclaimer.*
