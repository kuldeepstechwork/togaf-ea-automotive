# ADR-004: Federated Data Domain Ownership Model (Vehicle, Dealer, Customer, Parts)

## Status

Accepted — ratified by the Architecture Review Board during Phase C.

## Context

The as-is landscape has no formal data ownership model — vehicle identity alone is represented by at least four independent, uncoordinated identifiers across systems (see [data-architecture.md](../03-phase-c-information-systems-architecture/data-architecture.md)). Before the event-driven integration backbone ([ADR-003](./adr-003-event-driven-integration-backbone.md)) could be meaningfully designed, a decision was required on how master data ownership itself would be organized — specifically, whether Torvane would centralize all master data under a single enterprise data team or federate ownership by domain.

## Decision

Torvane adopts a **federated data domain ownership model**: each data domain (Vehicle, Dealer, Customer, Inventory State, Parts/SKU, Telemetry Event) has a single accountable owning function, with a named data steward, publishing that domain's canonical data through the shared event backbone. No domain is centrally owned by a single enterprise data team; instead, a Head of Data Governance role (see [stakeholder-map.md](../01-phase-a-vision-and-scope/stakeholder-map.md)) sets cross-domain standards (identifier conventions, schema governance policy) without owning any individual domain's data directly.

## Alternatives Considered

1. **Fully centralized enterprise master data management (single central team owns and curates all master data across all domains).** Rejected. Torvane evaluated this against its existing organizational structure and concluded that a central team would lack the domain expertise to make good ownership decisions for, e.g., telemetry event schemas (a Connected Vehicle & Telematics concern) versus parts SKU data (a Supply Chain concern) — and would become an organizational bottleneck for schema evolution, similar to the ESB rejection rationale in ADR-003. It would also require a significant, unbudgeted reorganization of existing domain teams that was judged disproportionate to the benefit.
2. **Fully decentralized (no cross-domain governance at all, each system team makes independent data decisions).** Rejected. This is architecturally close to the as-is state that caused the current fragmentation problem — the four-identifier vehicle problem exists precisely because no cross-domain standard governed identifier conventions. Fully decentralized ownership without any coordinating governance function would very likely reproduce this outcome in the target architecture.
3. **Domain ownership assigned to whichever team builds the first consuming application (ownership-by-first-mover) rather than by deliberate assignment.** Rejected. This was raised informally during Phase C working sessions as a pragmatic shortcut but was rejected by the ARB because it produces ownership assignments driven by implementation sequencing accidents rather than genuine business accountability — for example, Vehicle domain ownership could have defaulted to the DMS team simply because Inventory Service was built first, even though Vehicle identity is equally foundational to Telematics and Parts.

## Consequences

**Positive:** Domain expertise is applied to domain data decisions; the model scales organizationally without requiring a large central team; it is consistent with the loosely-coupled service architecture already adopted (Principle 6).

**Negative — quantified trade-off:** Federated ownership requires ongoing cross-domain coordination effort that a fully centralized model would avoid — the Head of Data Governance role and the quarterly schema governance review add an estimated 0.5 FTE of ongoing coordination overhead not required under centralization, and cross-domain schema disputes (e.g., how "vehicle" is represented differently across Manufacturing, DMS, and Telematics contexts) require the escalation path in [governance-framework-setup.md](../00-preliminary/governance-framework-setup.md) rather than a single team's unilateral decision, which is slower in the specific case of a genuine cross-domain disagreement.

**Notable Phase C boundary decision:** Customer domain ownership was deliberately kept narrower than Vehicle/Dealer under this model — the existing Customer Data Governance function retains primary ownership rather than this program establishing a new owning function, to avoid scope creep into an adjacent, separately governed domain (see [data-architecture.md](../03-phase-c-information-systems-architecture/data-architecture.md)).

**Affected governance bodies:** The Head of Data Governance role and quarterly schema governance review are new standing governance functions created by this decision, reporting into the ARB's principles enforcement structure.

*Fictional case study — see [README](../README.md) for full disclaimer.*
