# Architecture Vision and Scope

## Problem Statement

Torvane Mobility Group produces approximately 40,000 vehicles per year and sells and services them through roughly 600 franchised dealers across multiple countries, alongside a growing electric vehicle (EV) and connected-vehicle telematics business. Three interlocking system problems now materially constrain the business:

1. **Dealer Management System (DMS):** a 15-year-old on-premises monolith is the system of record for vehicle inventory, sales, and service scheduling at every dealer. It cannot provide real-time inventory visibility across the network — a vehicle sold at one dealer can show as available at another for up to several hours, causing lost sales, duplicate holds, and dealer frustration that shows up directly in franchise satisfaction scores.
2. **Connected-vehicle telemetry pipeline:** built as a bolt-on proof of concept three years ago when the EV fleet was a few thousand vehicles, the pipeline cannot scale past current EV volumes without dropping telemetry events, which degrades predictive maintenance alerts and over-the-air update targeting — both marketed features of Torvane's EV line.
3. **Parts supply chain:** runs on batch Electronic Data Interchange (EDI) file exchange with dealers and suppliers, introducing 24–48 hour latency between a parts order and supplier visibility. EV-native competitors offer real-time parts availability to their service network, and this latency is now cited directly in dealer network satisfaction surveys as a competitive disadvantage.

## Target-State Vision

By the end of the three-year program, Torvane will operate a cloud-native, event-driven platform in which:

- Vehicle inventory status is visible across the dealer network within seconds of a state change, not hours.
- Connected-vehicle telemetry ingestion scales elastically with EV fleet growth without event loss, supporting real-time predictive maintenance and OTA targeting at 5x current EV fleet volume without redesign.
- Parts orders and supply chain visibility operate on real-time or near-real-time APIs and events rather than batch EDI files, cutting the order-to-visibility latency from 24–48 hours to under 15 minutes for connected trading partners.
- Dealer-facing and customer-facing systems meet a 99.9% availability SLA with a 15-minute Recovery Time Objective (RTO) during regional cloud incidents.
- Master data (vehicle, dealer, customer, parts) is owned by a single accountable domain per entity and is never independently duplicated across systems.

## Scope Boundaries

### In Scope

- Replacement of the on-premises DMS core (inventory, sales workflow, service scheduling) with a cloud-native platform, described in Phase C/D/E.
- Redesign of the connected-vehicle telemetry ingestion pipeline to a scalable event-streaming architecture.
- Replacement of batch EDI parts supply chain integration with a real-time/near-real-time API and event-based model for dealers and suppliers able to consume it.
- Establishment of a shared integration backbone and master data ownership model across DMS, telematics, and supply chain domains.
- Dealer-facing UI modernization only to the extent required to consume new real-time inventory and parts data (a full dealer portal UX redesign is a related but separately scoped initiative).

### Explicitly Out of Scope

- **Vehicle production/manufacturing execution systems (MES).** These are governed by a separate, already-funded Industry 4.0 modernization program; integrating with this program's outputs is in scope, but replacing MES is not, to avoid two concurrent programs contending for the same plant-floor change windows.
- **Dealer financial/accounting systems.** Dealer-side accounting integration remains on existing EDI/file interfaces for this program's duration; replacing it would require dealer-by-dealer financial system migration that is not justified by this program's business case and risks stalling dealer buy-in for the higher-value inventory and parts changes.
- **Customer-facing marketing and CRM platforms.** Marketing technology is owned by a separate function with its own roadmap; this program exposes data (via the integration backbone) that marketing systems can consume, but does not redesign them.
- **Full replacement of legacy EDI for all trading partners.** Approximately 15% of Torvane's smallest parts suppliers lack the technical capacity to consume modern APIs within the program's timeline; EDI is retained for these partners with a defined future sunset date outside this program's three-year window, tracked as a known residual risk.
- **International regulatory/compliance system rationalization** beyond what is required for the specific data flows this program creates. A separate compliance program owns broader regulatory system harmonization.

These exclusions were set deliberately narrow: every excluded item either has its own funded program of record, or including it would introduce dependencies (plant floor change windows, dealer-by-dealer financial migration) that put the program's core 3-year timeline at risk without a proportional increase in benefit.

## Success Metrics

| Metric | Baseline (As-Is) | Target (To-Be) | Measured By |
|---|---|---|---|
| Cross-dealer inventory visibility latency | 2–6 hours | < 30 seconds | Event timestamp delta, inventory service telemetry |
| Parts order-to-visibility latency (connected partners) | 24–48 hours | < 15 minutes | Order event to supplier ack timestamp |
| Platform availability (customer/dealer-facing) | ~99.5% (unmeasured formally) | 99.9% | Cloud provider + APM uptime monitoring |
| EV telemetry ingestion capacity | ~15,000 vehicles sustained | 100,000+ vehicles sustained | Load test + production peak ingestion rate |
| DMS release cycle time | 6–8 weeks | ≤ 2 weeks | Deployment frequency tracking |
| Dealer network satisfaction (inventory/parts) | Baseline survey score, Year 0 | +20 points | Annual dealer network satisfaction survey |

*Fictional case study — see [README](../README.md) for full disclaimer.*
