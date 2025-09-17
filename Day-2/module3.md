# 📘 Azure Subscriptions & Resource Groups Training (Advanced)

**Authored by:** Vishwanath  
**Version:** 3.0 – Advanced Corporate Training  
**Target Audience:** Developers, DevOps Engineers, IT Admins, Cloud Architects  

---

## 1️⃣ Objective
This advanced module will enable participants to:

- Understand **multi-subscription hierarchy and management groups**  
- Apply **RBAC at multiple scopes with inheritance**  
- Create **advanced custom roles using wildcards and JSON**  
- Implement **policies, blueprints, and governance workflows**  
- Track **billing & cost optimization** across multiple subscriptions  
- Perform **hands-on labs for real-world enterprise scenarios**  

---

## 2️⃣ Why This is Critical
Large enterprises often have **multiple subscriptions and departments**. This advanced training ensures:

- ✅ Proper **resource organization** across subscriptions and environments  
- ✅ **Security & least privilege** enforced via RBAC and inheritance  
- ✅ **Governance & compliance** at scale with policies and blueprints  
- ✅ **Cost optimization** across multiple projects and departments  

---

## 3️⃣ Azure Hierarchy & Scope Inheritance

**Tenant → Management Group → Subscription → Resource Group → Resource**


**Example Enterprise Setup:**  
- **Tenant:** `vishwaops.onmicrosoft.com`  
- **Management Group:** `Corp-Mgmt → Divisions: Dev, Prod, QA`  
- **Subscriptions:** `Dev-Sub1`, `Dev-Sub2`, `Prod-Sub1`  
- **Resource Groups:** `Dev-RG1`, `Dev-RG2`, `Prod-RG1`, `QA-RG1`  

**RBAC Scope Inheritance:**  
- Role at **Management Group** → inherited by all subscriptions & RGs under it  
- Role at **Subscription** → inherited by all RGs under it  
- Role at **Resource Group** → only applies to that RG  

✅ **Outcome:** Centralized role management with least privilege control  

---

## 4️⃣ Multi-Subscription Lab Exercises

### 🔹 Exercise 1: Create Management Groups
- **Azure Portal → Management Groups → + Create**  
- Names: `Corp-Mgmt`, `Dev-Mgmt`, `Prod-Mgmt`  
- Assign subscriptions under respective groups  

**Scenario:** Dev subscriptions under `Dev-Mgmt`, Prod subscriptions under `Prod-Mgmt`  
✅ **Outcome:** Centralized governance and RBAC inheritance  

---

### 🔹 Exercise 2: Assign Roles at Management Group Level
- **Dev-Mgmt → Access Control → + Add → Role Assignment → Contributor**  
- Select user: `dev@company.com`  

**Scenario:** Dev user can manage all resources in all subscriptions under `Dev-Mgmt`  
✅ **Outcome:** Role automatically inherited by RGs & resources under Dev subscriptions  

---

### 🔹 Exercise 3: Advanced Custom Role with Wildcards
**Scenario:** Allow user to create VMs & NICs only, block deletion.  

```json
{
  "Name": "Advanced VM Creator",
  "IsCustom": true,
  "Description": "Can create VMs & NICs but cannot delete",
  "Actions": [
    "Microsoft.Compute/virtualMachines/*",
    "Microsoft.Network/networkInterfaces/*"
  ],
  "NotActions": [
    "Microsoft.Compute/virtualMachines/delete",
    "Microsoft.Network/networkInterfaces/delete"
  ],
  "AssignableScopes": [
    "/subscriptions/{subscription-id}/resourceGroups/Dev-RG1"
  ]
}


Exercise 4: Apply Policies Across Subscriptions

Policy: Allowed VM SKUs → Assign at Dev-Mgmt

Policy: Allowed Locations → Assign at Corp-Mgmt

Scenario: Restrict VM size & location across enterprise
✅ Outcome: Users cannot create non-compliant resources → automated governance

🔹 Exercise 5: Deploy Blueprints

Azure Portal → Blueprints → + Create

Assign Resource Groups, Policies, Role Assignments

Publish & Assign to subscriptions

Scenario: Predefine environment setup (RG + VMs + Policies + Tags)
✅ Outcome: Standardized enterprise deployment across multiple subscriptions

🔹 Exercise 6: Cost Management Across Subscriptions

Cost Management + Billing → Scope: Dev-Mgmt → Cost Analysis

Apply tags per RG/project

Scenario: Dev, QA, Prod cost tracking per project
✅ Outcome: Enterprise-wide cost visibility & optimization

5️⃣ Real-World Enterprise Scenarios


| Scenario                    | Problem                                  | Solution                       | Outcome                                 |
| --------------------------- | ---------------------------------------- | ------------------------------ | --------------------------------------- |
| Multi-subscription dev team | Need access to all dev subscriptions     | Assign Contributor at Dev-Mgmt | User inherits access across all RGs     |
| Governance enforcement      | Prevent deployment in disallowed regions | Policy assigned at Corp-Mgmt   | Non-compliant resources blocked         |
| Role separation             | Devs can’t delete production VMs         | Custom role with NotActions    | Prevent accidental deletion             |
| Standardized environment    | Multiple dev projects require same setup | Blueprint assignment           | RG, VMs, policies deployed consistently |
| Cost tracking               | Overspending in multiple subscriptions   | Cost analysis by MG & tags     | Budget enforced, optimized spend        |



6️⃣ Diagram: Enterprise RBAC + Governance


flowchart TD
    A[Azure AD Tenant: vishwaops.onmicrosoft.com] 
    subgraph MG["Management Groups"]
        B1[Corp-Mgmt] --> B2[Dev-Mgmt]
        B1 --> B3[Prod-Mgmt]
        B1 --> B4[QA-Mgmt]
    end
    subgraph SUBS["Subscriptions"]
        S1[Dev-Sub1] 
        S2[Dev-Sub2]
        S3[Prod-Sub1]
        S4[QA-Sub1]
    end
    subgraph RG["Resource Groups"]
        RG1[Dev-RG1] --> R1[VM, Storage]
        RG2[Dev-RG2] --> R2[VM, DB]
        RG3[Prod-RG1] --> R3[VM, Storage, DB]
        RG4[QA-RG1] --> R4[VM, App Service]
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
    MG --> S3
    MG --> S4
    S1 --> RG1
    S2 --> RG2
    S3 --> RG3
    S4 --> RG4
    O -->|Full Control| S3
    C -->|Manage Resources| B2
    R -->|View Only| B4
    S1 --> POL
    S1 --> COST
    S3 --> POL
    S3 --> COST


7️⃣ Expected Training Outcomes

After this module, participants can:

✅ Design multi-subscription Azure environments

✅ Apply RBAC with inheritance at scale

✅ Create custom roles with wildcards & restrictions

✅ Enforce governance and compliance policies

✅ Deploy Blueprints for standardized environments

✅ Track & optimize enterprise costs across subscriptions

