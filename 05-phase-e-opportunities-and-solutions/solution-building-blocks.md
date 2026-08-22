# Solution Building Blocks

## Purpose

This document decomposes the capabilities identified in [capability-map.md](../02-phase-b-business-architecture/capability-map.md) and the services identified in [application-architecture.md](../03-phase-c-information-systems-architecture/application-architecture.md) into concrete solution building blocks (SBBs) — the buildable or buyable units Phase E resolves each capability into, per Principle 3 (Buy Commodity, Build Differentiated).

## Solution Building Block Catalogue

| SBB | Capability Served | Buy or Build | Differentiation Justification |
|---|---|---|---|
| Commercial DMS Core Platform | Inventory, Sales Workflow, Service Scheduling (base functionality) | Buy | Dealer workflow management is not a Torvane differentiator; mature commercial platforms exist with automotive-specific configurability |
| Cross-Dealer Inventory Read Model & Conflict Resolution | Cross-dealer inventory visibility, hold conflict handling | Build | The specific conflict-resolution logic and real-time cross-network aggregation is where Torvane's competitive gap lives; no commercial platform evaluated in Phase E met the sub-30-second propagation target out of the box |
| EV Telemetry Ingestion Pipeline | Connected-vehicle telemetry ingestion at scale | Build | Torvane's telemetry schema, EV-specific diagnostic codes, and existing OTA/predictive-maintenance consumers are proprietary; see [ADR-005](../adrs/adr-005-ev-telemetry-ingestion-architecture.md) |
| Predictive Maintenance Scoring Service | Predictive maintenance alerting | Build (on top of bought ML platform primitives) | The maintenance-prediction models are trained on Torvane's proprietary fleet data and are a marketed product differentiator |
| OTA Update Targeting Service | OTA update targeting | Build | Tightly coupled to Torvane's proprietary vehicle software release process |
| Parts Ordering & Supplier Integration Platform | Parts order management, supplier inventory visibility | Buy (commercial supply-chain integration platform) with custom EDI translation layer | Real-time supplier integration workflow is commodity; the EDI translation layer bridging legacy suppliers is Torvane-specific and built |
| Vehicle / Dealer Master Data Management Services | Vehicle MDM, Dealer/Customer MDM | Build (on commercial MDM platform primitives) | Canonical identity resolution logic must reconcile Torvane's specific four legacy identifier schemes; commercial MDM platforms provide the primitives but not the mapping logic itself |
| Integration Event Backbone | API/Integration Management | Buy (managed streaming platform) | Commodity infrastructure; no differentiation value in operating this in-house |
| API Gateway & Developer Portal | API/Integration Management (external-facing) | Buy | Commodity capability with mature, well-supported commercial and cloud-native options |
| Dealer Portal UI (inventory/parts modules) | Dealer-facing usability of new capabilities | Build (thin UI layer) | Minimal scope per Phase A boundary; a full UX overhaul is out of scope, but the modules exposing new real-time data require custom UI work |

## Decomposition Rationale

Two capabilities warranted the most scrutiny in the buy/build boundary review: the Cross-Dealer Inventory Read Model and the EV Telemetry Ingestion Pipeline. Both were initially assumed to be addressable by extending the bought DMS core platform's included modules; Phase E vendor evaluation (see [vendor-evaluation.md](./vendor-evaluation.md)) found that none of the evaluated DMS platforms could meet the sub-30-second cross-dealer propagation target without custom extension, and none had first-class support for the diagnostic-code schema Torvane's EV telemetry already uses in its predictive maintenance models — retrofitting the vendor's schema would have required a data model migration for the maintenance-scoring models themselves, judged a materially higher-risk path than building the ingestion layer directly against the chosen event backbone.

## Traceability

Each SBB above carries forward into the gap analysis ([gap-analysis.md](./gap-analysis.md)) as either a "build" work item sized in the migration roadmap, or a "buy" work item tied to the vendor evaluation's selected platform and its own implementation timeline. SBBs marked Build additionally require an ADR where the decision meets the materiality threshold in [governance-framework-setup.md](../00-preliminary/governance-framework-setup.md) — five such ADRs are recorded in [adrs/](../adrs/).

*Fictional case study — see [README](../README.md) for full disclaimer.*
