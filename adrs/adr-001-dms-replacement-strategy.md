# ADR-001: DMS Replacement Strategy — Incremental Migration vs. Big-Bang Cutover

## Status

Accepted — ratified by the Architecture Review Board at the Phase A gate.

## Context

Torvane's core DMS is a 15-year-old on-premises monolith serving all 600 dealers. It must be replaced to enable the real-time inventory visibility, scalable telemetry, and real-time parts capabilities that are the program's core objectives (see [vision-and-scope.md](../01-phase-a-vision-and-scope/vision-and-scope.md)). A foundational decision was required early: how to sequence the replacement across 600 dealers in multiple countries without unacceptable business disruption, given Principle 1 (Dealer Operations Continuity).

## Decision

Torvane will migrate dealers to the new DMS Core Platform incrementally, in six waves over three years, sequenced by dealer region, with a mandatory parallel-run period per wave and a tested rollback path executable within one business day. This creates a sustained transition state (documented as Transition State T2 in [transition-architectures.md](../06-phase-f-migration-planning/transition-architectures.md)) where legacy and target systems coexist for most of the program's duration.

## Alternatives Considered

1. **Big-bang cutover (all 600 dealers simultaneously).** Rejected. This approach directly conflicts with Principle 1 — a single cutover event across a multi-country dealer network concentrates all migration risk into one irreversible event, with no way to isolate a subset of dealers if problems emerge during cutover. Modeling suggested a failed big-bang cutover could put a majority of Torvane's sales floor operations at simultaneous risk for an unbounded remediation period, an outcome the Steering Committee judged unacceptable regardless of probability.
2. **Parallel systems indefinitely (no full migration, permanent coexistence).** Rejected. While operationally lower-risk in the short term, this would mean the cross-dealer inventory visibility target — the program's largest single quantified benefit ($1.8M/year in the business case) — could never be fully realized, since a permanently split network cannot deliver uniform sub-30-second visibility. It also means carrying the T2 bidirectional bridge's operational cost indefinitely rather than as a bounded, retirable component.
3. **Function-first migration (migrate all dealers to new Inventory only, then all to new Sales Workflow, etc., rather than region-by-region).** Rejected as the primary sequencing axis, though elements of it appear within each wave. A function-first approach would require every one of 600 dealers to operate a hybrid of old and new DMS modules simultaneously for the program's full duration, which was assessed as a larger and more diffuse training/support burden (per [change-management-plan.md](../08-phase-h-change-management/change-management-plan.md)) than a region-by-region approach where a given dealer experiences a single, bounded transition period.

## Consequences

**Positive:** Migration risk is bounded per wave (never more than ~120 dealers at once); rollback is tested and time-boxed; the Dealer Network Advisory Council's peak-season blackout constraints can be honored region by region.

**Negative:** The program must build and operate the T2 bidirectional bridge and dual-consistency-guarantee logic, an estimated 14 person-months of engineering effort with no permanent home in the target architecture (pure transition cost). The program also carries a longer window (up to 3 years) during which dealers experience inconsistent capability depending on their migration wave, which is itself a communications and expectation-management burden addressed in the Phase H plan.

**Neutral / Monitored:** The exact wave boundaries (dealer count, region groupings) remain subject to Phase F ARB review at each wave gate and are not treated as immutable — the roadmap is a planning baseline, not a fixed commitment immune to re-sequencing if a wave's Post-Go-Live Checkpoint reveals unexpected adoption or technical issues.

*Fictional case study — see [README](../README.md) for full disclaimer.*
