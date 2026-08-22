# Change Management Plan

## Purpose

Phase H addresses the organizational change required for the modernization program to actually deliver its projected benefits — the business case's savings and ROI (see [business-case.md](../01-phase-a-vision-and-scope/business-case.md)) depend on dealer staff and internal teams actually adopting the new tools and processes, not merely on the technology being deployed. This plan was scoped against the "Dealer Change Adoption / Training Capability" gap identified in the capability map (maturity 2→3), a deliberately modest target reflecting a realistic near-term ceiling for a 600-dealer, multi-country training effort.

## Organizational Change Impact

| Affected Group | Nature of Impact | Severity |
|---|---|---|
| Dealer sales staff | New inventory workflow with real-time cross-dealer visibility and transfer recommendations; UI change | Medium — workflow change, not role change |
| Dealer service staff | New parts ETA visibility at point of service booking; service scheduling module changes | Medium |
| Dealer back-office/admin staff | Reduced manual reconciliation work (previously required due to inventory staleness) | Low-Medium — net reduction in manual effort, but requires trust-building in new system's accuracy |
| Torvane parts operations planners | Shift from batch EDI monitoring to real-time exception-based monitoring | High — meaningful role change from periodic batch review to continuous monitoring |
| Torvane data operations team (legacy MDM reconciliation) | Manual nightly matching scripts retired as Vehicle MDM Service takes over | High — role is substantially redefined; requires redeployment planning, addressed with HR partnership outside this document's scope |
| Cloud Platform Engineering (new function) | Net-new team responsibilities; the capability map's largest maturity gap (1→4) | High — hiring and skills build-out required, tracked jointly with HR |
| IT support / helpdesk | Must support both legacy and target systems during the T2 transition state ([transition-architectures.md](../06-phase-f-migration-planning/transition-architectures.md)) | Medium — temporary dual-system burden |

## Training Plan

Training is wave-aligned, not delivered once program-wide, since dealer-facing changes reach different dealers at different times per the migration roadmap:

- **Pre-cutover training (per wave):** a mandatory 4-hour session (2 hours in-person or live virtual, 2 hours self-paced module) delivered to each dealer's sales, service, and admin staff no more than 3 weeks before their region's cutover date — close enough that the training is fresh, far enough to allow a follow-up session if gaps are found.
- **Train-the-trainer model:** given 600 dealers, direct Torvane-led training does not scale; each dealer designates a "champion" who receives deeper training and is the first point of contact for peer questions post-cutover, with Torvane trainers as backup.
- **Role-specific tracks for internal teams:** parts operations planners and the data operations team (the two highest-severity-impact internal groups) receive dedicated multi-week transition programs rather than a single session, including shadowing periods during their function's specific migration wave.
- **Just-in-time reference materials:** short-form video and searchable reference documentation available in the Dealer Portal itself, addressing the reality that classroom training retention for infrequent workflows (like a rare inventory conflict resolution) is low.

## Communication Plan

| Audience | Channel | Cadence | Content Focus |
|---|---|---|---|
| Dealer Network (all) | Dealer Network Advisory Council briefings + email bulletin | Quarterly + wave-specific pre-cutover notices | Program progress, upcoming cutover dates, what's changing |
| Dealer champions | Dedicated channel (community forum + direct trainer contact) | Ongoing | Deeper technical detail, early access to release notes |
| Internal Torvane staff (all functions) | All-hands updates from CDTO sponsor | Semi-annual | Program milestones, business case progress against targets |
| Affected internal teams (parts ops, data ops) | Direct team briefings from function leadership | Monthly during their transition wave | Role change specifics, redeployment/reskilling plans |
| Executive Steering Committee | Formal program status report | Monthly | Budget, risk, milestone status against roadmap |

## Adoption Metrics

Adoption is tracked distinctly from the technical success metrics in [vision-and-scope.md](../01-phase-a-vision-and-scope/vision-and-scope.md) — a system can be live and technically functioning while still being under-adopted, and the two failure modes require different responses.

| Metric | Target | Cadence |
|---|---|---|
| Dealer champion training completion rate (pre-cutover) | 100% per wave before cutover proceeds | Per wave, gating criterion |
| Post-cutover active usage rate (new inventory/parts modules vs. legacy fallback where still available) | ≥ 85% within 60 days of cutover | 60/90-day post-cutover checkpoints |
| Dealer support ticket volume related to new system, per dealer | Declining trend, no more than 3 tickets/dealer in first 30 days | Monthly, per wave cohort |
| Internal role-transition team retention/redeployment completion (data ops, parts ops) | 100% placed in redefined or new roles within 90 days of their team's transition | Tracked jointly with HR, reported to Steering Committee |
| Dealer Network Satisfaction Survey score (inventory/parts) | +20 points cumulative by program end (ties to business case target) | Annual |

A wave's Post-Go-Live Checkpoint (per [governance-framework.md](../07-phase-g-implementation-governance/governance-framework.md)) explicitly includes adoption metrics alongside technical performance metrics — a wave that hits its latency targets but shows low active usage is treated as requiring remediation, not as a completed success, since low adoption directly undermines the business case the program was funded against.

*Fictional case study — see [README](../README.md) for full disclaimer.*
