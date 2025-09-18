# 🌍 Multi-Cloud Organization Structures (AWS | Azure | GCP)

This repo provides a comparison of **AWS, Azure, and GCP organizational structures** for enterprises handling multiple clients.  
It covers hierarchy, shared services, security accounts, networking hubs, and policy enforcement.

---

## 📌 Example Enterprise Setup

### AWS Organization (Root → OU → Accounts)


Org Root
│
├── OU: Clients
│   ├── OU: Philips
│   │   ├── Philips-Security   (GuardDuty, AWS Config, Security Hub)
│   │   ├── Philips-Dev        (Developer environment, EC2, RDS, S3)
│   │   ├── Philips-Prod       (Healthcare apps, ML, HIPAA compliant infra)
│   │   └── Philips-Sandbox    (POC for AI/ML models, testing)
│   │
│   ├── OU: GE
│   │   ├── GE-Security        (IoT traffic monitoring, IAM governance)
│   │   ├── GE-Dev             (IoT pipeline development, Kinesis, Lambda)
│   │   ├── GE-Prod            (Industrial IoT telemetry, analytics in Redshift)
│   │   └── GE-Sandbox         (Predictive maintenance ML tests)
│   │
│   ├── OU: Benz
│   │   ├── Benz-Security      (API monitoring, IAM least privilege)
│   │   ├── Benz-Dev           (Connected car app development)
│   │   ├── Benz-Prod          (Telemetry API, DynamoDB, Cognito, Mobile App)
│   │   └── Benz-Sandbox       (Autonomous driving experiments)
│   │
│   ├── OU: Netflix
│   │   ├── Netflix-Security   (Content protection, DRM monitoring)
│   │   ├── Netflix-Dev        (Media pipeline dev, test encoding)
│   │   ├── Netflix-Prod       (Streaming infra: CloudFront, MediaLive, S3)
│   │   └── Netflix-Sandbox    (New codec & AI subtitle experiments)
│   │
│   ├── OU: Siemens
│   │   ├── Siemens-Security   (SCADA security monitoring)
│   │   ├── Siemens-Dev        (Edge/IoT dev workloads)
│   │   ├── Siemens-Prod       (Smart factory analytics, IoT Core, Greengrass)
│   │   └── Siemens-Sandbox    (Prototype for Industry 4.0 apps)
│   │
│   └── OU: Pfizer
│       ├── Pfizer-Security    (Clinical trial compliance, FDA audit logs)
│       ├── Pfizer-Dev         (Drug research apps, test pipelines)
│       ├── Pfizer-Prod        (Genomics, R&D workloads, ML pipelines)
│       └── Pfizer-Sandbox     (AI/ML drug discovery experiments)
│
└── OU: Shared Services
    ├── Logging Account         (Centralized CloudTrail, S3 Logs, VPC Flow Logs)
    ├── Security Audit Account  (IAM Access Analyzer, Config aggregator, Inspector)
    ├── Networking Account      (Transit Gateway, VPC Peering, Direct Connect)
    └── Tooling Account         (CI/CD pipelines, Jenkins, CodeBuild, Monitoring)




Azure — Management / Subscription Design (real-time)

Top-level: Azure AD Tenant (Identity & Auth)
Root: Management Group (Root)

Management Group: Root
│
├── Management Group: SharedServices
│   ├── Subscription: Logging        (Log Analytics, Storage for diagnostics)
│   ├── Subscription: Security       (Azure Defender, Sentinel workspace)
│   ├── Subscription: Networking     (Hub VNet, Virtual WAN, ExpressRoute)
│   └── Subscription: Tooling        (DevOps, Artifacts, CI/CD, Azure Container Registry)
│
├── Management Group: Clients
│   ├── MG: Philips
│   │   ├── Sub: Philips-Security    (Sentinel, Policy initiative, Key Vault mgmt)
│   │   ├── Sub: Philips-Dev         (Dev subscriptions — cheaper SKUs)
│   │   ├── Sub: Philips-Prod        (Production workloads, AKS/VMSS, SQL MI)
│   │   └── Sub: Philips-Sandbox     (POCs, Data Science)
│   │
│   ├── MG: GE
│   │   ├── GE-Security
│   │   ├── GE-Dev
│   │   ├── GE-Prod
│   │   └── GE-Sandbox
│   │
│   ├── MG: Benz
│   │   ├── Benz-Security
│   │   ├── Benz-Dev
│   │   ├── Benz-Prod
│   │   └── Benz-Sandbox
│   │
│   ├── MG: Netflix
│   ├── MG: Siemens
│   └── MG: Pfizer
│
└── Management Group: Platform (optional)
    ├── Identity & Governance (Azure AD PIM, Conditional Access)
    └── Landing Zone Templates (Blueprints, Bicep/Terraform marketplace)

