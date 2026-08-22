# Business Case

All figures in this document are illustrative and invented for this fictional case study, held to a plausible and internally consistent standard for demonstration purposes. They should not be read as representing real financial data.

## Cost Basis and Assumptions

- Blended fully-loaded rate for integration/engineering effort: **$14,500 per person-month** (covers salary, benefits, overhead; a mix of internal staff and contracted specialists).
- Program duration: 3 years (12 quarters), aligned to the Phase F migration roadmap.
- All figures in USD, rounded to the nearest $10K.
- "As-Is" costs are the projected 3-year run cost of the current DMS, telemetry, and EDI landscape if no modernization occurs (status quo baseline).
- "To-Be" costs are the 3-year cost of building and running the target architecture, inclusive of the migration program itself.

## As-Is 3-Year Run Cost (Status Quo Baseline)

| Line Item | Annual Cost | 3-Year Total |
|---|---:|---:|
| On-prem DMS hosting, hardware refresh amortization, and data center costs | $2,100,000 | $6,300,000 |
| DMS vendor maintenance & support contract | $1,450,000 | $4,350,000 |
| Legacy telemetry pipeline hosting and vendor fees | $680,000 | $2,040,000 |
| EDI network/VAN (value-added network) fees | $420,000 | $1,260,000 |
| Internal engineering effort — keep-the-lights-on maintenance (avg. 14 FTE-equivalent at blended rate) | $2,436,000 | $7,308,000 |
| Estimated annual cost of lost sales from inventory visibility gaps (conservative estimate, 0.3% of gross vehicle sales revenue affected) | $1,800,000 | $5,400,000 |
| **As-Is 3-Year Total** | | **$26,658,000** |

## To-Be 3-Year Cost (Modernization Program, Build + Run)

| Line Item | Basis | Total (3 yrs) |
|---|---|---:|
| Cloud infrastructure (multi-region, all environments) | Ramping from $180K/mo in Year 1 to $410K/mo by Year 3 as migration completes | $10,440,000 |
| Commercial platform licensing (DMS core platform, telematics ingestion platform — see [vendor-evaluation.md](../05-phase-e-opportunities-and-solutions/vendor-evaluation.md)) | Blended annual license across selected vendors | $5,850,000 |
| Integration & migration engineering effort | 210 person-months total across 3 years at $14,500/PM | $3,045,000 |
| New platform engineering/SRE build-out (avg. 10 FTE-equivalent, ramping) | Blended across 3 years | $3,915,000 |
| Change management, training, communications (Phase H) | Fixed program allocation | $1,200,000 |
| Data migration and cleansing effort (one-time) | 40 person-months at $14,500/PM | $580,000 |
| Contingency reserve (12% of above, per Steering Committee policy) | Standard program contingency | $3,003,000 |
| **To-Be 3-Year Total** | | **$28,033,000** |

## Comparing As-Is vs. To-Be Over 3 Years

At face value, the 3-year To-Be cost ($28.03M) is **higher** than the 3-year As-Is cost ($26.66M) by roughly $1.38M — modernization programs frequently look more expensive than the status quo when compared only within the funding window, and the Steering Committee explicitly asked that this not be hidden in the business case. The case for the program rests on what happens *after* Year 3, and on benefits the As-Is run-cost table does not fully capture.

### Steady-State Run Cost Comparison (Year 4 onward, annualized)

| | As-Is Annual Run Cost | To-Be Annual Run Cost (post-migration, steady state) |
|---|---:|---:|
| Infrastructure/licensing/support | $4,650,000 | $4,920,000 |
| Internal engineering (keep-the-lights-on vs. platform run) | $2,436,000 | $1,470,000 (smaller team; automated deployment reduces manual maintenance load) |
| Lost-sales cost from inventory visibility gap | $1,800,000 | $180,000 (residual, assumes gap reduced ~90% but not eliminated) |
| **Annual Total** | **$8,886,000** | **$6,570,000** |

Steady-state annual savings once the program completes: **$2,316,000/year**.

### Payback Period Calculation

Using the incremental 3-year program cost over the As-Is baseline ($1,378,000) against the steady-state annual savings ($2,316,000/year) realized starting in Year 4:

Payback period = Incremental program investment ÷ Annual steady-state savings
Payback period = $1,378,000 ÷ $2,316,000/year ≈ **0.59 years (~7 months) after go-live**

Because savings only begin accruing at full run-rate after the final migration wave completes (end of Year 3, per the roadmap), the effective payback point relative to program start is approximately **Year 3, Month 7**.

### 5-Year Total Cost of Ownership View

Extending both scenarios two years past the program (Years 4–5 at steady-state annual run rate):

- As-Is 5-year TCO: $26,658,000 + (2 × $8,886,000) = **$44,430,000**
- To-Be 5-year TCO: $28,033,000 + (2 × $6,570,000) = **$41,173,000**

5-year net savings from modernization: **$3,257,000**, with the gap widening every year thereafter since the To-Be steady-state run rate is $2.3M/year cheaper.

## Return on Investment (ROI)

Using the 5-year view as the evaluation horizon (appropriate given the payback point falls late in Year 3):

ROI = (5-Year Net Benefit − Incremental Investment) ÷ Incremental Investment
Net Benefit = $3,257,000 (5-yr savings) + $5,400,000 − $900,000 (partial recapture of lost-sales cost already counted above — not double-counted; the $3,257,000 figure already nets this out)

To avoid double-counting, the ROI is calculated directly from the 5-year TCO delta against the incremental 3-year investment:

ROI = $3,257,000 ÷ $1,378,000 ≈ **236% over 5 years**, or roughly **47% annualized** over the 5-year horizon.

## Risk-Adjusted View

The Finance Business Partner requested a downside case assuming migration runs 20% over the contingency-adjusted budget and steady-state savings are 25% lower than modeled (slower dealer adoption). Under that downside case, payback extends to approximately **Year 4, Month 4**, and 5-year ROI falls to approximately **95%** — still net positive, which the Steering Committee treated as the deciding factor in approving the program at the Phase A gate.

*Fictional case study — see [README](../README.md) for full disclaimer.*
