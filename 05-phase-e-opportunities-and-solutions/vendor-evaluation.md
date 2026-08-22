# Vendor Evaluation: Dealer Management System (DMS) Core Platform

## Purpose

This evaluation covers the "Buy" solution building block identified as highest program risk — the Commercial DMS Core Platform (see [solution-building-blocks.md](./solution-building-blocks.md)) — since it underpins Inventory, Sales Workflow, and Service Scheduling. Four vendors were evaluated. Vendor names below are invented for this fictional case study and do not represent any real product.

## Candidates

- **Vendor A — "Meridian Drive Platform"**: cloud-native DMS platform, mid-market automotive focus, API-first architecture, 6 years in market.
- **Vendor B — "Ferrous DMS Suite"**: long-established DMS vendor with a large existing automotive customer base, hybrid cloud/on-prem deployment model, 20+ years in market.
- **Vendor C — "Northlane Retail Cloud"**: newer entrant, cloud-native, strong in EV-focused dealer groups, smaller implementation track record.
- **Vendor D — "Cascade Dealer OS"**: mid-size vendor, cloud-native, modular architecture, moderate market share in Torvane's operating regions.

## Weighted Evaluation Criteria

| Criterion | Weight | Vendor A | Vendor B | Vendor C | Vendor D |
|---|:---:|:---:|:---:|:---:|:---:|
| Real-time inventory/event API capability | 20% | 8 | 4 | 9 | 7 |
| Multi-region cloud-native architecture | 15% | 8 | 3 | 9 | 7 |
| Automotive/dealer domain fit (out-of-box workflows) | 15% | 7 | 9 | 6 | 7 |
| Integration flexibility (event backbone compatibility) | 15% | 8 | 4 | 8 | 7 |
| Implementation track record at Torvane's scale (600 dealers, multi-country) | 15% | 6 | 9 | 4 | 6 |
| Total cost of ownership (licensing + implementation) | 10% | 6 | 5 | 7 | 8 |
| Vendor lock-in / exit cost risk | 5% | 6 | 4 | 6 | 7 |
| Security & compliance posture (multi-country data residency) | 5% | 7 | 8 | 6 | 7 |

### Weighted Scores

| Vendor | Weighted Score (of 10) |
|---|:---:|
| **Vendor A — Meridian Drive Platform** | **7.30** |
| Vendor B — Ferrous DMS Suite | 5.85 |
| Vendor C — Northlane Retail Cloud | 7.15 |
| Vendor D — Cascade Dealer OS | 7.00 |

Calculation shown for the winning vendor as an example: (8×0.20)+(8×0.15)+(7×0.15)+(8×0.15)+(6×0.15)+(6×0.10)+(6×0.05)+(7×0.05) = 1.60+1.20+1.05+1.20+0.90+0.60+0.30+0.35 = **7.30**.

## Recommendation

**Vendor A (Meridian Drive Platform)** is recommended. It scored highest overall and, critically, scored strongly across the three criteria the ARB weighted most heavily given this program's specific problem (real-time API capability, multi-region architecture, integration flexibility — a combined 50% of total weight), reflecting that Torvane's core problem is architectural (batch, monolithic, non-event-driven) rather than a gap in dealer workflow functionality per se.

## Why the Runners-Up Lost

- **Vendor C (Northlane Retail Cloud)** scored a very close second (7.15) and in fact edged out Vendor A on raw technical architecture criteria. It lost on **implementation track record** (a 4/10, the lowest score in that category across all vendors) — Northlane's largest existing deployment is roughly 80 dealers, well short of Torvane's 600-dealer, multi-country requirement, and the ARB judged the delivery risk of being Northlane's largest-ever implementation, on a program with a hard 3-year timeline, to be a risk not adequately compensated for by its architectural edge over Vendor A.
- **Vendor D (Cascade Dealer OS)** was a credible, low-risk middle option (7.00) with the best TCO score, but its real-time API capability (7/10) and integration flexibility (7/10) were both a full point behind Vendor A's, and given those two criteria's combined 35% weight, the gap was enough to change the ranking. Cascade remains the documented fallback option should Vendor A contract negotiations fail.
- **Vendor B (Ferrous DMS Suite)** scored highest on domain fit and implementation track record — unsurprising given 20+ years of automotive DMS deployments — but its hybrid on-prem architecture and low event-API scores (4/10 on two of the three highest-weighted criteria) make it a poor architectural fit for a program whose entire premise is moving away from the batch/on-prem pattern Ferrous represents. Selecting Ferrous would have meant re-litigating Principle 8 (Cloud-Native by Default) for the single largest system in the program, which the ARB was not willing to do.

## Trade-offs Accepted With Vendor A

Vendor A's implementation track record score (6/10) is not exceptional — it has completed multi-country automotive rollouts but nothing at Torvane's exact scale. This is treated as an accepted, monitored risk: the architecture contract with Vendor A (see [architecture-contracts.md](../07-phase-g-implementation-governance/architecture-contracts.md)) includes explicit implementation milestones and a defined off-ramp to Vendor D if Wave 1 delivery milestones are missed by more than one full quarter.

*Fictional case study — see [README](../README.md) for full disclaimer.*