Key Azure controls & patterns (real-time)

Identity: Azure AD (use B2B for client teams), PIM for privileged roles.

Policies: Azure Policy initiatives applied at MG level (deny public IPs on prod, allowed locations).

Blueprints / Landing Zones: Deploy subscription baseline (NSGs, diagnostic settings, Key Vault).

Networking: Hub-and-spoke (Networking subscription as the hub; Shared VNet via peering or Private Link). Use ExpressRoute for on-prem links.

Logging: Central Log Analytics workspace in Logging subscription; forward diagnostics + Activity Logs.

Security: Microsoft Sentinel in Security subscription; Defender for Cloud across subscriptions.

Billing: Cost Management per subscription + tagging (client, env, project).

DevOps: Central tooling subscription with pipelines (Azure DevOps/GitHub Actions) deploying to client subscriptions with least-privileged service principals.

Example service mappings per client (brief)

Philips-Prod: AKS (ML inference), Azure SQL Managed Instance, Blob Storage (HIPAA controls), Private Endpoints.

GE-Prod: IoT Hub, Event Hubs, Data Lake Storage Gen2, Synapse Analytics.

Benz-Prod: API Management + Functions, Cosmos DB/Dynamo-like, Azure AD B2C for mobile users.

GCP — Organization / Folder / Project Design (real-time)

Top-level: GCP Organization (linked to Cloud Identity)
Hierarchy: Organization → Folders → Projects

Organization: my-company.com
│
├── Folder: Shared-Services
│   ├── Project: logging-project        (Cloud Logging, BigQuery export, audit logs)
│   ├── Project: security-project       (Security Command Center, Forseti / Policy)
│   ├── Project: networking-project     (VPCs, Shared VPC Host Project, Interconnect)
│   └── Project: tooling-project        (CI/CD, Cloud Build, Artifact Registry)
│
├── Folder: Clients
│   ├── Folder: Philips
│   │   ├── Project: philips-security   (SCC, Access Context Manager)
│   │   ├── Project: philips-dev
│   │   ├── Project: philips-prod
│   │   └── Project: philips-sandbox
│   │
│   ├── Folder: GE
│   │   ├── GE-security
│   │   ├── GE-dev
│   │   ├── GE-prod
│   │   └── GE-sandbox
│   │
│   ├── Folder: Benz
│   ├── Folder: Netflix
│   ├── Folder: Siemens
│   └── Folder: Pfizer
│
└── Folder: Platform (optional)
    ├── IAM & Policy management
    └── Landing Zone configs (Cloud Foundation Toolkit / Terraform)

Key GCP controls & patterns (real-time)

Identity: Cloud Identity + Google Workspace. Use groups for IAM (least privilege).

Resource hierarchy: Use Folders per client, Projects per environment.

Network: Shared VPC host project in Networking project; use VPC Service Controls for sensitive data (e.g., Philips, Pfizer).

Policies: Organization Policy Constraints (restrict regions, restrict external IPs).

Logging & Audit: Central Logging sink exporting to BigQuery / Cloud Storage in logging-project.

Security: Security Command Center, Binary Authorization for container deployment, Container Analysis.

Billing: Billing Account per business unit or consolidated with billing export to BigQuery. Use labels/tags.

CI/CD: Cloud Build or GitHub Actions connected to Artifact Registry. Deploy with terraform or Deployment Manager.

Example service mappings per client (brief)

Philips-Prod: GKE (ML inference), Cloud Storage (HIPAA controls), Cloud SQL / BigQuery for analytics, VPC-SC.

GE-Prod: Cloud IoT Core (or Pub/Sub ingestion), Dataflow (stream processing), BigQuery (analytics), Looker/Datastudio.

Benz-Prod: Cloud Functions/API Gateway, Firestore or Bigtable for telemetry, Identity Platform for auth.

Cross-cloud considerations (real-time ops)

Identity federation: Use central identity provider (Azure AD or Cloud Identity) and setup SSO across AWS/Azure/GCP for consultants/dev teams.

Landing zones: Use IaC (Terraform) with modules for each cloud to enforce baseline (networking, logging, monitoring).

Centralized logging & SIEM: Aggregate important alerts into a central SIEM (Splunk / Elastic / or cross-cloud Sentinel/SCC integration).

Networking: Consider VPN/Direct Connect/Interconnect + Transit architecture for hybrid connectivity across clouds.

Policies & Guardrails: Map AWS SCPs → Azure Policy initiatives → GCP Organization Policy constraints consistently across clouds.

FinOps: Use cost allocation tags/labels consistently; central Cost/Chargeback reporting (Cost Explorer, Azure Cost Management, GCP Billing export).



