# Stakeholder Map

## Purpose

Phase A requires an explicit stakeholder analysis so architecture decisions can be traced back to whose concerns they address and who is accountable for accepting the trade-offs. The table below lists the program's primary stakeholders, their core concern, and their RACI designation across the program as a whole. Individual phase documents refine RACI at the decision level where it differs from this baseline (for example, the CISO is Accountable, not merely Consulted, on any decision touching PII or vehicle location data).

## Stakeholder Table

| Stakeholder | Primary Concern | RACI (Program-Level) |
|---|---|---|
| CDTO (Chief Digital & Technology Officer) — Program Sponsor | Program delivers measurable business outcomes within approved budget; cross-program conflicts resolved | Accountable |
| CFO / Finance Business Partner | Capex/opex profile, ROI realization, budget governance | Accountable (business case), Consulted (technical decisions) |
| VP, Dealer Operations | Dealer-facing systems remain usable and available during migration; franchise relationships protected | Consulted, Informed on cutover schedules |
| VP, Connected Vehicle & Telematics | Telemetry pipeline scales with EV growth without service degradation | Consulted, Responsible for telematics domain requirements |
| Chief Information Security Officer (CISO) | Data protection, access control, and audit posture across all new systems | Accountable on security/privacy-impacting decisions |
| Head of Data Governance | Master data ownership, data quality, canonical identifiers | Responsible for data architecture (Phase C) |
| VP, Supply Chain & Parts Operations | Parts latency reduction without disrupting supplier relationships | Consulted, Responsible for supply chain requirements |
| Director, Cloud Platform Engineering | Technical feasibility, operational sustainability of target architecture | Responsible for Phase D technology architecture |
| VP, Enterprise Architecture (ARB Chair) | Architecture coherence, principle adherence, governance | Accountable for all architecture artifacts |
| Program Director, DMS Modernization | Day-to-day delivery execution against roadmap | Responsible for Phase F/G execution |
| Dealer Network Advisory Council (external, elected dealer representatives) | Dealer-side operational and financial impact of changes | Consulted on cutover planning and training (Phase H) |
| Regulatory/Compliance Office | Multi-country data residency and consumer protection compliance | Consulted, Informed |
| End Users — Dealer Sales/Service Staff | Day-to-day usability of new inventory, service, and parts tools | Informed, feedback loop via Phase H change management |
| End Users — Customers (via connected vehicle app) | Reliability of connected-vehicle features (predictive maintenance, OTA) | Informed indirectly via product management |
| Solution Architects (domain leads) | Design coherence within and across domains | Responsible, Consulted across domains |

## Reading This RACI

Because this is a program-level RACI, most rows resolve into more specific decision-level RACI further downstream — for example, the CISO's "Consulted" default becomes "Accountable" specifically for any decision the Principles Compliance Statement (see [governance-framework-setup.md](../00-preliminary/governance-framework-setup.md)) flags as touching personal or vehicle-location data. The Dealer Network Advisory Council's involvement is deliberately capped at Consulted/Informed rather than Accountable or Responsible: dealers are franchise partners rather than Torvane employees, and giving an external, elected body decision authority over internal system architecture would create a governance conflict the Steering Committee explicitly wanted to avoid. Their concerns are nonetheless treated as material — cutover scheduling in Phase F was directly shaped by Advisory Council input on peak sales season blackout windows (see [migration-roadmap.md](../06-phase-f-migration-planning/migration-roadmap.md)).

*Fictional case study — see [README](../README.md) for full disclaimer.*
