# Architecture Contracts

## Purpose

An architecture contract is the binding agreement between the Enterprise Architecture function (represented by the ARB) and a delivery team, translating an ARB-approved solution building block into commitments the delivery team is measured against at the compliance checkpoints defined in [governance-framework.md](./governance-framework.md). It exists to prevent the common failure mode where an architecturally sound design degrades silently during implementation because no one owns holding delivery to the original decision.

## What an Architecture Contract Contains

Every architecture contract includes:

1. **Scope reference** — the specific solution building block(s) from [solution-building-blocks.md](../05-phase-e-opportunities-and-solutions/solution-building-blocks.md) and any related ADR(s) it implements.
2. **Binding non-functional requirements** — quantified, testable targets (availability, latency, throughput) the implementation must meet, tied to the program's success metrics where applicable.
3. **Principles Compliance Statement** — the design's stated compliance against all 12 architecture principles, with any waivers referenced explicitly.
4. **Interface contracts** — the specific API/event schema contracts the service must publish and honor, including versioning obligations.
5. **Checkpoint schedule** — the dates or milestones at which the four compliance checkpoints apply to this specific SBB.
6. **Rollback and parallel-run commitments** — concrete, testable rollback procedures per Principle 1.
7. **Accountable owners** — named individuals (not just roles) on both the delivery team and the Enterprise Architecture function, so the contract has real accountability rather than diffuse organizational responsibility.
8. **Amendment process** — how the contract can be changed if requirements evolve, referencing the same waiver/exception mechanisms used elsewhere in governance.

## Worked Example: Cross-Dealer Inventory Read Model Architecture Contract

**Scope Reference:** Cross-Dealer Inventory Read Model & Conflict Resolution SBB (see [solution-building-blocks.md](../05-phase-e-opportunities-and-solutions/solution-building-blocks.md)); implements the eventual-consistency conflict-resolution pattern referenced in Principle 4.

**Binding Non-Functional Requirements:**
- Cross-dealer inventory state propagation: ≤ 30 seconds at p95, ≤ 90 seconds at p99, measured from source event publish to read-model consistency.
- Conflict resolution (double-hold race condition): resolved and losing-dealer notification delivered within 5 seconds of detection.
- Availability: 99.9%, multi-region active/active per [ADR-002](../adrs/adr-002-multi-region-active-active-topology.md).

**Principles Compliance Statement:** Compliant on all 12 principles. No waivers required for this SBB.

**Interface Contracts:**
- Consumes `vehicle.status.changed`, `vehicle.hold.placed`, `vehicle.hold.released` events (schema v1.2, registered in the schema registry).
- Publishes `inventory.conflict.resolved` event for downstream notification consumers.
- Exposes a synchronous read API (`GET /inventory/{vehicleId}/status`) via the API gateway for on-demand queries, per the reference architecture's dual-pattern approach.

**Checkpoint Schedule:**
- Design Review: Month 2 of Wave 2 (see [migration-roadmap.md](../06-phase-f-migration-planning/migration-roadmap.md)).
- Pre-Integration: Month 3 of Wave 2, prior to backbone connection in the pilot region.
- Pre-Cutover: Month 4 of Wave 2, prior to Region 2 dealer cutover.
- Post-Go-Live: 30 days after Region 2 cutover completes.

**Rollback and Parallel-Run Commitments:** During the parallel-run period, the legacy batch-sync inventory view remains the dealer-facing default with the new read model available in a "preview" mode; rollback consists of reverting the Dealer Portal's default data source flag, executable within 2 hours (well under the 1-business-day requirement), with no data loss since the legacy sync path continues running unmodified throughout parallel-run.

**Accountable Owners:**
- Enterprise Architecture: Solution Architect, Inventory Domain (named individual, ARB advisory seat holder).
- Delivery: Engineering Lead, Cross-Dealer Inventory Team.
- Escalation: VP, Enterprise Architecture (ARB Chair) and Program Director, DMS Modernization, jointly, per the escalation path in [governance-framework-setup.md](../00-preliminary/governance-framework-setup.md).

**Amendment Process:** Any change to the binding non-functional requirements above requires a written amendment approved at a standing ARB session; interface contract changes follow the backward-compatibility policy in [data-architecture.md](../03-phase-c-information-systems-architecture/data-architecture.md) and do not require a full contract amendment if additive.

## Why This Matters

The worked example above is deliberately specific and testable — "99.9% availability, multi-region active/active" rather than "should be highly available" — because an architecture contract that cannot be objectively checked at a compliance checkpoint is not enforceable, and an unenforceable contract provides governance theater rather than governance.

*Fictional case study — see [README](../README.md) for full disclaimer.*
