# ☁️ Vishwa's Tech Docs – Multi-Cloud Hierarchy

## Real-World Analogies First → Then Cloud Terms

Clouds may use different words, but the **concepts are very similar**.  
Let’s break it down using **real-world analogies** → then map them to **Azure, AWS, and GCP**.

---

### 🏢 1. Company HQ → Tenant / Account / Organization

- **Layman View:**  
  The **Company Headquarters (HQ)** where everything starts. All employees, offices, and projects belong here.  

- **Azure:** **Tenant** (Azure AD identity for the organization)  
- **AWS:** **Account** (root AWS account for a company)  
- **GCP:** **Organization** (top-level identity for a company in Google Cloud)  

---

### 🗄️ 2. Filing Cabinet → Management Group / Organization Unit

- **Layman View:**  
  Inside the HQ, you set up **filing cabinets** 🗄️ to organize by department (Finance, HR, IT).  

- **Azure:** **Management Group** (organize subscriptions, apply policies)  
- **AWS:** **Organizations → Organizational Units (OUs)** (group accounts, apply service control policies)  
- **GCP:** **Folders** (group projects by department or environment)  

---

### 💳 3. Electricity Bill Account → Subscription / Account / Project

- **Layman View:**  
  Each department pays its **own electricity bill account** 💳, even if it belongs to the same company.  

- **Azure:** **Subscription** (billing boundary + resource container)  
- **AWS:** **Account** (also the billing boundary, often managed under AWS Organizations)  
- **GCP:** **Project** (billing & resource container linked to an Org)  

---

### 📂 4. Project Folder → Resource Group / Resource Group / Project Namespace

- **Layman View:**  
  For each project, you create a **folder** 📂 on your computer that holds everything related.  

- **Azure:** **Resource Group (RG)** (logical container for resources)  
- **AWS:** **Resource Groups / Tags** (group resources for a project)  
- **GCP:** **Project itself acts as a container** (no separate RG, but can use **labels** for grouping)  

---

### 📄 5. Files → Resources

- **Layman View:**  
  Inside the folder, you have **files** (Word, Excel, images). These are the items you really use.  

- **Azure:** **Resources** (VMs, Databases, Storage Accounts, Networks)  
- **AWS:** **Resources** (EC2 instances, S3 buckets, RDS databases, VPCs)  
- **GCP:** **Resources** (VMs in Compute Engine, Buckets in Cloud Storage, BigQuery datasets)  

---

## 🔗 Multi-Cloud Hierarchy Visual

```mermaid
flowchart TD
    A[🏢 Company HQ<br/>Azure: Tenant<br/>AWS: Account<br/>GCP: Organization] 
      --> B[🗄️ Filing Cabinet<br/>Azure: Management Group<br/>AWS: Org Unit<br/>GCP: Folder]

    B --> C[💳 Electricity Bill<br/>Azure: Subscription<br/>AWS: Account<br/>GCP: Project]

    C --> D[📂 Project Folder<br/>Azure: Resource Group<br/>AWS: Resource Group/Tags<br/>GCP: Labels/Namespaces]

    D --> E[📄 Files<br/>Azure: Resources<br/>AWS: Resources<br/>GCP: Resources]
