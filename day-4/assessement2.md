# 🧭 Azure Subscriptions & Resource Groups – Assessments & Lab Exercises

## 📘 Concept Overview
In Azure, everything is organized by **scope**:

**Management Group → Subscription → Resource Group → Resources**

- **Subscriptions** define billing boundaries.  
- **Resource Groups (RGs)** are logical containers for resources like VMs, Storage Accounts, etc.

---

## 🎯 Why We Do This
- To organize resources logically (per **department**, **project**, or **environment**).  
- To apply **access control (RBAC)** at the right level (Subscription or RG).  
- To optimize **billing and governance** across large organizations.

---

## 🧰 Tools Used
| Tool | Purpose |
|------|----------|
| **Azure Portal** | Visual resource and policy management |
| **Azure CLI** | Scripting (`az group create`, `az account list`) |
| **PowerShell** | Automation (`New-AzResourceGroup`) |
| **Cost Management + Azure Policy** | Governance & billing control |

---

## 🏢 Real-Time Use Cases
- Large enterprises use **multiple subscriptions** (per region or department).  
- **Resource Groups** simplify lifecycle management (delete RG → removes all resources).  
- **Tags** and **Policies** help in cost allocation & compliance.

---

## 🟢 Basic Level Assessments

### **Scenario 1: Organizing by Department**
**Story:**  
A company has HR, Finance, and IT teams. Each department uses its own subscription. Finance creates a **Payroll-RG** for salary-related VMs.

**Lab:**  
Create a new RG `Payroll-RG`, deploy a VM inside it.  
Then delete the RG and verify all resources are deleted automatically.

**Expected Outcome:**  
Learners see how RGs simplify **organization and cleanup**.

**Assessment Questions:**
1. What is a **Resource Group** and why is it important in Azure?  
2. What happens to resources when a Resource Group is deleted?  
3. Can a single resource belong to multiple RGs? Explain.  
4. Why should different departments have separate RGs or subscriptions?  
5. How can tagging help when multiple departments use the same subscription?

---

### **Scenario 2: Separate Environments (Dev & Prod)**
**Story:**  
Developers need separate environments. You create 2 RGs — **Dev-RG** and **Prod-RG**.

**Lab:**  
Deploy one VM in each RG and observe separation in the Azure Portal.

**Expected Outcome:**  
Learners understand **environment isolation** using Resource Groups.

**Assessment Questions:**
1. Why is it a best practice to separate Dev and Prod environments?  
2. Can two RGs exist under the same subscription?  
3. How can you quickly identify which environment a resource belongs to?  
4. What are the advantages of deleting a Dev RG after testing?  
5. How does this setup support governance and cost optimization?

---

## 🟡 Intermediate Level Assessments

### **Scenario 1: RBAC at Different Scopes**
**Story:**  
The HR team should manage the payroll VM but not production DB.  
Assign **Contributor** at RG level, **Reader** at Subscription level.

**Lab:**  
Create user `hruser@company.com`, assign roles, and test access.

**Expected Outcome:**  
Learners understand **role-based access control (RBAC)** across different scopes.

**Assessment Questions:**
1. What is **RBAC** and what are its key benefits?  
2. What’s the difference between **Contributor** and **Reader** roles?  
3. At which levels can RBAC be assigned in Azure?  
4. If a user has Contributor at RG scope and Reader at Subscription scope, what is their effective permission on the RG?  
5. Why should permissions be granted using the **least privilege principle**?

---

### **Scenario 2: Governance with Management Groups**
**Story:**  
An organization has 3 subscriptions – Dev, Test, and Prod. They want centralized control via a **Management Group**.

**Lab:**  
Create a Management Group and link all three subscriptions.

**Expected Outcome:**  
Learners understand **hierarchical governance** using Management Groups.

**Assessment Questions:**
1. What is a **Management Group** in Azure?  
2. How does it differ from a Subscription?  
3. Why do large enterprises prefer Management Groups?  
4. Can policies or RBAC be applied at the Management Group level?  
5. What happens if you move a Subscription from one Management Group to another?

---

### **Scenario 3: Tagging & Cost Analysis**
**Story:**  
Finance team adds tags like `Dept=Finance`, `Env=Prod` for cost tracking.

**Lab:**  
Add tags to RGs and resources. Use **Cost Analysis** in the Portal.

**Expected Outcome:**  
Learners understand **cost allocation and filtering by tags**.

**Assessment Questions:**
1. What are **Tags** in Azure and how do they help in cost management?  
2. Can tags be applied at both RG and Resource levels?  
3. What are some examples of useful tags for enterprises?  
4. How can Cost Analysis be filtered using tags?  
5. What is the limitation of tags in resource organization?

---

## 🔴 Advanced Level Assessments

### **Scenario 1: Multi-Subscription Billing Strategy**
**Story:**  
A multinational company with 10 subscriptions consolidates billing into one invoice.

**Lab:**  
Use **Cost Management** to link subscriptions and analyze combined billing.

**Expected Outcome:**  
Learners understand **enterprise billing and cost visibility**.

**Assessment Questions:**
1. Why do enterprises use multiple subscriptions?  
2. What is **consolidated billing** in Azure?  
3. How can you view cost for multiple subscriptions together?  
4. What’s the difference between **payer account** and **linked account**?  
5. How can tagging and budgets improve billing management?

---

### **Scenario 2: Azure Policy Enforcement**
**Story:**  
Company enforces all resources to be created only in **East US** region.  
Other regions are blocked using **Azure Policy**.

**Lab:**  
Create a region restriction policy, assign it at Subscription level, and test deployment in another region.

**Expected Outcome:**  
Learners understand **compliance enforcement** using Azure Policy.

**Assessment Questions:**
1. What is **Azure Policy** used for?  
2. How does a **policy assignment** differ from an **initiative**?  
3. What happens when a user tries to create a resource in a disallowed region?  
4. At what levels can Azure Policy be assigned (Management Group, Subscription, RG)?  
5. How can Azure Policy help maintain corporate compliance and standards?

---

### **Scenario 3: Resource Locks**
**Story:**  
A critical Production RG should not be deleted. Apply a **Delete Lock**.

**Lab:**  
Apply the lock and attempt to delete the RG → deletion fails.

**Expected Outcome:**  
Learners understand **accidental deletion protection**.

**Assessment Questions:**
1. What types of locks exist in Azure?  
2. How does a **Delete Lock** differ from a **Read-Only Lock**?  
3. Who can remove a lock from a Resource Group?  
4. Does a lock at RG level affect resources inside it?  
5. Why are locks considered part of Azure governance and security?

---

## ✅ Final Outcome
Learners will be able to:
- Organize Azure resources using **logical structure and governance**.  
- Apply **RBAC, Policies, and Locks** for compliance.  
- Implement **cost control and tagging** strategies effectively.  

---

## 🧠 Bonus Challenge (Optional)
- Create a hierarchy:  
  **Management Group → Subscription → Resource Group → Resource**
- Assign:  
  - Azure Policy at Management Group  
  - RBAC at RG level  
  - Apply cost tags and locks  
- Submit a screenshot of the full hierarchy in Azure Portal.

---

## 🗂️ Submission Format
1. **Lab Screenshots** (setup + verification)  
2. **CLI Commands / Portal Steps**  
3. **Answers to Assessment Questions (PDF/MD)**

---

**Author:** [Vishwa-Tech: The Coders' Kingdom](https://github.com/vishwa-tech)  
**Instructor:** Vishwanath (Cloud Security & DevSecOps Trainer)
