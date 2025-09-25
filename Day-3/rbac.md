🔹 Overall Outline — RBAC Lab (GUI)
1. Goal

HR user (hruser@company.com) should:

✅ Manage Payroll VM(s) in Payroll-RG

❌ Not modify Production DB in Prod-RG

2. Steps

Create HR User

In Azure AD → Users → Add hruser@company.com

Create Resource Groups

Payroll-RG (for VM)

Prod-RG (for SQL Server/DB)

Create Resources

Small VM (payroll-vm) in Payroll-RG

SQL Server + Database (prod-sql-server / prod-db) in Prod-RG

Assign Roles

Reader → at Subscription scope

Contributor → at Payroll-RG scope

Testing

HR user can start/stop VM in Payroll-RG

HR user cannot modify SQL DB in Prod-RG

Lab Exercise

Screenshot successful VM action

Screenshot permission denied on Prod DB

Verify role assignments in Access control (IAM)

Cleanup

Delete RGs + test user

🔹 Diagram — RBAC Scope Visualization

Here’s a simple diagram to explain:

                 ┌─────────────────────────┐
                 │     Subscription         │
                 │  (Reader for HR User)    │
                 └─────────────┬───────────┘
                               │
     ┌─────────────────────────┴─────────────────────────┐
     │                                                   │
┌───────────────┐                              ┌────────────────┐
│   Payroll-RG  │                              │    Prod-RG     │
│ Contributor   │                              │ (No extra role │
│ for HR User   │                              │  → Reader only)│
└──────┬────────┘                              └───────┬────────┘
       │                                               │
┌───────────────┐                          ┌────────────────────┐
│  payroll-vm   │                          │  prod-sql-server   │
│  (VM actions) │                          │  prod-db           │
└───────────────┘                          └────────────────────┘


👉 Meaning:

At Subscription level → HR User = Reader (can only view everything).

At Payroll-RG level → HR User = Contributor (can manage only those resources).

At Prod-RG level → HR User stays as Reader only (cannot edit DB).
