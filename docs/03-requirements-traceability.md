# Requirements Traceability Matrix

Each gap from the [gap analysis](02-gap-analysis.md) is mapped to one or more system requirements (functional **FR** or non-functional **NFR**) and the BPMN element in the [To-Be diagram](../diagrams/to-be-bpmn.md) that realises it.

| Gap ID | Gap Summary | Requirement ID | Type | Requirement Statement | To-Be BPMN Element |
|---|---|---|---|---|---|
| GAP-01 | Dual paper + CBS data entry | FR-01 | Functional | The system shall provide a web/mobile digital application form that writes directly to the core banking system with no rekeying. | `SYS1` |
| GAP-01 | Transcription errors | FR-02 | Functional | The system shall OCR-extract data from uploaded ID and pay stubs and pre-populate the application. | `SYS2` |
| GAP-02 | Missing documents caught late | FR-03 | Functional | The system shall enforce a document checklist at submission and block submission until mandatory artifacts are uploaded. | `SYS1` → `SYS3` |
| GAP-03 | Manual bureau lookup | FR-04 | Functional | The system shall integrate with the credit bureau via REST API and retrieve credit report + score within 5 seconds. | `API1` |
| GAP-03 | Mis-routed bureau emails | NFR-01 | Non-functional (Security) | Bureau payloads shall be transmitted over TLS 1.3 with mutual auth; no PII transits via email. | `API1` |
| GAP-04 | FIFO shared-inbox queue | FR-05 | Functional | The system shall provide a workflow / case management tool with risk-weighted prioritization of the underwriter queue. | `UW1` task in `PARALLEL` |
| GAP-05 | Ad-hoc Excel DSR | FR-06 | Functional | The system shall calculate debt-service ratio and risk score via a centralized rules engine with versioned policy. | `RULES` |
| GAP-05 | Audit weakness | NFR-02 | Non-functional (Auditability) | All risk-decision inputs and outputs shall be persisted immutably for 7 years. | `AUDIT` |
| GAP-06 | Serial Compliance after UW | FR-07 | Functional | The system shall route applications to Underwriting and Compliance in parallel via an AND-split gateway and join only when both decisions are recorded. | `PARALLEL` (AND-split / AND-join) |
| GAP-07 | Wet-ink BM signature | FR-08 | Functional | The system shall provide qualified electronic signature capability for Branch Manager approval. | `BM1` |
| GAP-08 | Redundant approvals on small loans | FR-09 | Functional | The system shall auto-approve applications ≤ $15,000 that pass the rules engine without human review. | `TIER` → `AUTO1` |
| GAP-09 | In-person customer signing | FR-10 | Functional | The system shall enable remote identity verification and customer e-signature compliant with PIPEDA / eIDAS-equivalent. | `CUST1` |
| GAP-09 | Post-approval drop-off | FR-11 | Functional | The system shall send automated e-sign reminders at 24h and 72h after issuance. | `REMIND` |
| GAP-10 | Slow rejection notice | FR-12 | Functional | The system shall deliver adverse-action notices via portal + email within 60 seconds of a rejection decision, including specific reason codes. | `REJ1` |
| GAP-11 | No applicant visibility | FR-13 | Functional | The system shall expose a customer portal showing real-time application status and required actions. | Covered by `SYS1` channel + `REMIND` |
| GAP-11 | Inbound call volume | NFR-03 | Non-functional (Usability) | Customer portal shall achieve SUS score ≥ 80 in usability testing. | Portal (cross-cutting) |
| GAP-12 | No end-to-end audit trail | NFR-04 | Non-functional (Compliance) | The system shall maintain an immutable, append-only audit log of every state transition with actor, timestamp, and payload hash. | `AUDIT` |
| All | End-to-end SLA | NFR-05 | Non-functional (Performance) | 95% of low-risk applications shall reach disbursement within 2 business days. | Cross-cutting |
| All | Availability | NFR-06 | Non-functional (Availability) | Customer-facing portal and APIs shall maintain 99.9% monthly availability. | Cross-cutting |

## Coverage Check

| Gap | Covered? |
|---|---|
| GAP-01 → GAP-12 | ✅ all gaps have at least one mapped requirement and BPMN element |

## How to read this matrix

- **FR** = functional requirement (something the system does).
- **NFR** = non-functional requirement (a quality attribute the system must exhibit).
- A single gap may produce multiple requirements (one functional + one quality constraint, e.g. GAP-03 → FR-04 + NFR-01).
- Cross-cutting NFRs (NFR-05, NFR-06) are not tied to a single BPMN element but constrain the whole process.
