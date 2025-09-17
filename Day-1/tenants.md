# ☁️ Vishwa's Tech Docs – Azure Hierarchy

## Understanding Tenant, Management Groups, Subscriptions, Resource Groups & Resources

Azure organizes everything in a **hierarchical structure** so that enterprises can manage identity, billing, access, and resources in a logical way.

---

<details>
<summary>🎭 <b>1. Tenant – The Organization Identity</b></summary>

**Definition:**  
- A Tenant is your **organization’s dedicated identity** in Azure, powered by **Azure Active Directory (Azure AD)**.  
- It’s created when a company signs up for Microsoft Azure or Microsoft 365.  
- Every **user, group, and application** lives here.  

**Layman’s Example:**  
Think of a **Tenant as your company headquarters (HQ)** 🏢 where all employees and official records are maintained.  

</details>

---

<details>
<summary>🏢 <b>2. Management Group – The Parent Folder</b></summary>

**Definition:**  
- A Management Group is used to **organize multiple subscriptions** under a single umbrella.  
- It helps apply **policies, compliance, and governance** across different business units.  
- Large enterprises use it to structure **departments, environments (Dev/Test/Prod), or regions**.  

**Layman’s Example:**  
A **Management Group is like a big filing cabinet** 🗄️ that holds multiple department folders.  

</details>

---

<details>
<summary>💳 <b>3. Subscription – The Billing Account</b></summary>

**Definition:**  
- A Subscription is a **billing boundary** in Azure.  
- It defines **who pays** for the services and provides access/control to resources.  
- Each subscription is linked to one Tenant.  

**Layman’s Example:**  
A **Subscription is like your electricity bill account** ⚡.  
Each house (subscription) gets its own bill, even if all belong to the same company HQ (Tenant).  

</details>

---

<details>
<summary>📂 <b>4. Resource Group – The Project Folder</b></summary>

**Definition:**  
- A Resource Group (RG) is a **logical container** for Azure resources.  
- You place related services for a **single project/application** inside one RG.  
- Deleting a RG removes all resources within it.  

**Layman’s Example:**  
A **Resource Group is like a project folder** 📂 on your computer.  
Delete the folder → all files inside are gone too.  

</details>

---

<details>
<summary>🖥️ <b>5. Resources – The Actual Services</b></summary>

**Definition:**  
- Resources are the **individual services** you create in Azure.  
- Examples:  
  - Virtual Machines (VMs) 🖥️  
  - Databases 🗄️  
  - Storage Accounts 📦  
  - Virtual Networks 🌐  

**Layman’s Example:**  
Resources are the **actual files inside your project folder** (Word docs, Excel sheets, images).  

</details>

---

## 🔗 Azure Hierarchy Flow

```mermaid
flowchart TD
    A[🎭 Tenant<br/>Company HQ] --> B[🏢 Management Group<br/>Filing Cabinet]
    B --> C[💳 Subscription<br/>Billing Account]
    C --> D[📂 Resource Group<br/>Project Folder]
    D --> E[🖥️ Resources<br/>Actual Services]
