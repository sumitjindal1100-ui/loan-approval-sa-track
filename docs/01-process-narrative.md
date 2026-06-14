# Process Narrative — Loan Approval (As-Is)

**Organization:** Maple Trust Bank (fictional retail bank, ~80 branches)
**Product in scope:** Personal unsecured loans, CAD $5,000 – $50,000
**Document owner:** Systems Analyst track
**Version:** 1.0

## 1. Purpose

This narrative documents the current end-to-end loan approval process at Maple Trust Bank, from customer application through disbursement or rejection. It establishes the baseline for the gap analysis and To-Be redesign.

## 2. Actors

| Role | Responsibility |
|---|---|
| **Customer (Applicant)** | Submits loan application and supporting documents |
| **Loan Officer (LO)** | Branch-based intake, document review, data entry into core banking system |
| **Underwriter (UW)** | Centralized credit risk assessment and approval recommendation |
| **Credit Bureau** | External provider (Equifax / TransUnion) — credit report and FICO-equivalent score |
| **Compliance Officer (CO)** | AML / KYC review, sanctions screening, regulatory sign-off |
| **Branch Manager (BM)** | Final approval authority for loans > $25,000 |
| **Disbursement Clerk** | Funds release and account credit |

## 3. Process Flow (Current State)

### Step 1 — Application Intake (Day 0)
The customer visits a branch and meets the Loan Officer. The LO completes a paper application form (12 pages) capturing personal, employment, and income data. The LO photocopies the customer's ID, two pay stubs, and the most recent tax slip. The form is then manually keyed into the core banking system (CBS). **Pain point:** dual entry — paper + CBS — averaging 35 minutes per application; transcription errors observed in ~8% of files.

### Step 2 — Document Verification (Day 0–1)
The LO physically reviews documents for completeness. Missing documents trigger a phone call to the customer and a follow-up visit. **Pain point:** ~22% of applications require a return visit.

### Step 3 — Credit Bureau Pull (Day 1–2)
The LO logs in to the Credit Bureau web portal, manually keys the applicant's SIN and DOB, downloads the credit report as PDF, and emails it to the Underwriting team's shared inbox. **Pain point:** manual lookup, copy-paste, no API integration; reports occasionally emailed to wrong queue.

### Step 4 — Underwriting Review (Day 2–5)
An Underwriter pulls the next file from the shared inbox FIFO queue. The UW reviews the credit report, calculates debt-service ratios in Excel, and writes a recommendation memo. Files are worked **serially** in order received. **Pain point:** queue depth averages 40 files; 3-day median wait before pickup.

### Step 5 — Compliance Review (Day 5–7)
After Underwriting recommends approval, the file is forwarded to Compliance for AML / KYC and sanctions screening. Compliance reviews **after** Underwriting completes — no parallelism. **Pain point:** ~12% of files are rejected at this stage for issues that could have been caught earlier (e.g., PEP match), causing complete rework.

### Step 6 — Branch Manager Sign-off (Day 7–8)
For loans > $25,000, the file returns to the originating branch for the Branch Manager's wet-ink signature. Files are couriered between branches and the central underwriting hub. **Pain point:** courier delays of 1–2 days; signature page occasionally lost.

### Step 7 — Disbursement (Day 8–12)
Disbursement Clerk receives the approved file, prepares the loan agreement, the customer returns to the branch to sign in person, and funds are released to the customer's deposit account. **Pain point:** in-person signing requirement causes customer drop-off — ~9% of approved customers never complete signing.

### Step 8 — Rejection Path
Rejected applicants receive a paper letter by mail within 10 business days. **Pain point:** no adverse-action explanation provided in real time; customer-experience cost.

## 4. Volumetrics

| Metric | Current Value |
|---|---|
| Applications per month | ~2,400 |
| Median time-to-decision | 7 business days |
| Median time-to-disbursement | 9–12 business days |
| Approval rate | 61% |
| Post-approval drop-off | 9% |
| Compliance-stage rejection rate | 12% (of files reaching that stage) |
| Manual rework rate | ~18% |

## 5. Key Pain Points (Summary)

1. **Dual data entry** — paper + CBS, transcription errors.
2. **Manual credit bureau lookup** — no API; email handoff.
3. **Serial review** — Compliance only after Underwriting; rework when Compliance rejects.
4. **Paper-based BM approval** — courier delays, lost signatures.
5. **In-person signing** — 9% drop-off after approval.
6. **No real-time customer visibility** — rejection letters by mail.

These pain points drive the gap analysis in [02-gap-analysis.md](02-gap-analysis.md).
