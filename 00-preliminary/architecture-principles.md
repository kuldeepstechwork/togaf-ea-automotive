# Architecture Principles

These principles govern every architecture decision made across the Torvane modernization program. They were ratified by the Architecture Review Board (ARB) during the Preliminary Phase and are binding on Phase E vendor selection, Phase F migration sequencing, and Phase G implementation governance alike — any solution design that conflicts with a principle below requires a documented waiver from the ARB (see [governance-framework-setup.md](./governance-framework-setup.md)). Each principle follows the standard TOGAF format: Name, Statement, Rationale, Implications.

## 1. Dealer Operations Continuity Is Non-Negotiable

**Statement:** No migration activity may degrade a dealer's ability to sell, service, or source parts for a vehicle during business hours.

**Rationale:** Dealers are franchise partners, not internal business units — an outage at a dealer counter has direct revenue and contractual consequences Torvane does not fully control, and repeated disruption risks franchise relationship damage that outlasts the program.

**Implications:** Every migration wave requires a rollback path executable within a single business day; cutover windows are restricted to off-peak hours per region; parallel-run periods are budgeted into every wave rather than treated as optional.

## 2. Data Is a Shared Enterprise Asset, Not a System-Owned Silo

**Statement:** Master data (vehicle, dealer, customer, parts, inventory) is owned by a designated domain, exposed through governed APIs or events, and never duplicated via direct database access.

**Rationale:** The as-is landscape's core failure mode is uncontrolled point-to-point data duplication across the DMS, telematics platform, and EDI gateway, which is the direct cause of the inventory visibility and latency problems driving this program.

**Implications:** New systems must expose data through the integration backbone (see [reference-architecture.md](../04-phase-d-technology-architecture/reference-architecture.md)); direct database-to-database integration is prohibited without an ARB waiver; every data domain requires a named data owner accountable for schema and quality.

## 3. Buy Commodity Capability, Build Differentiated Capability

**Statement:** Where a capability is not a source of competitive differentiation for Torvane, the program will select a commercial platform over custom development.

**Rationale:** A 15-year custom DMS is the underlying problem, not the solution pattern to repeat; commodity capabilities (dealer CRM workflow, parts catalog management) do not justify the ongoing engineering cost of ownership when mature commercial platforms exist.

**Implications:** Phase E vendor evaluation is mandatory before any build decision; EV telemetry ingestion and real-time inventory conflict resolution are treated as differentiated and may be built in-house (see [ADR-005](../adrs/adr-005-ev-telemetry-ingestion-architecture.md)); build decisions require an explicit differentiation justification recorded in the solution building block catalogue.

## 4. Design for Eventual Consistency, Not Distributed Transactions

**Statement:** Cross-domain business processes are designed to tolerate eventual consistency; the architecture does not rely on distributed two-phase commit across system boundaries.

**Rationale:** A multi-region, multi-vendor target architecture makes synchronous distributed transactions operationally fragile and a direct threat to the availability principle below; the business processes involved (inventory, order, parts allocation) already tolerate short-lived inconsistency in the as-is state.

**Implications:** Every cross-domain write path requires an explicit conflict-resolution and compensation design reviewed by the ARB; user-facing screens must be able to represent "pending reconciliation" states; idempotency keys are mandatory on all event producers.

## 5. Security and Privacy Are Designed In, Not Bolted On

**Statement:** Every solution building block must satisfy data protection, access control, and audit requirements at design time, not as a pre-launch checklist item.

**Rationale:** Connected-vehicle telemetry and dealer/customer PII place Torvane under multiple overlapping data protection regimes across its operating countries; retrofitting security into a live production system is measurably more expensive and error-prone than designing it in.

**Implications:** Threat modeling is a mandatory Phase E deliverable per solution building block; the ARB will not approve a Phase F transition architecture without a completed data protection impact assessment where personal or vehicle-location data is involved.

## 6. Prefer Loosely Coupled, Independently Deployable Services

**Statement:** New application components are designed as independently deployable services with explicit, versioned contracts rather than as extensions to a shared monolith.

