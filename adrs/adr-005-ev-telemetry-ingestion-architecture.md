# ADR-005: EV Telemetry Ingestion Architecture — Build vs. Buy and Scaling Approach

## Status

Accepted — ratified by the Architecture Review Board during Phase E.

## Context

The as-is telemetry ingestion pipeline was built as a three-month proof of concept when the EV fleet was a few thousand vehicles; it now regularly drops or delays events during peak ingestion windows and cannot scale to support projected EV fleet growth (see [as-is-business-architecture.md](../02-phase-b-business-architecture/as-is-business-architecture.md)). A decision was required on both (a) whether to build a replacement in-house or adopt a commercial IoT/telemetry ingestion platform, and (b) the target scaling architecture, before Wave 1 of the migration roadmap could proceed, since telemetry is the program's first dealer-independent, network-wide cutover.

## Decision

Torvane will **build** the EV Telemetry Ingestion Pipeline in-house, on top of the approved managed event-streaming platform (per [technology-standards.md](../04-phase-d-technology-architecture/technology-standards.md)), deployed as a **multi-region, horizontally scalable ingestion layer** load-balanced across the fleet's geographic distribution, load-tested and provisioned to sustain 100,000+ concurrently reporting vehicles — approximately 5x the EV fleet size projected at the end of the 3-year program, deliberately over-provisioned relative to near-term need to avoid repeating the as-is pattern of building only to current-year scale.

## Alternatives Considered

1. **Adopt a commercial IoT/connected-vehicle telemetry platform** (evaluated informally alongside the DMS vendor evaluation process). Rejected for this specific component, per Principle 3 (Buy Commodity, Build Differentiated) — Torvane's telemetry schema, EV-specific diagnostic codes, and existing predictive-maintenance models are trained on and tightly coupled to a proprietary data model. Migrating to a commercial platform's schema would have required retraining or re-deriving the maintenance-scoring models against a new data representation, assessed as a materially higher-risk path than building the ingestion layer to feed the existing model pipeline. This differentiation justification is recorded in [solution-building-blocks.md](../05-phase-e-opportunities-and-solutions/solution-building-blocks.md).
2. **Vertically scale the existing single-region pipeline (larger instances, more database capacity) rather than re-architecting.** Rejected. Load testing of the current architecture indicated degradation beginning at roughly 1.3x current peak volume regardless of instance size, because the bottleneck is architectural (a relational database as the primary write target for high-volume time-series ingestion, and tightly coupled ingestion/processing logic) rather than a capacity ceiling that more hardware resolves. Vertical scaling would have bought limited runway against a fleet growth trajectory expected to cross even a generously scaled single-region ceiling within roughly 18–24 months.
3. **Single-region ingestion with the new streaming architecture (re-architect the bottleneck, but keep single-region deployment).** Rejected as insufficient on its own — this would resolve the throughput bottleneck but not the resilience requirement; a single-region telemetry outage would silently drop predictive-maintenance and OTA-targeting data fleet-wide with no fallback, which the ARB judged unacceptable for a marketed, safety-adjacent feature (predictive maintenance alerts) even though telemetry ingestion does not carry the same hard 99.9%/15-minute RTO SLA as dealer-facing tier-1 services under [ADR-002](./adr-002-multi-region-active-active-topology.md).

## Consequences

**Positive:** The rebuilt pipeline directly resolves the capability maturity gap rated 2/5 in the capability map, targeting 4/5; predictive maintenance and OTA targeting move from best-effort to managed, measured capabilities; durable, replayable event streams mean a downstream consumer outage no longer causes permanent data loss.

**Negative — quantified trade-off:** Building in-house rather than buying carries the full engineering cost of design, implementation, and ongoing operation — reflected in the "new platform engineering/SRE build-out" line item of the business case rather than a licensing fee, and requires Torvane to develop and retain telemetry-at-scale engineering expertise it does not currently have in depth. Over-provisioning to 5x current EV volume also means Year 1 infrastructure spend for this component exceeds what current-year load alone would justify — an accepted, deliberate cost against the alternative risk of a second premature scaling wall.

**Affected governance bodies:** This decision is binding on the Wave 1 Pre-Integration and Pre-Cutover Checkpoints for the telemetry pipeline ([governance-framework.md](../07-phase-g-implementation-governance/governance-framework.md)); the VP, Connected Vehicle & Telematics holds primary accountability for the resulting architecture contract, jointly with the Director, Cloud Platform Engineering for the underlying streaming infrastructure.

*Fictional case study — see [README](../README.md) for full disclaimer.*
