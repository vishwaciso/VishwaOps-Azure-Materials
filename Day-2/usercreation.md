# 👥 Azure – Creating Multiple Users & Role Differences

This guide explains how to create multiple users in **Azure Active Directory (Entra ID)** and the difference between **Directory Roles** and **RBAC Roles**.

---

## 🔑 Step 1: Login to Azure Portal
1. Go to [Azure Portal](https://portal.azure.com/).  
2. Sign in with your **Azure admin account** (usually Global Admin or User Admin role).  
3. In the search bar, type **"Azure Active Directory"** (now called **Entra ID**) and open it.

---

## 👥 Step 2: Create Multiple Users
1. Inside **Azure Active Directory (Entra ID)** → Select **Users**.  
2. Click **+ New user** → **Create new user**.  
3. Fill in the details:
   - **User name** → e.g., `mukesh@yourdomain.onmicrosoft.com`  
   - **Name** → Mukesh Kumar  
   - **Password** → Auto-generate (user changes at first login)  
   - **Groups** (optional) → Assign to a team (e.g., Developers, HR, Finance)  
   - **Directory role** → Assign role (e.g., Global Reader, Security Admin)  
4. Click **Review + Create** → User is added.  
5. Repeat the same process to add more users.  

✅ For **bulk creation**, you can upload a **CSV file** in the **Users → Bulk create** option.  

---

## 🎭 Step 3: Assign Roles (Directory vs RBAC)
When creating a user, you will see **Directory roles** (Azure AD roles).  
For resources, you will use **RBAC roles** (Azure Resource Manager roles).

Here’s the difference:

| Feature | **Directory Roles (Azure AD / Entra ID)** | **RBAC Roles (Azure Resources)** |
|---------|-------------------------------------------|-----------------------------------|
| **Scope** | Applies at **tenant / directory level** (identity & access to Azure AD itself) | Applies at **resource level** (subscription, RG, VM, storage, etc.) |
| **Purpose** | Manage **users, groups, apps, directory settings** | Manage **Azure resources** like VMs, Storage, Databases, Networks |
| **Examples** | Global Admin, User Admin, Security Reader, Application Admin | Owner, Contributor, Reader, Storage Blob Data Contributor |
| **Where Assigned?** | In **Azure AD (Entra ID)** under user roles | In **Azure Resource Manager (ARM)** at subscription, RG, or resource level |
| **Real-Time Example** | - HR manager needs to create & manage employee accounts → Assign **User Admin** (Directory Role) <br> - Security team monitors sign-ins → Assign **Security Reader** | - DevOps engineer needs to deploy resources in Dev RG → Assign **Contributor** (RBAC) <br> - Finance team should only view billing data → Assign **Reader** (RBAC) |

---

## 🚀 Real-World Use Case
- **Directory Role:**  
  A company’s **IT Admin** manages all employee logins, password resets, MFA, and app registrations → needs **User Administrator (Directory Role)**.  

- **RBAC Role:**  
  The **DevOps Team** deploys VMs, AKS clusters, and storage accounts in **Dev Resource Group** → needs **Contributor (RBAC Role)**.  

---

## 📌 Best Practice
- Use **least privilege** → give minimum role required.  
- Combine **Directory Roles + RBAC Roles** when a user needs both identity & resource access.  
- For multiple users → use **Groups** and assign roles at group level (easier management).  

---
