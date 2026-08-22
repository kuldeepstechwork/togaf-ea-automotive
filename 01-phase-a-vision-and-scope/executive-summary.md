# Executive Summary

## The Problem

Torvane's dealer, inventory, and parts systems are built on a 15-year-old on-premises platform that cannot show accurate vehicle inventory across our 600-dealer network in real time, cannot scale our connected-vehicle telemetry pipeline past current EV volumes, and moves parts data on 24–48 hour batch file exchanges. EV-native competitors offer real-time inventory and parts visibility today. This is now a measurable competitive disadvantage, showing up in dealer satisfaction scores and an estimated $1.8M/year in lost sales from inventory visibility gaps alone.

## The Recommendation

Replace the core DMS, telemetry pipeline, and parts integration with a cloud-native, event-driven platform over a 3-year phased program, migrating dealer-by-dealer and region-by-region to avoid disrupting sales floor and service bay operations. Full detail is in [vision-and-scope.md](./vision-and-scope.md); the roadmap and sequencing are in [migration-roadmap.md](../06-phase-f-migration-planning/migration-roadmap.md).

## The Cost

The 3-year program costs approximately **$28.0M**, roughly **$1.4M more** than continuing to run the current systems as-is over the same 3 years. The investment case is not a 3-year story — it is a steady-state story: once the program completes, we project **$2.3M/year in ongoing savings** versus the status quo, paying back the incremental investment in **under 7 months** after go-live, and delivering roughly **236% ROI over 5 years**. Full arithmetic is in [business-case.md](./business-case.md).

## The Timeline

Three years, phased in waves by dealer region, with the highest-risk cutovers scheduled outside peak sales seasons. The connected-vehicle telemetry pipeline is prioritized in the first 12 months because it is the closest to a hard scaling wall. Full DMS cutover for the last dealer region completes by the end of Year 3.

## The Risk

The primary risk is dealer-facing disruption during cutover; we are managing it with mandatory rollback paths, parallel-run periods, and off-peak cutover windows as binding architecture principles, not optional best practices. The secondary risk is vendor lock-in on the new DMS platform; our vendor evaluation weighted this explicitly and the selected platform's exit costs are documented and monitored. A downside scenario (20% cost overrun, slower adoption) still returns a positive 5-year ROI of approximately 95%, which is why the Steering Committee approved the program at the current budget rather than requesting a reduced-scope alternative.

*Fictional case study — see [README](../README.md) for full disclaimer.*
