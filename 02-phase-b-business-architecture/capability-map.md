# Capability Map

## Purpose

This capability map inventories Torvane's core business capabilities relevant to the modernization program and rates each on a 1–5 maturity scale, as-is and target, using a standard capability maturity rubric: **1 = Ad hoc/manual**, **2 = Repeatable but inconsistent**, **3 = Defined and standardized**, **4 = Managed and measured**, **5 = Optimized/continuously improved**. Maturity ratings are assessed by the Enterprise Architecture function in consultation with each capability's business owner, and are used to prioritize the gap analysis (see [gap-analysis.md](../05-phase-e-opportunities-and-solutions/gap-analysis.md)).

## Capability Ratings

| Capability | As-Is Maturity | Target Maturity | Rationale for Gap |
|---|:---:|:---:|---|
| Vehicle Inventory Visibility (cross-dealer) | 2 | 5 | Currently manual/phone-based confirmation is common practice due to batch sync staleness; target is fully event-driven with sub-30-second propagation |
| Vehicle Inventory Visibility (single-dealer) | 4 | 5 | Local DMS instance is reasonably reliable for single-dealer view today; target closes remaining gaps in hold/conflict handling |
| Connected-Vehicle Telemetry Ingestion | 2 | 4 | Pipeline was built as a proof of concept and has not been re-architected for scale; target is managed, elastically scaled, with defined SLOs |
| Predictive Maintenance Alerting | 2 | 4 | Directly dependent on telemetry ingestion maturity; alerts today are frequently delayed or dropped during peak load |
| Over-the-Air (OTA) Update Targeting | 3 | 4 | Functions adequately at current scale but has no defined capacity ceiling; target adds explicit scale management |
| Parts Order Management | 2 | 4 | Batch EDI creates inherent latency; target introduces real-time order visibility for connected trading partners |
| Parts Inventory Visibility (supplier-facing) | 1 | 4 | Largely opaque today — dealers and Torvane parts planners cannot see live supplier stock; target exposes near-real-time supplier inventory via API |
| Master Data Management (Vehicle) | 2 | 4 | At least four independent vehicle-identity representations exist across systems today; target establishes single canonical identifier |
| Master Data Management (Dealer/Customer) | 2 | 4 | Similar duplication issue as vehicle MDM; target consolidates under a governed data domain |
| API/Integration Management | 1 | 4 | No formal integration backbone exists — integration today is ad hoc point-to-point; target establishes a governed event backbone with published contracts |
| Architecture Governance | 2 | 4 | Governance existed informally prior to this program; the Preliminary Phase work formalized the ARB, but embedding governance into steady-state operations is still in progress |
| Cloud Platform Operations | 1 | 4 | Torvane has minimal production cloud footprint today; target requires building this capability largely from scratch via the platform engineering build-out |
| Dealer Change Adoption / Training Capability | 2 | 3 | Existing dealer training function handles periodic DMS updates adequately but has not managed a change of this scale; modest target increase reflects realistic near-term ceiling given a 600-dealer, multi-country network |

## Capability Heat Map

```mermaid
quadrantChart
    title Capability Gap: As-Is vs Target Maturity
    x-axis Low Current Maturity --> High Current Maturity
    y-axis Low Priority Gap --> High Priority Gap
    quadrant-1 Close Fast (High Gap, Some Foundation)
    quadrant-2 Foundational Build (High Gap, Starting from Zero)
    quadrant-3 Monitor Only (Low Gap, Already Mature)
    quadrant-4 Incremental Improvement
    "Cross-Dealer Inventory Visibility": [0.35, 0.9]
    "Telemetry Ingestion": [0.3, 0.85]
    "Predictive Maintenance": [0.3, 0.8]
    "Parts Order Mgmt": [0.3, 0.75]
    "Parts Supplier Visibility": [0.1, 0.85]
    "Vehicle MDM": [0.3, 0.65]
    "Dealer/Customer MDM": [0.3, 0.6]
    "Integration Backbone": [0.1, 0.9]
    "Cloud Platform Ops": [0.1, 0.8]
    "OTA Targeting": [0.5, 0.4]
    "Single-Dealer Inventory": [0.7, 0.25]
    "Architecture Governance": [0.35, 0.45]
    "Dealer Change Adoption": [0.35, 0.3]
```

The heat map deliberately separates capabilities with *some* existing foundation (quadrant 1 — where investment yields faster returns) from those effectively starting at zero maturity (quadrant 2 — Integration Backbone and Cloud Platform Operations chief among them), because these two groups require different Phase E solution strategies: quadrant 1 capabilities are largely addressed by replacing or extending existing systems, while quadrant 2 capabilities require net-new organizational capability building that the Phase H change management plan accounts for separately from the technical migration timeline.

*Fictional case study — see [README](../README.md) for full disclaimer.*