**Rationale:** The as-is DMS monolith's core failure mode is that a single low-risk change requires a full-system regression cycle; coupling is the root cause of the multi-week release cadence that makes the current platform unable to respond to market pressure.

**Implications:** Shared libraries are permitted for cross-cutting concerns (logging, auth) but shared mutable state across services is prohibited; every service exposes a versioned API contract with a documented deprecation policy; team boundaries are expected to roughly track service boundaries.

## 7. Architecture Decisions Are Made Explicit and Recorded

**Statement:** Any decision with material cost, risk, or reversal-cost impact is documented as an Architecture Decision Record (ADR) with alternatives considered and trade-offs quantified.

**Rationale:** A program of this scale and duration will outlive the individuals who make its early decisions; undocumented rationale is the most common cause of costly decision reversal in multi-year programs.

**Implications:** No solution building block enters Phase F migration planning without an associated ADR where the decision meets the materiality threshold defined in [governance-framework-setup.md](./governance-framework-setup.md); ADRs are version-controlled artifacts, not meeting minutes.

## 8. Cloud-Native by Default, On-Premises by Exception

**Statement:** New workloads are designed for public cloud deployment; on-premises deployment requires an explicit, ARB-approved exception.

**Rationale:** The as-is on-premises DMS is the primary constraint preventing the elastic scaling and multi-region availability the to-be architecture requires; Torvane does not have, and does not intend to build, the operational capability to run multi-region infrastructure at cloud-provider reliability levels in-house.

**Implications:** Data residency requirements in specific operating countries may still require an on-premises or in-country exception, evaluated case by case; the technology standards catalogue (see [technology-standards.md](../04-phase-d-technology-architecture/technology-standards.md)) defines the approved cloud platform and services.

## 9. Interoperate Through Standards, Not Point Integrations

**Statement:** Integration with dealer, supplier, and regulatory third parties uses industry-standard protocols and data formats wherever a viable standard exists.

**Rationale:** Custom point-to-point integration with 600 dealers and their varied local systems does not scale operationally and is a direct contributor to the current EDI batch-latency problem.

**Implications:** New dealer-facing integrations are API-first with published OpenAPI contracts; legacy EDI is retained only where a trading partner cannot yet consume the modern interface, with a defined sunset date per partner.

## 10. Architecture Serves Measurable Business Outcomes

**Statement:** Every architecture initiative is justified against a named business metric (inventory visibility latency, parts fulfillment cycle time, telemetry ingestion throughput) and is not approved on technical merit alone.

**Rationale:** Technology modernization programs fail governance credibility when they cannot connect spend to business outcomes; this principle keeps the ARB's decisions anchored to the business case in [business-case.md](../01-phase-a-vision-and-scope/business-case.md).

**Implications:** Every Phase E solution building block carries a target metric and baseline; Phase H change management tracks adoption against these same metrics rather than a separate scorecard.

## 11. Minimize Data Duplication, Maximize Data Reuse

**Statement:** A data element is captured once at its authoritative source and reused everywhere else through governed access, not re-entered or re-derived.

**Rationale:** The as-is landscape has at least four independent vehicle-identity representations across DMS, telematics, EDI, and dealer CRM extracts, which is a direct root cause of the inventory visibility failures motivating this program.

**Implications:** Phase C data architecture must resolve to a single canonical vehicle, dealer, and parts identifier; any new system requiring a "local copy" of master data must justify it against a defined caching pattern, not ad hoc replication.

## 12. Resilience Is Designed for Regional and Vendor Failure

**Statement:** Target-state architecture for customer- and dealer-facing capability assumes that any single cloud region or vendor dependency will eventually fail, and is designed to degrade gracefully rather than fail completely.

**Rationale:** A 600-dealer network spanning multiple countries cannot tolerate a single-region or single-vendor outage translating into a full sales-floor or service-bay outage; this is the direct driver of the availability SLA established in Phase A.

**Implications:** Multi-region or multi-availability-zone deployment is mandatory for tier-1 services as defined in the technology standards catalogue; vendor lock-in risk is an explicit, weighted criterion in Phase E vendor evaluation.

*Fictional case study — see [README](../README.md) for full disclaimer.*
