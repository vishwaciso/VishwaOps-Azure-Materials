# ☁️ Vishwa's Tech Docs – Azure Tenant & Subscription Q&A

## 🎭 What is a Tenant?
- A **Tenant** is a dedicated, trusted instance of **Azure Active Directory (Azure AD)** that represents an **organization**.  
- It is created automatically when you sign up for Azure, Microsoft 365, or other Microsoft cloud services.  
- It is the **identity and security boundary** for users, groups, and applications.

---

## 🔀 Cross Questions on Tenant

**Q1. What is an Azure Tenant in simple terms?**  
➡️ A Tenant is like a **Company Headquarters (HQ)** 🏢 where all employees, apps, and resources are registered.

**Q2. What are the types of Tenants?**  
- **Microsoft 365 Tenant** → Created when you subscribe to Microsoft 365 services.  
- **Azure AD Tenant** → Created when you sign up for Azure services (identity + access).  
- **Hybrid Tenant** → A combination where Azure AD connects to on-premises AD (Active Directory Federation).  

**Q3. Can one user belong to multiple Tenants?**  
➡️ Yes ✅, a user can be a **guest user** in another Tenant via **Azure AD B2B collaboration**.

**Q4. How many Subscriptions can a Tenant have?**  
➡️ A single Tenant can have **many subscriptions (hundreds or thousands)**.  
This is how large enterprises separate billing for departments or projects.

---

## 💳 What is a Subscription?
- A **Subscription** is a **billing container** for Azure resources.  
- It defines **who pays the bill** and provides **limits & access control**.  
- Each subscription is linked to **one Tenant only**.

---

## 🔀 Cross Questions on Subscription

**Q1. What are the types of Subscriptions in Azure?**  
- **Free Trial** → $200 credit for 30 days.  
- **Pay-As-You-Go (PAYG)** → Pay only for what you use.  
- **Enterprise Agreement (EA)** → Volume licensing for large organizations.  
- **Microsoft Customer Agreement (MCA)** → Modern billing agreement.  
- **Student Subscription** → Free credit for students with valid academic email.  
- **Visual Studio/MSDN Subscription** → Monthly Azure credits for developers.  

**Q2. Can one Subscription belong to multiple Tenants?**  
➡️ ❌ No. A Subscription is always linked to **exactly one Tenant**.  
But you can **move a subscription** from one Tenant to another.

**Q3. Can one Tenant have multiple Subscriptions?**  
➡️ ✅ Yes. A Tenant can have **many subscriptions** (e.g., Finance-Sub, HR-Sub, IT-Sub).

**Q4. Why do companies use multiple Subscriptions?**  
- Separate **billing** for departments/projects.  
- Enforce **security boundaries**.  
- Manage **quotas & limits** per subscription.  
- Organize **environments** (Dev, Test, Prod).

---

## 🔗 Relationship Between Tenant & Subscription

| Question | Answer |
|----------|--------|
| Under one Tenant, how many Subscriptions can we create? | Many (unlimited in theory, practical limits in hundreds/thousands) |
| Under one Subscription, how many Tenants can we create? | Only ONE Tenant. A Subscription always belongs to a single Tenant. |

---

## 🔄 Visual Flow

```mermaid
flowchart TD
    A[🎭 Tenant<br/>Company HQ] --> B1[💳 Subscription 1<br/>Finance Dept]
    A --> B2[💳 Subscription 2<br/>HR Dept]
    A --> B3[💳 Subscription 3<br/>IT Dept]

    B1 --> C1[📂 Resource Groups + Resources]
    B2 --> C2[📂 Resource Groups + Resources]
    B3 --> C3[📂 Resource Groups + Resources]
