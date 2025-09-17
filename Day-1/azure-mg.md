# ☁️ Vishwa's Tech Docs – AWS Accounts vs Azure Subscriptions

## 📌 Introduction
Both **AWS** and **Azure** organize resources using **accounts (billing boundaries)** and **hierarchy layers**.  
While the terms differ, the concepts are similar.  
- **AWS → Root → Organizational Units (OUs) → Accounts → Resources**  
- **Azure → Tenant → Management Groups → Subscriptions → Resource Groups → Resources**

---

# 🟥 AWS Accounts in Detail

## 🔑 What is an AWS Account?
- An **AWS Account** is the **fundamental isolation and billing boundary** in AWS.  
- Each account has:  
  - Its own **Root User** (super admin).  
  - Its own **billing system**.  
  - Its own **IAM users, roles, and policies**.  
  - Its own **resources** (EC2, S3, RDS, etc.).  
- Accounts can be grouped under **AWS Organizations** for central management.

---

## 🏷️ Types of AWS Accounts
1. **Root Account** → The very first account created; has highest privileges.  
2. **Member Accounts** → Child accounts created under AWS Organizations.  
3. **Shared Service Accounts** → For centralized services like networking or logging.  
4. **Sandbox Accounts** → For developer experimentation.  
5. **Production Accounts** → For mission-critical workloads.  

---

## 📊 Why Multiple AWS Accounts?
- **Billing separation** → Finance, HR, IT each get their own bill.  
- **Security isolation** → One account’s failure doesn’t affect others.  
- **Service quotas** → AWS limits apply per account.  
- **Compliance** → Different legal requirements.  
- **Environment separation** → Dev, Test, Prod accounts.  

---

## 📈 AWS Accounts Visual

```mermaid
flowchart TD
    ROOT[🌍 Root] --> OU1[🗄️ OU: Finance]
    ROOT --> OU2[🗄️ OU: HR]
    ROOT --> OU3[🗄️ OU: IT]
    ROOT --> OU4[🗄️ OU: Security]

    OU1 --> ACC1[👤 Finance-Prod Account]
    OU1 --> ACC2[👤 Finance-Dev Account]

    OU2 --> ACC3[👤 HR-Prod Account]
    OU2 --> ACC4[👤 HR-Test Account]

    OU3 --> ACC5[👤 IT-Prod Account]
    OU3 --> ACC6[👤 IT-Dev Account]
    OU3 --> ACC7[👤 IT-Test Account]

    OU4 --> ACC8[👤 Security-Audit Account]
    OU4 --> ACC9[👤 Security-Logging Account]

    ACC1 --> R1[📄 Resources<br/>EC2, RDS, S3]
    ACC5 --> R2[📄 Resources<br/>EKS, Lambda, DynamoDB]
    ACC8 --> R3[📄 Resources<br/>GuardDuty, CloudTrail]
🟦 Azure Subscriptions in Detail
🔑 What is an Azure Subscription?
A Subscription is a billing container for Azure resources.

It defines who pays the bill and who can access resources.

Each subscription belongs to exactly one Tenant (Azure AD).

Without a Subscription, you cannot create resources in Azure.

🏷️ Types of Azure Subscriptions
Free Trial → $200 credit for 30 days.

Pay-As-You-Go (PAYG) → Pay only for what you use.

Enterprise Agreement (EA) → Volume licensing for enterprises.

Microsoft Customer Agreement (MCA) → New billing arrangement.

Student Subscription → Free credit for students.

Visual Studio / MSDN Subscription → Monthly credits for developers.

📊 Why Multiple Azure Subscriptions?
Billing separation → Project or department-based billing.

Security isolation → Limit user access per subscription.

Quota limits → Each subscription has service limits.

Environment separation → Dev, Test, UAT, Prod.

Chargeback → Easy cost allocation across teams.

📈 Azure Subscriptions Visual
mermaid
Copy code
flowchart TD
    TENANT[🎭 Tenant<br/>Company HQ] --> MG1[🗄️ Mgmt Group: Finance]
    TENANT --> MG2[🗄️ Mgmt Group: IT]
    TENANT --> MG3[🗄️ Mgmt Group: HR]

    MG1 --> SUB1[💳 Subscription: Finance-Prod]
    MG1 --> SUB2[💳 Subscription: Finance-Dev]

    MG2 --> SUB3[💳 Subscription: IT-Prod]
    MG2 --> SUB4[💳 Subscription: IT-Test]
    MG2 --> SUB5[💳 Subscription: IT-Dev]

    MG3 --> SUB6[💳 Subscription: HR-Prod]

    SUB1 --> RG1[📂 RG: Payroll]
    SUB1 --> RG2[📂 RG: Invoices]
    SUB3 --> RG3[📂 RG: ERP]
    SUB3 --> RG4[📂 RG: WebApps]

    RG1 --> AZR1[📄 VM, SQL DB, Storage]
    RG3 --> AZR2[📄 App Service, Cosmos DB, AKS]
⚖️ AWS Accounts vs Azure Subscriptions
Analogy	AWS Term	Azure Term
🏢 Company HQ	Root	Tenant
🗄️ Department Cabinet	Organizational Unit (OU)	Management Group
💳 Billing Account	AWS Account	Subscription
📂 Project Folder	Resource Groups/Tags	Resource Group
📄 Files	Resources (EC2, S3, RDS)	Resources (VM, DB, Storage)

📊 Line Graph Comparison
mermaid
Copy code
graph LR
    subgraph AWS 🟥
    A1[🌍 Root] --> A2[🗄️ OUs]
    A2 --> A3[👤 Accounts]
    A3 --> A4[📄 Resources]
    end

    subgraph Azure 🟦
    B1[🎭 Tenant] --> B2[🗄️ Mgmt Groups]
    B2 --> B3[💳 Subscriptions]
    B3 --> B4[📂 Resource Groups]
    B4 --> B5[📄 Resources]
    end
✅ Key Training Takeaways
AWS → Multi-account strategy (strong isolation, billing per account).

Azure → Multi-subscription strategy (all tied to a single Tenant).

Both models support:

Centralized billing

Policy enforcement

Environment separation

Scalability for enterprises

