# Loan Approval Process — SA Track

**BPMN Process Mapping + Gap Analysis** for a fictional retail bank ("Maple Trust Bank") loan approval workflow.

## Executive Summary

This repository demonstrates Systems Analyst (SA) deliverables for a retail loan approval transformation. The current ("As-Is") process at Maple Trust Bank averages **9–12 business days** end-to-end and depends heavily on manual credit pulls, paper-based approvals, and serial compliance review — producing bottlenecks, rework, and customer drop-off. Through process narrative, BPMN modelling, and a structured gap analysis, this project proposes a redesigned ("To-Be") workflow that introduces an automated credit scoring API, parallel compliance + underwriting review, and digital signature for disbursement, targeting a **≤ 2 business day** turnaround. A requirements traceability matrix links each identified gap to a functional or non-functional requirement and the BPMN element that addresses it, providing a defensible bridge from business problem to system design.

## Contents

| Deliverable | File |
|---|---|
| 1. Process Narrative | [docs/01-process-narrative.md](docs/01-process-narrative.md) |
| 2. As-Is BPMN Diagram | [diagrams/as-is-bpmn.md](diagrams/as-is-bpmn.md) |
| 3. Gap Analysis | [docs/02-gap-analysis.md](docs/02-gap-analysis.md) |
| 4. To-Be BPMN Diagram | [diagrams/to-be-bpmn.md](diagrams/to-be-bpmn.md) |
| 5. Requirements Traceability Matrix | [docs/03-requirements-traceability.md](docs/03-requirements-traceability.md) |

## Roles Modelled

- **Loan Officer** — application intake, document collection, customer-facing
- **Underwriter** — credit assessment, risk scoring, approval recommendation
- **Credit Bureau** (external) — credit history and score provider
- **Compliance Officer** — AML/KYC, regulatory review, policy adherence
- **Branch Manager** — final approval authority for loans above threshold

## Tooling

All diagrams use **Mermaid** BPMN-style notation so they render natively on GitHub — no external viewer required.

## Author

Sumit Jindal — Systems Analyst portfolio project.
