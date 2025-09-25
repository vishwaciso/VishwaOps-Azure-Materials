🔹 Overall Outline — Governance & RBAC Lab
Scenario 1: RBAC at Different Scopes

Goal: HR user can manage Payroll VM but cannot touch Production DB.

Action: Assign Contributor at Payroll-RG, Reader at Subscription.

Outcome: Fine-grained RBAC in action.

Scenario 2: Governance with Management Groups

Goal: Place Dev, Test, Prod subscriptions under a single Management Group (Org-MG).

Action: Create Org-MG, move subscriptions under it.

Outcome: Centralized governance at scale (RBAC/Policies cascade).

Scenario 3: Tagging & Cost Analysis

Goal: Apply Dept=Finance, Env=Prod tags to resources.

Action: Add tags to RGs & resources, run Cost Analysis grouped by tags.

Outcome: Cost transparency and accountability by department/environment.

🔹 Unified Diagram — Governance & RBAC
                          ┌────────────────────────────┐
                          │    Tenant Root Group        │
                          └──────────────┬─────────────┘
                                         │
                          ┌──────────────┴─────────────┐
                          │        Org-MG              │
                          │ (Management Group)          │
                          └───────┬─────────┬──────────┘
                                  │         │
              ┌───────────────────┘         └───────────────────┐
              │                                     │           │
   ┌───────────────────┐                ┌───────────────────┐   │
   │   Dev Subscription│                │   Test Subscription│   │
   └───────────────────┘                └───────────────────┘   │
                                                                 │
                                                        ┌───────────────────┐
                                                        │  Prod Subscription│
                                                        └─────────┬─────────┘
                                                                  │
                                                ┌─────────────────┴────────────────┐
                                                │                                  │
                                     ┌──────────────────────┐        ┌─────────────────────┐
                                     │  Payroll-RG          │        │  Prod-RG            │
                                     │ Contributor: HR User │        │ Reader: HR User     │
                                     └──────────┬───────────┘        └──────────┬──────────┘
                                                │                               │
                                        ┌─────────────┐                ┌─────────────────┐
                                        │ payroll-vm  │                │ prod-sql-server │
                                        │ (VM tags:   │                │ prod-db         │
                                        │ Dept=Finance│                │ (Tagged Env=Prod│
                                        │ Env=Prod)   │                │ Dept=Finance)   │
                                        └─────────────┘                └─────────────────┘

🔹 Key Takeaways for Learners

RBAC (Scenario 1) → Use least privilege (Contributor at RG, Reader at Subscription).

Management Groups (Scenario 2) → Enable centralized governance for multiple subscriptions.

Tagging & Cost Analysis (Scenario 3) → Track and analyze costs by department/environment.
