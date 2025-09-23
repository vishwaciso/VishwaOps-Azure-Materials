# RBAC Lab — GUI step-by-step

**Level:** Intermediate — RBAC at different scopes

**Scenario:** HR team should manage **Payroll VM(s)** but **not** the Production DB. We will give `hruser@company.com` **Contributor** on the *Payroll* Resource Group and **Reader** on the *Subscription*.

> This document is a click-by-click Azure Portal guide you can hand to corporate employees. Replace placeholder values (e.g., `<your-subscription>`) before running the lab.

---

## Lab goal (one line)

Allow `hruser@company.com` to fully manage resources in `Payroll-RG` (start/stop/create/delete VMs) but prevent any modification to resources in `Prod-RG` (production SQL server / DB).

---

## Prerequisites (lab admin)

* You must be **Azure AD Global Admin** or **Subscription Owner** (able to create users and assign roles).
* An Azure subscription for the lab.
* Minimum required permissions: Owner or **User Access Administrator** on the subscription.
* Decide resource names before starting:

  * HR user: `hruser@company.com`
  * Payroll RG: `Payroll-RG`
  * Payroll VM name: `payroll-vm`
  * Prod RG: `Prod-RG`
  * Prod SQL server: `prod-sql-server`
  * Prod DB: `prod-db`

---

## Part 1 — Create the HR user (Azure Portal)

