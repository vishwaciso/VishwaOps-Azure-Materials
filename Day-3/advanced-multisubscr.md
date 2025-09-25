🔹 Advanced Level — Multi-Subscription Billing Strategy
Scenario 1: Multi-Subscription Billing Strategy

Story:
A multinational organization has 10 Azure subscriptions across different regions. To simplify finance and reporting, the company wants to consolidate all subscriptions into one invoice and analyze combined billing in a single view.

Lab Goal:
Learners will practice consolidating subscription billing under a single billing account and running a consolidated cost analysis.

Outcome:
Learners will understand how enterprises achieve cost visibility at scale with Azure Cost Management + Billing.

🧪 Lab Guide
Part 1 — Verify Billing Account Access

Sign in to Azure Portal
 using an account with:

Billing Administrator role, or

Owner role at the billing account.

In the search bar, type Cost Management + Billing and open it.

Confirm you can view all 10 subscriptions.

If some are missing:

Ensure subscriptions are linked to the same Azure AD directory and Billing account.

Part 2 — Consolidate Billing (Enrollment or Billing Account)

In Cost Management + Billing, go to Billing scopes.

Select the Billing account or Enrollment account for your organization.

Verify all 10 subscriptions appear under this scope.

If not:

Click Add subscription → choose the tenant → confirm linking.

Once linked, Azure generates one consolidated invoice for all subscriptions.

Part 3 — Run Consolidated Cost Analysis

In the Cost Management + Billing blade, click Cost Management → Cost analysis.

At the top, set the Scope to the Billing account (⚠️ not an individual subscription).

Validate that costs from all 10 subscriptions are included.

Use tools to analyze:

Group by → Subscription name → compare costs across subscriptions.

Group by → Resource group → drill into specific workloads.

Filters → Region/Department → analyze per business unit.

Part 4 — Verification for Learners

✔ Learners must provide a screenshot of Cost analysis at the Billing account scope, showing all subscriptions included.
✔ Highlight the cost breakdown per subscription to prove consolidation.

Expected Outcome:

One consolidated invoice across 10 subscriptions.

Unified cost visibility in a single dashboard.

Part 5 — Optional Exercises

📤 Export costs → CSV/Excel for finance teams.

📊 Build a Power BI dashboard from exported data.

🏷 Apply Tags or Management Groups to refine rollups (e.g., Dept=Finance, Region=US).

🧹 Cleanup

No cleanup required.

Billing scope changes remain for enterprise visibility.
