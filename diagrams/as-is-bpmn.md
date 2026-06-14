# As-Is BPMN — Loan Approval (Current State)

Mermaid BPMN-style swimlane diagram. Pain-point steps are highlighted in red.

```mermaid
flowchart TD
    Start([Customer submits application]) --> LO1[LO: Paper form intake<br/>+ photocopy IDs]
    LO1 --> LO2[/LO: Dual entry into CBS/]
    LO2 -.pain.-> P1{{"Pain: 35 min, 8% errors"}}
    LO2 --> LO3{Documents complete?}
    LO3 -- No --> LO4[Call customer, schedule return visit]
    LO4 -.pain.-> P2{{"Pain: 22% return-visit rate"}}
    LO4 --> LO1
    LO3 -- Yes --> LO5[/LO: Manual login to Credit Bureau portal/]
    LO5 --> LO6[/Download PDF, email to UW inbox/]
    LO6 -.pain.-> P3{{"Pain: no API, mis-routed emails"}}
    LO6 --> UW1[UW: Pull next file FIFO from shared inbox]
    UW1 -.pain.-> P4{{"Pain: 3-day median queue wait"}}
    UW1 --> UW2[UW: Calculate DSR in Excel,<br/>write recommendation memo]
    UW2 --> UW3{Recommend approve?}
    UW3 -- No --> REJ1[Paper rejection letter mailed]
    REJ1 -.pain.-> P5{{"Pain: no real-time adverse-action notice"}}
    REJ1 --> EndR([End: Rejected])
    UW3 -- Yes --> CO1[CO: AML / KYC / sanctions review]
    CO1 -.pain.-> P6{{"Pain: serial review, 12% rework"}}
    CO1 --> CO2{Compliance pass?}
    CO2 -- No --> REJ1
    CO2 -- Yes --> AMT{Loan > $25K?}
    AMT -- No --> DISB1[Disbursement Clerk prepares agreement]
    AMT -- Yes --> BM1[Courier file to originating branch]
    BM1 -.pain.-> P7{{"Pain: 1-2 day courier delay"}}
    BM1 --> BM2[BM: Wet-ink signature]
    BM2 --> BM3[Courier back to hub]
    BM3 --> DISB1
    DISB1 --> DISB2[Customer returns to branch in person to sign]
    DISB2 -.pain.-> P8{{"Pain: 9% post-approval drop-off"}}
    DISB2 --> DISB3{Customer signs?}
    DISB3 -- No --> EndD([End: Abandoned])
    DISB3 -- Yes --> DISB4[Funds released to deposit account]
    DISB4 --> EndA([End: Disbursed])

    classDef pain fill:#ffe5e5,stroke:#c0392b,color:#c0392b,font-style:italic
    class P1,P2,P3,P4,P5,P6,P7,P8 pain
```

## Swimlane View (Roles)

```mermaid
flowchart LR
    subgraph Customer
        C1([Submit application]) --> C2([Return to sign])
    end
    subgraph LoanOfficer
        L1[Paper intake] --> L2[Dual CBS entry] --> L3[Verify docs] --> L4[Manual bureau pull] --> L5[Email to UW]
    end
    subgraph Underwriter
        U1[FIFO pickup] --> U2[DSR + memo] --> U3{Recommend?}
    end
    subgraph Compliance
        K1[AML / KYC] --> K2{Pass?}
    end
    subgraph BranchManager
        B1[Wet-ink sign > 25K]
    end
    subgraph Disbursement
        D1[Prepare agreement] --> D2[Release funds]
    end

    C1 --> L1
    L5 --> U1
    U3 -- yes --> K1
    K2 -- yes --> B1
    B1 --> D1
    D1 --> C2 --> D2
```

**Legend**
- Red italic notes = identified pain points (cross-referenced in [gap analysis](../docs/02-gap-analysis.md)).
- `[/.../]` shapes denote manual / non-automated activities.
