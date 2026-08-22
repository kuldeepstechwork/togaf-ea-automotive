# TOGAF Enterprise Architecture Case Study — Torvane Mobility Group

**Disclaimer:** This is an illustrative TOGAF Enterprise Architecture case study modeling common, publicly known challenges in automotive OEM mobility platforms — not a real engagement. Torvane Mobility Group is an invented name, not affiliated with any real company, and nothing here is based on confidential information from any real employer or client. All figures, vendor names, and technical details are constructed for this exercise.

## Program Overview

This repository documents a three-year Enterprise Architecture engagement for **Torvane Mobility Group**, a fictional mid-size automotive OEM (~40,000 vehicles/year) with a growing electric vehicle and connected-vehicle telematics business, sold and serviced through a network of roughly 600 franchised dealers across multiple countries. The artifacts here follow the TOGAF Architecture Development Method (ADM) end to end — from Preliminary Phase through Phase H — and represent the kind of work product an Enterprise/Solution Architecture function would produce to sponsor, govern, and steer a large-scale modernization program: principles, stakeholder maps, business and data architectures, reference architectures, vendor evaluations, migration roadmaps, and architecture decision records.

## The Business Problem

Torvane's core dealer management system (DMS) is a fifteen-year-old on-premises monolith that cannot support real-time inventory visibility across the dealer network. Its connected-vehicle telemetry pipeline began life as a bolt-on proof of concept and cannot scale past the current EV fleet's data volume. Its parts supply chain runs on batch EDI file exchange with 24–48 hour latency, which has become a competitive liability against EV-native entrants that offer dealers and customers real-time parts and inventory data. Leadership has mandated a three-year modernization program to replace these systems with a cloud-native, event-driven platform without disrupting dealer operations or vehicle production during the transition. This repository is the architecture function's record of how that program was scoped, governed, and sequenced.

## How to Navigate This Repository

Start with [TOGAF-ADM-MAPPING.md](./TOGAF-ADM-MAPPING.md) for a one-page index of every ADM phase and where its artifacts live. From there:

- [00-preliminary/](./00-preliminary/) — architecture principles and governance setup that precede scoping
- [01-phase-a-vision-and-scope/](./01-phase-a-vision-and-scope/) — vision, stakeholders, business case, executive summary
- [02-phase-b-business-architecture/](./02-phase-b-business-architecture/) — as-is/to-be business architecture, capability map
- [03-phase-c-information-systems-architecture/](./03-phase-c-information-systems-architecture/) — data and application architecture
- [04-phase-d-technology-architecture/](./04-phase-d-technology-architecture/) — reference architecture and technology standards
- [05-phase-e-opportunities-and-solutions/](./05-phase-e-opportunities-and-solutions/) — solution building blocks, vendor evaluation, gap analysis
- [06-phase-f-migration-planning/](./06-phase-f-migration-planning/) — migration roadmap and transition architectures
- [07-phase-g-implementation-governance/](./07-phase-g-implementation-governance/) — governance framework and architecture contracts
- [08-phase-h-change-management/](./08-phase-h-change-management/) — organizational change management plan
- [adrs/](./adrs/) — five Architecture Decision Records for the program's most consequential technical calls

## How to Read This Repo

Every document here is written in **decision voice, not build voice**. You will not find "we deployed a Kafka cluster" — you will find "we evaluated three integration patterns, selected an event-driven backbone, rejected point-to-point and shared-database integration for named reasons, and accepted a specific set of trade-offs in cost, timeline, and operational complexity, with sign-off required from the named governance body." That framing is deliberate: the deliverable of an Enterprise Architecture function is not code, it is a defensible decision with alternatives considered, trade-offs quantified, and stakeholders accountable for it. Figures throughout (costs, timelines, maturity scores, vendor ratings) are invented but held to a plausible, internally consistent standard — they exist to demonstrate the *reasoning method*, not to represent real financial data.

---
*Fictional case study — see disclaimer above for full context.*
