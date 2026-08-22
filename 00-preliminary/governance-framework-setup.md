# Governance Framework Setup

## Purpose

This document establishes the governance function that oversees the Torvane modernization program before any scoping work in Phase A begins. TOGAF's Preliminary Phase requires that governance structures, principles enforcement, and escalation paths be defined before the ADM cycle starts producing artifacts that need governing — retrofitting governance onto an in-flight program is a known failure pattern the ARB explicitly wanted to avoid, having seen it happen on Torvane's previous (unsuccessful) DMS replacement attempt four years ago.

## Architecture Review Board (ARB) Constitution

The ARB is the program's binding architecture governance body. It is chaired by the VP of Enterprise Architecture and comprises:

| Seat | Role | Voting? |
|---|---|---|
| Chair | VP, Enterprise Architecture | Yes |
| Member | Chief Information Security Officer (or delegate) | Yes |
| Member | VP, Dealer Operations | Yes |
| Member | VP, Connected Vehicle & Telematics | Yes |
| Member | Head of Data Governance | Yes |
| Member | Director, Cloud Platform Engineering | Yes |
| Member | Finance Business Partner (Program) | Yes |
| Advisory (non-voting) | Program Director, DMS Modernization | No |
| Advisory (non-voting) | Solution Architects (rotating, by domain under review) | No |

A decision requires a simple majority of voting members present, with the Chair holding a tie-breaking vote. The CISO holds an effective veto on any decision with an unresolved security or data protection finding — a majority vote cannot override an open CISO objection; it can only be escalated (see below).

## Cadence

- **Standing ARB session:** biweekly, 90 minutes, for architecture decision review and ADR ratification.
- **Phase-gate review:** at the close of every ADM phase (Preliminary through H), a dedicated ARB session formally accepts or rejects the phase's artifacts before the next phase begins.
- **Ad hoc session:** may be convened within 3 business days by the Chair or any voting member for a decision that blocks active delivery work.
- **Quarterly principles review:** the ARB reviews the 12 architecture principles for continued relevance every quarter; a principle can only be amended by a two-thirds majority vote, recorded as an addendum to [architecture-principles.md](./architecture-principles.md).

## Principles Enforcement

Every solution design submitted to the ARB (as part of Phase E solution building blocks or a Phase G architecture contract) must include a **Principles Compliance Statement** — a short table mapping the design against each of the 12 principles as Compliant / Non-Compliant / Not Applicable. A Non-Compliant entry requires either a redesign or a documented waiver.

**Waiver process:** A waiver requires (1) a written justification from the submitting team, (2) a quantified description of the risk being accepted, (3) a named accountable owner for that risk, and (4) an expiry date no longer than 12 months, after which the waiver must be re-justified or the design brought into compliance. Waivers are logged in the program's architecture decision log and reviewed at every phase-gate review.

## Escalation Path

1. **Solution Architect ↔ Delivery Team disagreement:** resolved by the relevant domain Solution Architect; if unresolved within 5 business days, escalates to step 2.
2. **Domain dispute (e.g., data ownership conflict between Telematics and DMS domains):** escalates to the ARB's biweekly session or an ad hoc session if delivery is blocked.
3. **ARB deadlock or CISO veto dispute:** escalates to the Program Steering Committee, chaired by the Chief Digital & Technology Officer (CDTO), which includes the CFO sponsor and the Chief Revenue Officer representing dealer network interests. The Steering Committee's decision is final for the program.
4. **Cross-program conflict (e.g., a decision here conflicts with a parallel finance-systems program):** escalates directly to the CDTO for cross-program arbitration, bypassing the Steering Committee queue given the time-sensitivity such conflicts typically carry.

## Relationship to Delivery Governance

The ARB governs architecture; it does not run agile delivery ceremonies or manage the program plan — that is the Program Director's function, tracked separately. The two intersect formally at architecture contracts (see [architecture-contracts.md](../07-phase-g-implementation-governance/architecture-contracts.md)), which translate ARB-approved designs into commitments a delivery team is measured against.

*Fictional case study — see [README](../README.md) for full disclaimer.*