| Feature / Aspect            | **AWS** (Organizations)                                                                            | **Azure** (Management Groups & Subscriptions)                                                          | **GCP** (Organization / Folders / Projects)                                                |
| --------------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| **Root Entity**             | Master AWS Organization Account (billing consolidated view)                                        | Azure AD Tenant (identity root) + Root Management Group                                                | GCP Organization (tied to Cloud Identity / Workspace domain)                               |
| **Hierarchy Levels**        | Org Root → Organizational Units (OUs) → Accounts                                                   | Root MG → Management Groups → Subscriptions                                                            | Org → Folders → Projects                                                                   |
| **Workload Container**      | **Account** (completely isolated environment, own IAM, billing unit)                               | **Subscription** (isolated billing & resource container)                                               | **Project** (IAM + billing unit, services/resources live here)                             |
| **Grouping Mechanism**      | **OU (Organizational Unit)** for grouping accounts                                                 | **Management Groups** for grouping subscriptions                                                       | **Folders** for grouping projects                                                          |
| **Shared Services Pattern** | Separate accounts (Logging, Security, Networking, Tooling)                                         | Separate subscriptions (Logging, Security, Networking, Tooling)                                        | Separate projects (logging-project, security-project, networking-project, tooling-project) |
| **Centralized Logging**     | Central Logging Account (CloudTrail, Config, S3 logs, GuardDuty findings)                          | Central Log Analytics Workspace + Storage Account                                                      | Logging sinks to **logging-project** → BigQuery / Cloud Storage                            |
| **Security Centralization** | Security Audit Account (Security Hub, GuardDuty, Config aggregator, IAM Analyzer)                  | Security Subscription (Sentinel, Defender for Cloud, central Key Vaults)                               | Security Project (Security Command Center, Forseti / Policy, IAM org policies)             |
| **Networking Hub**          | Networking Account (Transit Gateway, VPCs, Direct Connect, shared VPCs)                            | Networking Subscription (Hub VNet, Virtual WAN, ExpressRoute, shared services)                         | Networking Project (Shared VPC host project, Interconnect, Cloud NAT, VPN)                 |
| **Policy Controls**         | **SCPs (Service Control Policies)** applied at OU/account level                                    | **Azure Policy** & **RBAC** applied at MG/subscription level                                           | **Organization Policy Constraints** & IAM applied at org/folder/project level              |
| **IAM Model**               | IAM Users/Roles (but in enterprises mostly SSO → IdP like Azure AD/Okta via SAML)                  | Azure AD (central identity), RBAC roles assigned at MG/Sub/Resource Group levels                       | Cloud IAM (roles at Org/Folder/Project/resource level; groups recommended)                 |
| **Landing Zone**            | AWS Control Tower (or custom Terraform) for account vending + guardrails                           | Azure Landing Zones (CAF / Blueprints / Bicep / Terraform modules)                                     | Google Cloud Foundation Toolkit (Terraform/Deployment Manager for baseline setup)          |
| **Isolation Strength**      | **Accounts are hard isolation units** (best for security & billing separation)                     | Subscriptions are strong isolation, but identity is still shared under same Azure AD tenant            | Projects are isolation, but less “hard” than AWS accounts (still under same Org policies)  |
| **Billing Model**           | Consolidated billing at master account; CUR (Cost & Usage Report) → Athena/QuickSight for analysis | Cost Management + Billing by subscription, roll-up at tenant; Azure Cost Management + tags/initiatives | Billing account(s) → projects linked; export billing to BigQuery for FinOps                |
| **Tagging / Labeling**      | Resource Tags (Client, Env, Project, Owner, CostCenter)                                            | Tags + Azure Policy enforcement                                                                        | Labels on resources; enforced via Org Policy or custom scripts                             |
| **Example for Philips**     | `Philips-Prod` Account → EC2, RDS, S3, HIPAA controls                                              | `Philips-Prod` Subscription → AKS, SQL MI, Blob Storage w/ Private Link                                | `Philips-Prod` Project → GKE, Cloud SQL, BigQuery, HIPAA constraints via VPC-SC            |
| **Typical Shared Tooling**  | Jenkins / CodePipeline / Prometheus in Tooling Account                                             | Azure DevOps / GitHub Enterprise / Monitoring in Tooling Subscription                                  | Cloud Build / Artifact Registry / Stackdriver in Tooling Project                           |
| **Compliance Alignment**    | HIPAA, PCI, SOC2, FedRAMP via SCP + Config + Audit Account                                         | HIPAA, ISO27001, FedRAMP via Policy, Sentinel, Azure Monitor                                           | HIPAA, GDPR, ISO via Org Policies, Security Command Center, VPC-SC                         |

