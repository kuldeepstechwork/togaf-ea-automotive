# Gap Analysis

## Purpose

This document consolidates the gaps identified across the as-is business architecture, capability map, and data/application architectures into a single prioritized list, forming the basis for the migration roadmap ([migration-roadmap.md](../06-phase-f-migration-planning/migration-roadmap.md)). Priority is scored as a function of business impact (per the success metrics in [vision-and-scope.md](../01-phase-a-vision-and-scope/vision-and-scope.md)) and the capability maturity gap (per [capability-map.md](../02-phase-b-business-architecture/capability-map.md)).

## Prioritized Gap Register

| # | Gap | Business Impact | Maturity Gap | Priority | Addressed By |
|---|---|---|:---:|:---:|---|
| 1 | No event-driven integration backbone exists; all integration is batch or point-to-point | High — root cause of gaps 2, 3, 4 | 1→4 (largest gap) | Critical | Reference architecture + Wave 1 backbone build-out |
| 2 | Cross-dealer inventory visibility latency (hours, not seconds) | High — directly tied to $1.8M/year lost-sales estimate | 2→5 | Critical | Cross-Dealer Inventory Read Model SBB, Wave 2 |
| 3 | Telemetry ingestion cannot scale past current EV fleet volume | High — blocks EV fleet growth strategy, degrades marketed features | 2→4 | Critical | EV Telemetry Ingestion Pipeline SBB, Wave 1 |
| 4 | Parts order-to-visibility latency of 24–48 hours | High — cited competitive disadvantage in dealer surveys | 2→4 (order mgmt), 1→4 (supplier visibility) | High | Parts Ordering & Supplier Integration Platform, Wave 3 |
| 5 | No canonical vehicle identifier; ~3% unresolved match rate across systems | Medium-High — undermines reliability of every downstream fix | 2→4 | High | Vehicle MDM Service, Wave 1 (foundational, precedes gap 2) |
| 6 | No formal cloud platform operations capability | Medium — organizational risk, not a direct customer-facing symptom yet | 1→4 (largest capability gap of all) | High | Platform engineering build-out, concurrent with Wave 1 |
| 7 | DMS monolith release cycle of 6–8 weeks limits responsiveness | Medium — indirect cost, slows all future improvement | 2→4 (application architecture, not separately scored in capability map) | Medium | DMS Core Platform decomposition, Waves 1–4 |
| 8 | Dealer/Customer MDM duplication across DMS and CRM extracts | Medium — data quality and marketing/finance friction | 2→4 | Medium | Dealer MDM Service, Wave 2 |
| 9 | Architecture governance function is informal outside this program | Medium — risk to program's own sustainability post-migration | 2→4 | Medium | Governance framework operationalization, Phase G |
| 10 | Dealer training/change capacity not sized for a program of this scope | Medium — adoption risk across all other fixes | 2→3 (deliberately modest target) | Medium | Phase H change management plan |
| 11 | Legacy EDI dependency for ~15% of suppliers persists beyond program end | Low-Medium — known, accepted residual risk, not a program failure | N/A — explicitly out of full-remediation scope | Low (tracked, not actioned this program) | EDI translation layer, monitored for future sunset program |
| 12 | No formal API contract/versioning discipline exists today | Medium — technical debt risk if not addressed alongside backbone build | 1→4 (part of Integration Management) | Medium | Schema registry + API gateway, Wave 1 |

## Sequencing Logic

Gaps 1, 3, and 5 are sequenced into Wave 1 because they are foundational: the event backbone (gap 1) and vehicle MDM (gap 5) are prerequisites for meaningfully closing gap 2 (cross-dealer inventory), and the telemetry pipeline (gap 3) is prioritized in Wave 1 on its own merits because it is closest to a hard scaling failure, independent of the backbone build. This sequencing was reviewed and accepted at the Phase E ARB gate specifically to avoid the common modernization-program failure mode of building visible, demo-able features (like cross-dealer inventory) before the underlying data and integration foundation can support them reliably at scale.

Gap 11 is deliberately not closed within this program — it is logged as an accepted residual risk consistent with the Phase A scope boundary, not omitted by oversight, and is carried forward as an input to future program planning rather than silently dropped from the register.

*Fictional case study — see [README](../README.md) for full disclaimer.*