1. Open a browser and go to **[https://portal.azure.com](https://portal.azure.com)**. Sign in with your admin account.
2. In the top search bar type **Azure Active Directory** and press Enter. Click the **Azure Active Directory** result.
3. In the left menu of Azure AD, click **Users**.
4. Click **+ New user** → choose **Create user**.
5. On the Create user blade fill these fields:

   * **Identity** → **User name**: `hruser@company.com`
   * **Name**: `HR User` (optional)
   * **Password**: Select **Let me create the password** or **Auto-generate password**. If you generate it, **copy** the temporary password shown.
   * Ensure **Require user to change password on first sign-in** is checked.
6. Click **Create**. Wait for the success notice.
7. Save the temporary password securely and provide it to the learner via a secure channel (e.g., company SSO message). They will be asked to reset it on first sign-in.

---

## Part 2 — Create the Resource Groups (Portal)

> Skip this part if these RGs already exist.

1. In the left menu search box type **Resource groups** and open **Resource groups**.
2. Click **+ Create**.
3. On the Create resource group page:

   * **Subscription**: pick your lab subscription
   * **Resource group**: `Payroll-RG`
   * **Region**: pick a region (e.g., `East US`)
4. Click **Review + create** → **Create**.
5. Repeat steps to create **Prod-RG**.

---

## Part 3 — Create a small VM in `Payroll-RG` (Portal)

1. In the left menu search for **Virtual machines** and open it.
2. Click **+ Create** → **Azure virtual machine**.
3. On the **Basics** tab fill:

   * **Subscription**: choose the lab subscription
   * **Resource group**: select `Payroll-RG`
   * **Virtual machine name**: `payroll-vm`
   * **Region**: same as RG
   * **Image**: `Ubuntu Server 22.04 LTS` (or `Windows Server` if preferred)
   * **Size**: click **Change size** and select the smallest (e.g., `Standard_B1s`)
   * **Administrator account**: choose **Password** or **SSH public key** (for labs, using password is simpler)
   * **Username**: `azureuser` (example) and set a secure password
   * **Public inbound ports**: choose **None** if you don't need inbound access, or **SSH (22)** for Linux during the lab
4. Click **Next: Disks** → Accept defaults → **Next: Networking** → Accept defaults → **Next: Management** → keep default → **Review + Create** → **Create**.
5. Wait until deployment completes (notification bell → "Deployment succeeded").

---

## Part 4 — Create a production SQL server + database in `Prod-RG` (Portal)

> Use the smallest SKU and minimal firewall rules for lab safety.

1. In top search box type **Azure SQL** and open **Azure SQL** → Click **Create SQL server** (or use **SQL servers** then **+ Add**).
2. On the Basics tab:

   * **Subscription**: choose your subscription
   * **Resource group**: `Prod-RG`
   * **Server name**: `prod-sql-server`
   * **Server admin login**: `sqladmin` and set a strong password
   * **Location**: choose same region
3. Click **Review + create** → **Create**.
4. After server creation, go to the SQL server page → **+ Create database** → **Database name**: `prod-db` → Choose smallest compute (Basic / General Purpose minimum) → **Create**.

---

## Part 5 — Assign **Reader** at Subscription scope (Portal, admin)

1. From the left menu click **Subscriptions** and select the lab subscription (or search **Subscriptions** in the top bar).
2. In the subscription blade left menu click **Access control (IAM)**.
3. Click **+ Add** → **Add role assignment**.
4. In the **Role** dropdown choose **Reader**.
5. **Assign access to**: select **User, group, or service principal**.
6. Click **Select members** → search for `hruser@company.com` → tick the user → **Select**.
7. Click **Review + assign** → **Review + assign** (or **Assign**). Wait for the success toast: *Role assignment succeeded*.

---

## Part 6 — Assign **Contributor** at Resource Group scope (Portal, admin)

1. In the left menu click **Resource groups**, then click **Payroll-RG**.
2. Inside the `Payroll-RG` blade, click **Access control (IAM)** in the left menu.
3. Click **+ Add** → **Add role assignment**.
4. In **Role** choose **Contributor**.
5. **Assign access to**: **User, group, or service principal** → Click **Select members** → search `hruser@company.com` → select and **Select**.
6. Click **Review + assign** → **Review + assign** (or **Assign**).
7. Wait for the confirmation toast.

**Important:** Make sure the **scope** shown at the top of the Add role assignment blade is `/subscriptions/<id>/resourceGroups/Payroll-RG` and not the subscription-level scope.

---

## Part 7 — Testing the permissions (as `hruser@company.com`)

> Have the learner sign in with the temporary password and perform the steps below.

### A. Sign in and reset password

1. Instruct learner to open **[https://portal.azure.com](https://portal.azure.com)** and sign in with `hruser@company.com` and temporary password.
2. Complete the password reset flow when prompted.

### B. Confirm subscription visibility (Reader)

1. In the portal left menu search **Subscriptions** and open it.
2. Learner should see the lab subscription listed. They can click it to **view** details but they should not be able to perform write operations at subscription scope.

### C. Manage the Payroll VM (Contributor on `Payroll-RG`) — **should succeed**

1. From the left menu click **Resource groups** → open **Payroll-RG**.
2. Click **Virtual machines** (under the Payroll-RG resources) → click `payroll-vm`.
3. On the VM blade use **Stop**, **Start**, **Restart**, and check **Disks**, **Networking** — most resource-level operations should be allowed.
4. Try to **Create** a new resource inside Payroll-RG: In the Payroll-RG blade click **+ Add** → create a tiny storage account or another small VM. The contributor role allows creating resources within the RG.

**Expected result:** Actions like Start/Stop or creating resources under `Payroll-RG` succeed.

### D. Attempt to modify the Production DB (Prod-RG) — **should be blocked**

1. From left menu click **Resource groups** → open **Prod-RG**.
2. Click **SQL servers** → open `prod-sql-server` → try to **Configure** or **Reset password** or **Update** server properties.
3. Try editing the database `prod-db` (for example, scale compute or change pricing tier) by clicking **Overview** → **Configure** or **Compute + storage**.

**Expected result:** The UI will show errors or the action buttons will be disabled. You may see a permission error such as **You do not have permission to perform this action** or the operation fails when you attempt it.

### E. Verify role assignments (Admin) — quick check

1. Admin: Subscriptions → select subscription → **Access control (IAM)** → **Role assignments** → search `hruser@company.com` → verify **Reader** at subscription.
2. Admin: Resource groups → select `Payroll-RG` → **Access control (IAM)** → **Role assignments** → verify **Contributor** assigned to `hruser@company.com`.

---

## Troubleshooting (GUI pointers)

* **If user cannot sign in:** Ensure the user was created in the same Azure AD tenant (not as a guest pending invitation) and that the temporary password is correct.
* **If user sees no subscription:** Confirm the Reader role at subscription scope was assigned to the right subscription and the correct user object (search the full UPN). Use the tenant dropdown (top-right) to confirm tenant.
* **If VM actions are denied despite Contributor on the RG:** Check whether a Deny assignment or Azure Policy is blocking the action. Go to the VM blade → **Diagnose and solve problems** for operation logs.
* **If assignments aren’t visible yet:** Role assignments can take a minute to propagate. Wait 2–5 minutes and refresh the portal.

---

## Lab exercises for learners (give as checklist)

1. Log in as `hruser@company.com` and show a screenshot of the VM **Stop** operation succeeding.
2. Attempt to edit `prod-db` and take a screenshot of the permission-denied message.
3. In the portal, open **Subscriptions** → **Access control (IAM)** → **View my access** (or admin checks **Role assignments**) and copy the role assignment lines proving Reader+Contributor.
4. Short written answer: Why is assigning Contributor at RG + Reader at subscription preferred instead of giving Contributor at subscription? (expected: least privilege, limits blast radius, prevents changing role assignments or subscription-level settings)

---

## Cleanup (important to avoid charges)

1. Admin: Resource groups → open `Payroll-RG` → click **Delete resource group** → type the resource group name to confirm → **Delete**.
2. Admin: Resource groups → open `Prod-RG` → **Delete resource group**.
3. Optionally delete the user: Azure Active Directory → Users → search `hruser@company.com` → click **Delete**.

---

## Assessment rubric (quick)

* **Pass** if learner can start/stop `payroll-vm` and create a small resource in `Payroll-RG`.
* **Pass** if learner receives a permission error when trying to modify `prod-db`.
* **Evidence required:** Screenshots of the successful VM action, the permission-denied message, and the role assignment listing.

---

If you want this converted into a one-page printable PDF or a slide deck for instructor-led training, tell me and I will produce it next.
