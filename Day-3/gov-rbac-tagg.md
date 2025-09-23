# Governance & RBAC Lab Guide (GUI step-by-step)

This guide now includes multiple scenarios for corporate employees. Each section is **click-by-click** navigation in Azure Portal.

---

## Scenario 1: RBAC at Different Scopes

**Story:** HR team should manage payroll VM but not production DB. Assign Contributor at RG scope, Reader at Subscription scope.
**Lab:** Create user `hruser@company.com`, assign roles, test access.
**Outcome:** Learners practice fine-grained RBAC.

👉 *(Steps already documented in earlier section of this guide.)*

---

## Scenario 2: Governance with Management Groups

**Story:** Org has 3 subscriptions → Dev, Test, Prod. Add them under a Management Group for centralized governance.
**Lab:** Create Management Group, link subscriptions.
**Outcome:** Learners see consolidated control at scale.

👉 *(Steps already documented in earlier section of this guide.)*

---

## Scenario 3: Tagging & Cost Analysis

**Story:** Apply tags Dept=Finance, Env=Prod. Run cost analysis by tag.
**Lab:** Add tags to RGs & resources. Use Cost Analysis in portal.
**Outcome:** Learners understand tracking cost per department/project.

---

### Part 1 — Apply tags at Resource Group level

1. Sign in to **[https://portal.azure.com](https://portal.azure.com)**.
2. In the search bar, type **Resource groups** → open the list.
3. Select an existing RG (e.g., `Finance-RG`).
4. In the left menu, click **Tags**.
5. Click **+ Add** → Enter the following:

   * Name: `Dept` → Value: `Finance`
   * Name: `Env` → Value: `Prod`
6. Click **Apply**.
7. Verify the tags appear on the RG.

---

### Part 2 — Apply tags at individual resource level

1. In the Resource group blade, click on a specific resource (e.g., a VM or Storage account).
2. In the left menu, click **Tags**.
3. Add the same tags:

   * `Dept=Finance`
   * `Env=Prod`
4. Click **Save**.
5. Confirm tags are applied.

*(Note: Tags applied at the RG level do not automatically cascade to resources — they must be inherited at creation or added manually.)*

---

### Part 3 — Run Cost Analysis by tags

1. In the portal search bar, type **Cost Management + Billing**.
2. In the left menu, click **Cost Management** → **Cost analysis**.
3. In the **Scope**, select your subscription.
4. In the toolbar, click **Group by** → select **Tag**.
5. Choose **Dept** tag. Verify that costs are grouped under **Finance**.
6. Repeat for **Env** tag to see Prod environment costs.
7. Adjust the time range (e.g., Last 7 days / Last month) for analysis.

---

### Part 4 — Verification for learners

* Learners should provide a screenshot of a **Cost analysis chart grouped by Dept=Finance**.
* Learners should explain how tagging helps in cross-team cost allocation.

**Expected outcome:** Costs are filtered/grouped by applied tags, showing Finance + Prod resource spend.

---

### Part 5 — Optional Exercises

* Apply different tags for another RG: `Dept=HR`, `Env=Test` and compare.
* Export cost analysis to CSV and share.
* Build a custom dashboard pinned to Azure Portal home with cost charts.

---

### Cleanup (if required)

1. Navigate to RG or resource → Tags → remove tags.
2. Re-run cost analysis to confirm tags no longer appear.

---

### Assessment rubric

* **Pass** if learner successfully applies `Dept=Finance`, `Env=Prod` tags.
* **Pass** if learner runs cost analysis grouped by tag and submits a screenshot.
* **Bonus:** Learner compares costs across multiple departments/environments.

---

✅ Now the guide covers **Scenario 1: RBAC**, **Scenario 2: Management Groups**, and **Scenario 3: Tagging & Cost Analysis** in GUI mode.
