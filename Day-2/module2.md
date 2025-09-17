# 📘 Azure Subscriptions & Resource Groups Training (In-Depth)

**Authored by:** Vishwanath  
**Version:** 2.0  
**Target Audience:** Developers, DevOps Engineers, IT Admins, Corporate Teams  

---

## 1️⃣ Objective
After this module, trainees will:

- Understand Azure hierarchy: **Tenant → Subscription → RG → Resources**  
- Apply **RBAC roles and scopes** for least privilege  
- Implement **custom roles using JSON**  
- Use **governance & policies** for compliance  
- Track **billing & costs** per RG or subscription  
- Perform **hands-on lab exercises** with real-world scenarios  

---

## 2️⃣ Importance of Subscriptions & RGs
- **Resource Organization** → Logical grouping by environment, project, or team  
- **Security** → RBAC prevents unauthorized access  
- **Governance** → Policies enforce standards (VM sizes, regions, tags)  
- **Cost Optimization** → Track spend per subscription or RG  

---

## 3️⃣ Azure Hierarchy
**Tenant → Management Group → Subscription → Resource Group → Resource**


**Example:**  
- Tenant: `vishwaops.onmicrosoft.com`  
- Management Group: `Corp-Mgmt → Dev / Prod Subscriptions`  
- Subscription: `Dev-Subscription → RG: Dev-RG1`  
- Resource: VM, Storage Account  

✅ **Expected Outcome:** Logical separation, security, governance, and cost control  

---

## 4️⃣ Hands-On Steps (With Detailed Instructions)

### Step 1: Create a Resource Group
**Portal Steps:**
- Azure Portal → **Resource Groups → + Create**  
- Subscription → Name: `Dev-RG1` → Region: *Central India* → **Review + Create**  

**Scenario:** Dev team prepares RG for project X  
✅ **Outcome:** RG created successfully  

📷 **Screenshot Placeholder:**  
`[Image: RG creation page]`

---

### Step 2: Assign Built-In RBAC Roles
**Portal Steps:**
- RG → **Access Control (IAM) → + Add → Role Assignment**  
- Choose **Contributor** → Select user → Save  

**Scenario:** Dev team member can create/manage resources in `Dev-RG1` only  
✅ **Outcome:** RBAC restricts scope → least privilege applied  

---

### Step 3: Deploy Resource (VM)
**Portal Steps:**
- RG → **+ Add → Virtual Machine → Fill VM details → Review + Create**  

**Scenario:** User deploys `Dev-VM1` inside `Dev-RG1`  
✅ **Outcome:** Resources contained in RG, RBAC enforced  

📷 **Screenshot Placeholder:**  
`[Image: VM deployment page]`

---

### Step 4: Apply Governance & Policies
**Portal Steps:**
- Subscription → **Policies → Assign → Select policy (e.g., allowed VM sizes, allowed regions)**  

**Scenario:** Only `Standard_B2s` VMs allowed in Dev subscription  
✅ **Outcome:** Policy prevents non-compliant resources → compliance enforced  

📷 **Screenshot Placeholder:**  
`[Image: Policy assignment page]`

---

### Step 5: Track Billing & Cost
**Portal Steps:**
- Subscription → **Cost Management + Billing → Cost Analysis → Filter by RG or tag**  

**Scenario:** Compare cost for `Dev-RG1` vs `Prod-RG1`  
✅ **Outcome:** Clear cost tracking per project  

📷 **Screenshot Placeholder:**  
`[Image: Cost analysis page]`

---

## 5️⃣ Advanced: Custom RBAC Role JSON

**Scenario:** Allow a user to create VMs only in `Dev-RG1`

```json
{
  "Name": "VM Creator",
  "IsCustom": true,
  "Description": "Can create and manage Virtual Machines only",
  "Actions": [
    "Microsoft.Compute/virtualMachines/*",
    "Microsoft.Network/networkInterfaces/*",
    "Microsoft.Network/publicIPAddresses/*",
    "Microsoft.Storage/storageAccounts/read"
  ],
  "NotActions": [
    "Microsoft.Compute/virtualMachines/delete",
    "Microsoft.Authorization/*"
  ],
  "AssignableScopes": [
    "/subscriptions/{subscription-id}/resourceGroups/Dev-RG1"
  ]
}


| Exercise           | Steps                                | Expected Outcome                            |
| ------------------ | ------------------------------------ | ------------------------------------------- |
| Create RG          | Create `Dev-RG1` in Dev subscription | RG ready for resources                      |
| Assign Contributor | Assign to dev user                   | User can create/manage resources only in RG |
| Deploy VM          | Deploy `Dev-VM1`                     | VM created inside RG only                   |
| Apply Policy       | Restrict VM size                     | Users cannot create non-compliant VMs       |
| Track Cost         | Use tags per resource                | Cost tracked per RG/project                 |



| Scenario              | Problem                          | Solution                       | Outcome                                       |
| --------------------- | -------------------------------- | ------------------------------ | --------------------------------------------- |
| Dev team provisioning | Prevents accidental Prod changes | Assign Contributor at Dev-RG   | Devs can deploy resources safely              |
| QA testing            | Needs read-only access           | Assign Reader at subscription  | QA can view resources but not modify          |
| Cost tracking         | Overspending on test environment | Tag resources per project      | Cost per project visible, budget enforced     |
| Governance            | Enforce compliance               | Apply policies at subscription | Non-compliant resources blocked automatically |


8️⃣ Training Outcomes

After this training, participants will be able to:

Create subscriptions & RGs

Assign built-in and custom RBAC roles

Deploy resources within RBAC scope

Apply policies and governance

Track billing and cost per RG/subscription

Implement real-world access control and cost optimization scenarios


9️⃣ Professional Diagram
flowchart TD
    A[Azure AD Tenant: vishwaops.onmicrosoft.com] 
    subgraph MG["Management Groups"]
        B1[Corp-Mgmt] --> B2[Dev-Mgmt]
        B1 --> B3[Prod-Mgmt]
    end
    subgraph SUBS["Subscriptions"]
        S1[Dev-Subscription] 
        S2[Prod-Subscription]
    end
    subgraph RG["Resource Groups"]
        RG1[Dev-RG1] --> R1[VM, Storage, App Service]
        RG2[Prod-RG1] --> R2[VM, Storage, DB]
    end
    subgraph ROLES["RBAC Roles"]
        O[Owner] 
        C[Contributor]
        R[Reader]
    end
    subgraph POLICY["Governance & Billing"]
        POL[Policies & Blueprints]
        COST[Cost Management & Tags]
    end
    A --> MG
    MG --> S1
    MG --> S2
    S1 --> RG1
    S2 --> RG2
    O -->|Full Control| S1
    O -->|Full Control| S2
    C -->|Manage Resources| RG1
    R -->|View Only| RG2
    S1 --> POL
    S1 --> COST
    S2 --> POL
    S2 --> COST




