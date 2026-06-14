# Gap Analysis — Loan Approval

This document inventories inefficiencies in the As-Is process and classifies each by type, impact, and root cause. Each gap is assigned a stable ID (`GAP-NN`) used downstream in the [requirements traceability matrix](03-requirements-traceability.md).

## Gap Inventory

| ID | Gap | Type | As-Is Step | Impact | Root Cause |
|---|---|---|---|---|---|
| **GAP-01** | Dual data entry (paper + CBS) | Manual handoff / data quality | Step 1 — Intake | ~35 min/application; 8% transcription errors | No digital intake channel; legacy paper form |
| **GAP-02** | Document completeness only caught at branch | Rework | Step 2 — Verification | 22% return-visit rate; customer friction | No upfront checklist / validation logic |
| **GAP-03** | Manual credit bureau lookup via web portal | Manual handoff / integration gap | Step 3 — Credit pull | 15–20 min/file; mis-routed emails | No API integration with bureau |
| **GAP-04** | FIFO shared-inbox queue, no prioritization | Bottleneck | Step 4 — Underwriting pickup | 3-day median queue wait | No workflow / case management system |
| **GAP-05** | DSR calculation in ad-hoc Excel sheets | Inconsistency / risk | Step 4 — Underwriting | Inconsistent risk decisions; audit weakness | No standardized rules engine |
| **GAP-06** | Compliance review is serial (after UW) | Serialization bottleneck | Step 5 — Compliance | 12% rework when Compliance rejects post-UW | Process designed sequentially |
| **GAP-07** | Wet-ink signature for BM approval | Manual handoff / delay | Step 6 — BM sign-off | 1–2 day courier delay; lost pages | No e-signature workflow |
| **GAP-08** | Redundant approval — UW + Compliance + BM all sign | Redundant approval | Steps 4–6 | Over-control on low-risk files (<$15K) | Risk policy not tiered |
| **GAP-09** | In-person customer signing required | Customer experience / drop-off | Step 7 — Disbursement | 9% post-approval abandonment | No remote ID verification or e-sign |
| **GAP-10** | Rejection notified by paper mail | Customer experience / compliance | Step 8 — Rejection | Slow adverse-action notice; potential regulatory exposure | No customer-facing portal |
| **GAP-11** | No real-time status visibility for applicant | Transparency | Whole process | Inbound call volume; NPS impact | No applicant portal |
| **GAP-12** | No audit trail across paper handoffs | Compliance risk | Whole process | Difficulty proving regulator timelines | Hybrid paper/digital trail |

## Severity Heat-map

| Severity | Gaps |
|---|---|
| 🔴 High | GAP-03, GAP-04, GAP-06, GAP-09, GAP-12 |
| 🟠 Medium | GAP-01, GAP-02, GAP-05, GAP-07, GAP-10 |
| 🟡 Low | GAP-08, GAP-11 |

Severity is a function of cycle-time impact, customer-experience cost, and regulatory exposure.

## Themes

1. **Integration absence** — bureau and signature systems are not wired to the CBS (GAP-03, GAP-07).
2. **Sequential bottlenecks** — work that could run in parallel does not (GAP-06).
3. **Paper inertia** — physical artifacts drive courier delays and audit gaps (GAP-01, GAP-07, GAP-12).
4. **Customer experience** — limited self-service produces drop-off and call volume (GAP-09, GAP-10, GAP-11).

These themes shape the To-Be design in [to-be-bpmn.md](../diagrams/to-be-bpmn.md).
