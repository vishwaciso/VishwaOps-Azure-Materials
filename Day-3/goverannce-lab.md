# Governance Lab — Management Groups (GUI step-by-step)

**Level:** Intermediate — Governance with Management Groups

**Scenario:** Organization has 3 subscriptions → **Dev**, **Test**, **Prod**. Add them under a Management Group for centralized governance.

> This is a click-by-click Azure Portal guide for corporate employees. Replace placeholder values (like `<your-tenant-id>`) before running the lab.

---

## Lab goal (one line)

Group Dev, Test, and Prod subscriptions under a single Management Group to enable centralized policy and RBAC governance.

---

## Prerequisites (lab admin)

* You must be **Azure AD Global Admin** or **Management Group Contributor** at tenant root.
* Azure AD tenant must have **Management groups** feature enabled (default in most tenants).
* At least 3 existing subscriptions (`Dev`, `Test`, `Prod`) linked to the same Azure AD tenant.

---

## Part 1 — Enable management groups (if not already)

1. Sign in to **[https://portal.azure.com](https://portal.azure.com)** with your admin account.
2. In the search bar type **Management groups** and press Enter.
3. If this is your first time, you may be asked to enable management groups. Click **Start using management groups**. Wait until provisioning completes.

---

## Part 2 — Create a root management group (if not already present)

1. In the Management groups blade, you should see a **Tenant root group** automatically. If hidden, click **Settings** → **Toggle show tenant root group** → Save.
2. Verify that the root group is visible.

---

## Part 3 — Create a new management group for Org governance

1. In the Management groups blade, click **+ Create**.
2. On the **Basics** tab:

   * **Management group ID**: `Org-MG` (ID must be unique; lowercase letters and hyphens only)
   * **Display name**: `Org Management Group`
3. Click **Submit**.
4. Wait until creation succeeds and `Org-MG` appears in the list.

---

## Part 4 — Move Dev, Test, Prod subscriptions under the new Management Group

1. In the Management groups blade, click your new group `Org-MG`.
2. In the left menu click **Details**.
3. On the toolbar click **+ Add subscription**.
4. In the dialog box:

   * Select subscription `Dev` → **Save**.
5. Repeat the same for `Test` and `Prod` subscriptions.
6. Confirm that all three subscriptions are now listed under `Org-MG`.

---

## Part 5 — Verification (as learner)

1. In the portal, search **Management groups** → open `Org-MG`.
2. Learners should see `Dev`, `Test`, and `Prod` subscriptions listed.
3. Click on each subscription — notice the breadcrumb navigation shows `Tenant root group` → `Org-MG` → `Dev` (or Test/Prod).

**Expected outcome:** Learners observe centralized governance structure with all subscriptions under a single parent.

---

## Part 6 — Optional governance demonstration

1. In `Org-MG`, click **Access control (IAM)**. Assign a role (e.g., **Reader**) to a test user at the management group level.

   * Verify the user inherits this Reader role across all 3 subscriptions.
2. In `Org-MG`, click **Policies** → **Assignments** → **+ Assign policy**.

   * Example: assign a built-in policy like **Allowed locations**.
   * Verify the policy applies to all 3 subscriptions.

---

## Troubleshooting (GUI pointers)

* If subscriptions do not appear in the **+ Add subscription** list: ensure they are in the same Azure AD tenant.
* If you cannot create a management group: confirm you have **Global Admin** and the tenant root group is visible.
* Changes may take 1–2 minutes to propagate — refresh the blade if you don’t see updates immediately.

---

## Lab exercises for learners (checklist)

1. Create a management group `Org-MG`.
2. Add `Dev`, `Test`, and `Prod` subscriptions under it.
3. Capture a screenshot showing the hierarchy tree with all 3 subscriptions under `Org-MG`.
4. (Optional) Assign a Reader role at the management group level and prove access cascades to subscriptions.

---

## Cleanup (if required)

1. Open Management groups → click `Org-MG`.
2. Remove the subscriptions by clicking **... (More)** next to each subscription → **Move** → move back to root.
3. After subscriptions are removed, click **Delete** on the management group.

---

## Assessment rubric

* **Pass** if learner creates `Org-MG` and adds all 3 subscriptions.
* **Pass** if learner provides screenshot of hierarchy tree.
* **Optional bonus**: Demonstrate cascading RBAC or Policy assignment at `Org-MG` level.

---
