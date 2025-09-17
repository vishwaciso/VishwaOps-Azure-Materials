🌐 Azure Organization Hierarchy
1. Layman Analogy (to explain in training)

Tenant = Headquarters (HQ)
Like the central company office, every Azure customer gets one HQ that controls identity (Azure AD / Entra ID).

Management Group = Cabinet / Department
Just like government departments (Finance, HR, IT), used to group subscriptions for governance & policies.

Subscription = Electricity Bill
Each department gets its own bill. It defines billing boundaries and service quotas.

Resource Group = Folder
Inside each subscription, you keep things organized in folders. Example: HR-Payroll-RG, IT-Infra-RG.

Resources = Files in Folder
Actual services: VMs, Databases, Storage, Key Vaults, AKS clusters, etc.

Azure Tenant (HQ / Identity Boundary)
│
├─ Management Groups (Gov/OU Level)
│   ├─ Corp-IT-MG
│   │   ├─ Subscription: Finance-Sub
│   │   │    ├─ RG: Payroll-RG
│   │   │    │   ├─ VM: Payroll-VM01
│   │   │    │   ├─ DB: Payroll-DB01
│   │   │    │   └─ KV: Payroll-KeyVault
│   │   │    └─ RG: Reports-RG
│   │   │         └─ Storage: SalaryReports
│   │   └─ Subscription: HR-Sub
│   │        └─ RG: Recruitment-RG
│   │             ├─ App Service: HR-App01
│   │             └─ DB: Candidate-DB
│   │
│   └─ DevOps-MG
│       ├─ Subscription: Dev-Sub
│       │    └─ RG: Dev-Infra
│       │         ├─ AKS: DevCluster01
│       │         └─ ACR: DevContainerRegistry
│       └─ Subscription: Test-Sub
│            └─ RG: QA-Infra
│                 └─ VM: QA-VM01
│
└─ Root Management Group (applies org-wide policies)

Box Layout (for PPT/Docs)
+---------------------------------------------------+
|                Azure Tenant (HQ)                  |
|    Identity & Directory (Entra ID / Azure AD)     |
+--------------------------+------------------------+
           |                                |
   +-------+------+                +--------+-------+
   | Management   |                | Management     |
   | Group: Corp- |                | Group: DevOps- |
   | IT-MG        |                | MG             |
   +-------+------+                +--------+-------+
           |                                |
+----------+-----------+        +-----------+----------+
| Subscription: Finance|        | Subscription: Dev-Sub|
| - Payroll-RG         |        | - Dev-Infra RG      |
| - Reports-RG         |        |   • AKS Cluster     |
|                      |        |   • ACR             |
+----------------------+        +----------------------+
| Subscription: HR-Sub |        | Subscription: Test-Sub|
| - Recruitment-RG     |        | - QA-Infra RG        |
+----------------------+        +----------------------+

Mermaid Diagram (for GitHub/Docs rendering)
flowchart TD
  TENANT["Azure Tenant (HQ / Identity Boundary)"]

  subgraph MG1["Corp-IT-MG (Management Group)"]
    SUBF["Finance-Sub"]
    SUBH["HR-Sub"]
  end

  subgraph MG2["DevOps-MG (Management Group)"]
    SUBD["Dev-Sub"]
    SUBT["Test-Sub"]
  end

  SUBF --> RG1["Payroll-RG (VMs, DBs, KV)"]
  SUBF --> RG2["Reports-RG (Storage)"]

  SUBH --> RG3["Recruitment-RG (App, DB)"]

  SUBD --> RG4["Dev-Infra RG (AKS, ACR)"]
  SUBT --> RG5["QA-Infra RG (VMs)"]

  TENANT --> MG1
  TENANT --> MG2

3. Key Notes for Students

Tenant = identity + global scope (only 1 tenant per organization, but multiple subscriptions under it).

Subscriptions = billing units (can have many subscriptions under one tenant, but not vice versa).

Management Groups = governance layers, where you apply Azure Policy, RBAC, Blueprints.

Resource Groups = logical containers to group & manage lifecycle (delete RG → deletes all resources inside).

Resources = actual services you provision.
