# TOGAF ADM Phase Mapping

This table indexes every TOGAF Architecture Development Method (ADM) phase to the folder and artifacts in this repository that address it. Phases are worked iteratively in practice — Torvane's architecture function revisited Phase B and Phase C findings twice during Phase E vendor evaluation, for example — but the artifacts are organized by their primary phase of record for readability.

| ADM Phase | Folder | What's In It |
|---|---|---|
| Preliminary | [00-preliminary/](./00-preliminary/) | Architecture principles the program is bound by, and how the Architecture Review Board (ARB) and governance function were stood up before scoping began |
| Phase A — Architecture Vision | [01-phase-a-vision-and-scope/](./01-phase-a-vision-and-scope/) | Problem statement, target-state vision, explicit scope boundaries, stakeholder map with RACI, business case with 3-year TCO, and a CxO-facing executive summary |
| Phase B — Business Architecture | [02-phase-b-business-architecture/](./02-phase-b-business-architecture/) | As-is and to-be business process/capability narratives with diagrams, and a capability map with maturity ratings |
| Phase C — Information Systems Architecture | [03-phase-c-information-systems-architecture/](./03-phase-c-information-systems-architecture/) | Data architecture (domains, entities, integration patterns) and application architecture (as-is application landscape vs. to-be) |
| Phase D — Technology Architecture | [04-phase-d-technology-architecture/](./04-phase-d-technology-architecture/) | The target event-driven reference architecture (with explicit anti-pattern conditions) and the approved technology standards catalogue with an exceptions process |
| Phase E — Opportunities & Solutions | [05-phase-e-opportunities-and-solutions/](./05-phase-e-opportunities-and-solutions/) | Solution building block decomposition, a scored vendor evaluation, and a prioritized gap analysis |
| Phase F — Migration Planning | [06-phase-f-migration-planning/](./06-phase-f-migration-planning/) | The phased migration roadmap (Gantt) and named transition architectures between as-is and to-be |
| Phase G — Implementation Governance | [07-phase-g-implementation-governance/](./07-phase-g-implementation-governance/) | Implementation governance model, compliance checkpoints, and the architecture contract process with a worked example |
| Phase H — Architecture Change Management | [08-phase-h-change-management/](./08-phase-h-change-management/) | Organizational change impact assessment, training plan, communications plan, and adoption metrics |
| Requirements Management (ADM hub) | Threaded through all phases; formalized in [07-phase-g-implementation-governance/governance-framework.md](./07-phase-g-implementation-governance/governance-framework.md) | Requirements traceability and change-request handling sit at the center of the ADM cycle and are governed continuously rather than in a single phase |
| Cross-cutting decisions | [adrs/](./adrs/) | Five Architecture Decision Records covering the program's most consequential and hardest-to-reverse technical choices |

*Fictional case study — see [README](./README.md) for full disclaimer.*
