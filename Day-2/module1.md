# 📘 Azure Subscriptions & Resource Groups Training

**Authored by:** Vishwanath  
**Version:** 1.0  
**Target Audience:** Developers, DevOps Engineers, IT Admins, Corporate Teams  

---

## 1. 🎯 Objective
This training module will teach you how to:

- Understand **Azure hierarchy and scopes**  
- Work with **subscriptions and resource groups (RGs)**  
- Apply **RBAC roles at different scopes**  
- Implement **governance and policies**  
- Track **billing and cost management**  

---

## 2. 🚀 Why This Training is Important
Azure resources are vast and complex. Proper understanding of subscriptions and RGs is critical to:

- Organize resources logically for **Dev/Test/Prod environments**  
- Apply **security controls with least privilege**  
- Enforce **compliance and governance policies**  
- Track costs and **optimize cloud spending**  

---

## 3. 🗝️ Key Concepts

| Concept              | Description                        | Example                              | Why Needed |
|----------------------|------------------------------------|--------------------------------------|------------|
| **Tenant**           | Azure AD instance                  | `vishwaops.onmicrosoft.com`          | Central identity, manages all users & groups |
| **Management Group** | Organizes subscriptions            | `Corp-Mgmt`                          | Apply governance policies to multiple subscriptions |
| **Subscription**     | Billing + resource container       | `Dev-Subscription`, `Prod-Subscription` | Separate costs, quotas, and policies |
| **Resource Group (RG)** | Logical container for resources | `Dev-RG1`, `Prod-RG1`                | Manage lifecycle, access, and cost per project |
| **Resource**         | Actual Azure service               | VM, Storage Account, App Service     | The cloud asset you deploy |
| **Scope**            | Where RBAC is applied              | Subscription, RG, Resource           | Control permissions efficiently |
| **RBAC Roles**       | Assign permissions                 | Owner, Contributor, Reader           | Least privilege access management |
| **Policies & Governance** | Rules enforcement             | Allowed VM sizes, Allowed Regions    | Ensure compliance and security |
| **Billing & Cost Mgmt** | Track usage and cost            | Cost per RG, subscription            | Optimize cloud spending |

---

## 4. 🔗 Azure Hierarchy Overview
Azure resources are structured as follows:



Tenant → Management Group → Subscription → Resource Group → Resource


**Example Scenario:**  
- Tenant: `vishwaops.onmicrosoft.com`  
- Management Group: `Corp-Mgmt → Dev / Prod`  
- Subscription: `Dev-Subscription → RG: Dev-RG1`  
- Resource: VM, Storage Account  

**Outcome:** Logical separation, governance, cost tracking, and access control.

---

## 5. 🛠️ Hands-On Steps

### Step 1: Create a Resource Group
- Azure Portal → **Resource Groups → + Create**  
- Select Subscription → Enter Name (`Dev-RG1`) → Region → Review + Create  

✅ **Outcome:** RG created successfully; ready for resources  

---

### Step 2: Assign RBAC Roles
- Navigate to RG → **Access Control (IAM) → + Add → Role Assignment**  
- Assign **Contributor** → Select user (`dev@company.com`) → Save  

**Scenario:** Dev team member can create/manage VMs only in `Dev-RG1`  
✅ **Outcome:** Least privilege applied; cannot modify other RGs  

---

### Step 3: Deploy Resource (VM)
- RG → **+ Add → Virtual Machine → Fill details → Review + Create**  

**Scenario:** Dev team deploys VM inside `Dev-RG1`  
✅ **Outcome:** Resources contained within RG; RBAC enforced  

---

### Step 4: Apply Governance & Policies
- Subscription → **Policies → Assign → Select policy (e.g., allowed VM sizes)**  

**Scenario:** Restrict VMs to `Standard_B2s`  
✅ **Outcome:** Policy blocks non-compliant resources → ensures compliance  

---

### Step 5: Track Billing & Cost
- Subscription → **Cost Management + Billing → Cost Analysis → Filter by RG**  

**Scenario:** Compare costs for `Dev-RG1` vs `Prod-RG1`  
✅ **Outcome:** Understand per-project cost; manage budgets efficiently  

---

## 6. 🌍 Real-World Scenarios

| Scenario             | Steps                                      | Outcome |
|----------------------|--------------------------------------------|---------|
| Dev team provisioning | Create RG → Assign Contributor → Deploy VM | Dev can deploy/manage VMs in RG only |
| QA team read-only     | Assign Reader role at subscription/RG      | QA can view resources but not modify |
| IT admin governance   | Assign policy to limit VM size             | Users comply with rules automatically |
| Cost tracking         | Tag resources per project                  | Cost visible per RG/project |

---

## 7. 🎓 Expected Learning Outcomes
After this training, participants will be able to:

- Create and manage **Resource Groups (RGs)**  
- Assign **RBAC roles** at subscription and RG level  
- Deploy and manage **resources** within RBAC scope  
- Apply **policies for governance**  
- Track and optimize **billing and cost** per RG/subscription  

---

## 8. 💡 Why We Do This

- **Control & Organization:** Resources grouped logically for lifecycle management  
- **Security:** RBAC ensures least privilege access  
- **Governance:** Policies enforce company compliance  
- **Cost Management:** Track spending per project or subscription  

---

## 9. 📊 Example Diagram

```mermaid
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
    subgraph BILLING["Billing & Governance"]
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
