# Azure Governance Advanced Scenarios (GUI step-by-step)

This guide provides corporate learners with **click-by-click labs** for advanced governance use cases in Azure Portal.

---

## Scenario 2: Azure Policy Enforcement

**Story:** Company enforces that all resources must be created in **East US**. Any other region is blocked.
**Lab:** Create a policy restricting region, assign it at subscription. Try creating resource in West US.
**Outcome:** Learners understand compliance enforcement.

---

### Part 1 — Create a new policy definition

1. Sign in to **[https://portal.azure.com](https://portal.azure.com)**.
2. In the search bar, type **Policy** and select it.
3. In the left menu, click **Definitions**.
4. Click **+ Policy definition**.
5. Fill the form:

   * **Definition location**: Select your subscription.
   * **Name**: `Allowed Locations — East US`
   * **Description**: `Restrict resources to East US only`
   * **Category**: Use existing or create `Governance`
   * **Policy rule**: Use built-in JSON or custom rule:

```json
{
  "if": {
    "not": {
      "field": "location",
      "equals": "eastus"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

6. Click **Save**.

---

### Part 2 — Assign the policy

1. In the **Policy** blade, click **Assignments**.
2. Click **+ Assign policy**.
3. Basics tab:

   * **Scope**: Select your subscription.
   * **Policy definition**: Select `Allowed Locations — East US`.
4. Parameters tab: leave default (since hardcoded in rule).
5. Click **Review + Create** → **Create**.

---

### Part 3 — Test enforcement

1. In the portal, try creating a new resource (e.g., a Storage Account).
2. When choosing **Region**, select **West US**.
3. Click **Review + Create**.
4. Validation should fail with a policy error: *“The resource location is not allowed.”*
5. Try again with **East US** → deployment succeeds.

**Expected outcome:** Learners observe that only East US deployments are allowed.

---

### Assessment rubric

* **Pass** if learner creates and assigns policy at subscription scope.
* **Pass** if attempt to deploy in West US is denied.
* **Bonus:** Assign policy at Management Group level and verify inheritance.

---

## Scenario 3: Resource Locks

**Story:** A critical Production RG should not be deleted. Add a Delete Lock.
**Lab:** Apply lock, try deleting RG → fails.
**Outcome:** Learners learn protection against accidental deletion.

---

### Part 1 — Apply lock on Resource Group

1. In the portal, search **Resource groups**.
2. Select the **Production-RG** (or create a new test RG).
3. In the left menu, click **Locks**.
4. Click **+ Add**.

   * **Lock name**: `Protect-Prod-RG`
   * **Lock type**: **Delete**
   * Click **OK**.

---

### Part 2 — Test the lock

1. In **Production-RG**, click **Delete resource group**.
2. Enter the RG name to confirm deletion.
3. Click **Delete**.
4. Azure shows an error: *“Cannot delete resource group because of a lock.”*

---

### Part 3 — Optional Read-only lock

1. In the same RG, add another lock:

   * **Lock type**: **Read-only**
2. Try editing resource settings inside the RG — changes are blocked.

---

### Part 4 — Remove lock (cleanup)

1. Navigate back to **Production-RG → Locks**.
2. Delete the `Protect-Prod-RG` lock.
3. Retry deletion — now succeeds.

---

### Assessment rubric

* **Pass** if learner applies a Delete lock and deletion fails.
* **Bonus:** Demonstrate Read-only lock and its effect.

---

✅ Learners now practice **Scenario 2: Policy Enforcement** and **Scenario 3: Resource Locks** using only GUI navigation.
