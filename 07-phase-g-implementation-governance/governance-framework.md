# Implementation Governance Framework

## Purpose

Phase G governs the gap between an ARB-approved architecture and what delivery teams actually build. This document defines the compliance checkpoints, the architecture contract mechanism (detailed further in [architecture-contracts.md](./architecture-contracts.md)), and the non-compliance handling process for the modernization program, building on the ARB structure established in [governance-framework-setup.md](../00-preliminary/governance-framework-setup.md).

## Compliance Checkpoints

Every solution building block passes through four mandatory compliance checkpoints between Phase E approval and production go-live:

1. **Design Review Checkpoint** — before implementation begins, the delivery team presents its detailed design against the approved solution building block and architecture contract. The Principles Compliance Statement (per [governance-framework-setup.md](../00-preliminary/governance-framework-setup.md)) is reviewed here. Gate owner: relevant domain Solution Architect, with ARB escalation available.
2. **Pre-Integration Checkpoint** — before a service is connected to the shared event backbone or any production data domain, its schema contracts, idempotency handling, and observability instrumentation are reviewed against the technology standards catalogue ([technology-standards.md](../04-phase-d-technology-architecture/technology-standards.md)). Gate owner: Director, Cloud Platform Engineering.
3. **Pre-Cutover Checkpoint** — before any dealer-facing cutover (per the migration roadmap's wave structure), the team must demonstrate a tested rollback path executable within one business day (Principle 1) and evidence of a completed parallel-run period. Gate owner: ARB, mandatory full session.
4. **Post-Go-Live Checkpoint** — 30 days after cutover, the team reports actual performance against the success metrics baseline set in [vision-and-scope.md](../01-phase-a-vision-and-scope/vision-and-scope.md) and any waivers taken. Gate owner: ARB, reviewed at the next standing session.

No checkpoint may be skipped; a checkpoint may be expedited (compressed review window) only with Chair approval, and expediting is logged in the architecture decision log identically to a waiver.

## Non-Compliance Handling

When a delivery team's implementation deviates from its approved architecture contract:

- **Minor deviation** (e.g., an implementation detail not materially affecting the contract's binding terms) — documented by the Solution Architect, no ARB action required, tracked for pattern analysis across the program.
- **Material deviation** (e.g., a design that no longer meets a bound performance target, or introduces a new external dependency not in the original design) — triggers a mandatory ARB review before the affected checkpoint can pass. The team may proceed only with an approved waiver or a corrected design.
- **Principle violation discovered post-go-live** — the most severe category. Triggers an immediate ARB session, a formal risk assessment, and a remediation plan with a bounded timeline; the CISO holds escalation authority to require an emergency remediation ahead of the standard timeline if the violation involves data protection or security exposure.

## Governance Metrics

The ARB tracks its own effectiveness using metrics reviewed at each phase-gate review: number of waivers granted and their expiry status, average time-to-decision for escalated issues, number of material deviations caught at each checkpoint versus discovered post-go-live (a proxy for whether checkpoints are functioning as intended), and principles compliance rate across all reviewed designs. A rising rate of post-go-live discoveries relative to checkpoint-caught deviations is treated as a governance process failure signal requiring its own remediation, not just a delivery team issue.

## Relationship to Program Management

Implementation governance intersects with, but is organizationally distinct from, program delivery management. The Program Director owns schedule, budget burn-down, and resourcing; the ARB owns whether what is being built is what was architecturally approved. Where these two conflict — for example, a schedule-driven proposal to skip the Pre-Cutover Checkpoint's parallel-run requirement to hit a date — the escalation path defined in [governance-framework-setup.md](../00-preliminary/governance-framework-setup.md) applies, and schedule pressure alone is explicitly not accepted as sufficient justification for a waiver against Principle 1.

*Fictional case study — see [README](../README.md) for full disclaimer.*
