🔹 Overall Outline — Governance Lab (Management Groups)
1. Goal

Create a centralized governance structure by placing Dev, Test, and Prod subscriptions under a single Management Group (Org-MG).

2. Steps

Enable Management Groups (if first-time use).

Check Root Management Group (Tenant root should be visible).

Create Org Management Group (Org-MG).

Move Subscriptions (Dev, Test, Prod) under Org-MG.

Verify Hierarchy (Learner sees all subscriptions under Org-MG).

Optional Governance

Assign RBAC role (e.g., Reader) at Org-MG and verify it cascades.

Assign a Policy (e.g., Allowed locations) at Org-MG and confirm inheritance.

Exercises

Screenshot of hierarchy tree.

Show cascading RBAC/Policy effects.

Cleanup (Move subscriptions back → Delete Org-MG).

🔹 Diagram — Management Group Governance Structure

Here’s the visual to explain:

                   ┌─────────────────────────┐
                   │   Tenant Root Group      │
                   └─────────────┬───────────┘
                                 │
                      ┌──────────┴──────────┐
                      │   Org-MG             │
                      │  (Org Management     │
                      │   Group)             │
                      └──────────┬──────────┘
                                 │
      ┌───────────────┬──────────┴───────────┬───────────────┐
      │               │                      │               │
┌──────────────┐  ┌──────────────┐      ┌──────────────┐
│ Dev          │  │ Test          │      │ Prod         │
│ Subscription │  │ Subscription  │      │ Subscription │
└──────────────┘  └──────────────┘      └──────────────┘


👉 Meaning:

Tenant Root Group = top of hierarchy (represents entire org/tenant).

Org-MG = parent governance node created by us.

Dev, Test, Prod Subscriptions = children that inherit RBAC + Policy assignments from Org-MG.
