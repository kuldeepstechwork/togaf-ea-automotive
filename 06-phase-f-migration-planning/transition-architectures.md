# Transition Architectures

## Purpose

TOGAF Phase F requires that migration planning define not just the as-is and to-be end states but the intermediate architecture states the organization will actually operate in along the way — because a multi-year program spends most of its calendar time in transition states, and those states carry their own risks, constraints, and support requirements that neither the as-is nor to-be documents address. This document names and describes the most architecturally significant transition state in the program: **Transition State T2 — "Dual-Write Coexistence,"** reached at the end of Wave 2 and sustained (in a shrinking footprint) through Wave 5.

## Transition State T2: Dual-Write Coexistence

### What Is True at T2

By the end of Wave 2 (per [migration-roadmap.md](./migration-roadmap.md)), roughly 180 of Torvane's 600 dealers operate on the new DMS Core Platform and Cross-Dealer Inventory Read Model, while the remaining ~420 dealers still operate on the legacy on-premises DMS monolith. Because cross-dealer inventory visibility is only valuable if it reflects the *entire* network, not just migrated dealers, the architecture at T2 requires:

- **A bidirectional bridge** between the legacy DMS's nightly/4-hourly batch sync and the new event backbone: legacy dealer inventory changes are polled and translated into backbone events (with the batch system's inherent staleness, not eliminated for those dealers yet), while backbone events reaching legacy dealers are translated back into the format the legacy batch sync process expects.
- **A visibly degraded consistency guarantee for legacy-side dealers** — the cross-dealer inventory read model must represent, and the Dealer Portal UI must display, a different staleness expectation depending on whether the counterparty dealer has migrated, rather than presenting uniform sub-30-second freshness the target architecture promises but T2 cannot yet deliver end-to-end.
- **The legacy identifier mapping table operating at full scale** (not just for individual vehicle transfers as in steady state, but as the primary reconciliation mechanism for the majority of the fleet still on legacy identifiers).
- **Dual support processes** — dealer support and platform operations staff must be trained on, and able to diagnose issues across, both the legacy monolith and the new services simultaneously, a temporary but real operational burden factored into the Phase H training plan.

### Why T2 Is Necessary Rather Than Skippable

An alternative "big bang" approach — cutting every dealer over simultaneously — was considered and rejected during Phase A scoping specifically because it violates Principle 1 (Dealer Operations Continuity): a single cutover event across 600 dealers in multiple countries would concentrate migration risk into one irreversible event, with no way to isolate or roll back a subset of dealers if problems emerged. T2 exists because incremental migration is the only approach consistent with that principle, and incremental migration mathematically implies a sustained period of legacy/target coexistence, not just a brief moment in between.

### Trade-offs Accepted at T2

The bidirectional bridge and dual-consistency-guarantee logic are themselves non-trivial engineering effort with no permanent home in the target architecture — they are explicitly temporary components, budgeted at approximately 14 person-months of the Wave 2 integration effort (reflected in the [business-case.md](../01-phase-a-vision-and-scope/business-case.md) integration engineering line item) and are retired entirely once Wave 5 completes and the legacy DMS is decommissioned. The ARB accepted this as a bounded, one-time cost against the alternative of the significantly higher risk profile a big-bang cutover would carry. The visibly degraded consistency guarantee at T2 was a deliberate UX decision, not an oversight: the Dealer Portal team initially proposed hiding the distinction to present a uniform experience, which the ARB rejected because it would mean silently misrepresenting data freshness to dealers making real-time sales decisions — a direct conflict with the transparency the to-be architecture is meant to deliver relative to the as-is state's undisclosed staleness.

### Exit Criteria for T2

T2 is retired when Wave 5 dealer cutover completes and the legacy DMS monolith is decommissioned (see Wave 5/6 in the migration roadmap). Exit is not calendar-triggered alone — it additionally requires that the bidirectional bridge's own operational metrics (translation error rate, reconciliation backlog) have remained within defined thresholds for a full quarter prior to legacy decommission, to avoid discovering bridge defects only after the fallback path (the legacy system itself) is no longer available.

## Other Transition Considerations

A secondary, shorter-lived transition state exists around the Wave 3 Parts platform cutover, where the EDI translation layer must simultaneously serve suppliers already migrated to real-time APIs and suppliers still on legacy EDI — this is a permanent feature of the to-be architecture for the ~15% EDI-only segment (per the Phase A scope decision), not a temporary transition state, and is therefore documented in [reference-architecture.md](../04-phase-d-technology-architecture/reference-architecture.md) rather than here.

*Fictional case study — see [README](../README.md) for full disclaimer.*
