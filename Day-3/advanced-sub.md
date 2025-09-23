# Governance & RBAC Lab Guide (GUI step-by-step)

This guide now includes multiple scenarios for corporate employees. Each section is **click-by-click** navigation in Azure Portal.

---

## Intermediate Level

### Scenario 1: RBAC at Different Scopes

**Story:** HR team should manage payroll VM but not production DB. Assign Contributor at RG scope, Reader at Subscription scope.
**Lab:** Create user `hruser@company.com`, assign roles, test access.
**Outcome:** Learners practice fine-grained RBAC.

👉 *(Steps already documented earlier in this guide.)*

---

### Scenario 2: Governance with Management Groups

**Story:** Org has 3 subscriptions → Dev, Test, Prod. Add them under a Management Group for centralized governance.
**Lab:** Create Management Group, link subscriptions.
**Outcome:** Learners see consolidated control at scale.

👉 *(Steps already documented earlier in this guide.)*

---

### Scenario 3: Tagging & Cost Analysis

**Story:** Apply tags Dept=Finance, Env=Prod. Run cost analysis by tag.
**Lab:** Add tags to RGs & resources. Use Cost Analysis in portal.
**Outcome:** Learners understand tracking cost per department/project.

👉 *(Steps already documented earlier in this guide.)*

---

## Advanced Level

### Scenario 1: Multi-Subscription Billing Strategy

**Story:** A multinational org has 10 subscriptions in different regions. Consolidate billing to one invoice.
**Lab:** Use Cost Management to link subscriptions & analyze combined billing.
**Outcome:** Learners see how enterprises simplify cost visibility.

---

### Part 1 — Verify billing account access

1. Sign in to **[https://portal.azure.com](https://portal.azure.com)** with a **Billing Administrator** or **Owner** role.
2. In the search bar, type **Cost Management + Billing** and open it.
3. Confirm you can see all 10 subscriptions under your tenant. If not, ensure they’re all associated with the same Azure AD directory and billing account.

---

### Part 2 — Consolidate billing (Enrollment or Billing Account)

1. In **Cost Management + Billing**, select **Billing scopes**.
2. Choose the **Billing account** or **Enrollment account** that covers your organization.
3. Verify that all 10 subscriptions are listed.

   * If not, link subscriptions to the billing account by following prompts: **Add subscription** → select tenant → confirm.
4. Once linked, all subscriptions will roll up to a single consolidated invoice.

---

### Part 3 — Run consolidated cost analysis

1. In the **Cost Management + Billing** blade, click **Cost Management** → **Cost analysis**.
2. At the top, set the **Scope** to the **Billing account** (not a single subscription).
3. Verify costs from all 10 subscriptions appear combined.
4. Use the **Group by** option to split costs by **Subscription name** or **Resource group**.
5. Use **Filters** to analyze costs per region or department.

---

### Part 4 — Verification for learners

* Learners must show a screenshot of **Cost analysis** at the **Billing account scope** with all subscriptions included.
* Learners should highlight cost breakdown per subscription to confirm consolidation.

**Expected outcome:** One consolidated invoice covers all 10 subscriptions, and costs are visible in a single view.

---

### Part 5 — Optional exercises

* Export the consolidated cost report to CSV/Excel.
* Build a Power BI dashboard from **Cost Management exports**.
* Apply **Tags** or **Management groups** to further refine cost rollups.

---

### Cleanup (if required)

* No cleanup is needed. Billing scope changes persist for enterprise visibility.

---

### Assessment rubric

* **Pass** if learner demonstrates consolidated billing with all 10 subscriptions in a single cost view.
* **Bonus:** Provides exported CSV or Power BI dashboard.

---

✅ The guide now covers:

* **Intermediate Level:** RBAC, Management Groups, Tagging/Cost Analysis
* **Advanced Level:** Multi-Subscription Billing Strategy
