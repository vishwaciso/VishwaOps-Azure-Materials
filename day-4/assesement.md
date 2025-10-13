# 🧠 Azure Networking Module — Assessment Plan

---

## 🗂️ 1. Assessment Format

| Type | Purpose | Example Count |
|------|----------|----------------|
| **Theory (MCQs + Short Answers)** | Check conceptual understanding | 10–12 Questions |
| **Scenario-Based Questions** | Check problem-solving & design thinking | 3–5 Questions |
| **Lab Tasks (Hands-On)** | Check practical Azure skills | 3–5 Tasks |

---

## 💡 Section 1: Theory / MCQ Questions (Basic Understanding)

1. What is the purpose of a **Virtual Network (VNet)** in Azure?  
   a) Provide compute resources  
   b) Provide isolated network environment  
   c) Store data  
   d) Manage subscriptions  

2. Which component divides a VNet into smaller logical segments?  
   a) Peering  
   b) Subnets  
   c) NSG  
   d) Route Table  

3. What is the default direction for **NSG rules** if not specified?  
   a) Inbound  
   b) Outbound  
   c) Both  
   d) None  

4. You can connect two VNets using ________.  
   a) Peering  
   b) Load balancer  
   c) Application Gateway  
   d) Azure Policy  

5. Which Azure tool helps diagnose and monitor network traffic?  
   a) Azure Advisor  
   b) Network Watcher  
   c) Monitor Logs  
   d) Sentinel  

6. What is the difference between **Private Endpoint** and **Service Endpoint**? *(Short Answer)*  

7. What happens if you apply an **NSG rule with deny RDP (3389)** on a subnet where a VM is hosted?  

8. Why is **Hub-Spoke architecture** preferred in enterprise environments?  

9. In Azure, how can you restrict a **Storage Account** to accept only internal VNet traffic?  

10. Define **VNet Peering** and mention one real-time use case.  

---

## 🧩 Section 2: Scenario-Based Questions (Intermediate Level)

1. You have 2 VNets in different regions — `Prod-VNet` and `Dev-VNet`.  
   You want secure communication between them without using the internet.  
   👉 What Azure feature will you use and why?  

2. Your application has a **Web tier** and a **Database tier**.  
   You want only the Web tier to communicate with the DB tier, and block everything else.  
   👉 Which Azure networking features will you configure?  

3. A company wants to connect its **on-premises data center** to Azure securely.  
   👉 Which service would you use and what are the key components?  

4. You have multiple **Spoke VNets** (Finance, HR, IT) that need to share security policies and internet access via a central firewall.  
   👉 How will you design the architecture?  

5. You want to allow only **HTTP (port 80)** traffic and deny **SSH (port 22)** on your Linux VM.  
   👉 How can this be done using NSG rules?  

---

## 🧑‍💻 Section 3: Hands-On / Lab Assessment Tasks

---

### 🧩 Basic Level

#### 1. VNet + Subnets Creation
- Create a VNet named **CorpVNet** with two subnets: `WebSubnet` and `DBSubnet`.  
- Deploy one VM in each subnet.  
- Ping between them and show **subnet-level isolation**.

#### 2. NSG Rule Control
- Create an NSG for **WebSubnet**.  
- Deny inbound RDP (3389) and test remote connection → it should fail.  
- Modify NSG to allow RDP → it should succeed.

---

### ⚙️ Intermediate Level

#### 3. VNet Peering
- Create **VNetA** and **VNetB**.  
- Peer them and ensure VMs in both VNets can communicate using private IPs.

#### 4. VPN Gateway Hybrid
- Create a **VPN Gateway** and connect to a local VM acting as an on-prem network.  
- Verify hybrid connectivity.

#### 5. Priority Rules
- Create **NSG rules** where HTTP is allowed and SSH is denied.  
- Test both using a browser and SSH client.

---

### 🏗️ Advanced Level

#### 6. Hub-Spoke Architecture
- Create a **Hub VNet** with Azure Firewall or NVA.  
- Connect 2 **Spoke VNets** via peering.  
- Route traffic through the Hub for inspection.

#### 7. Private Endpoint
- Create an **Azure Storage Account** and add a **Private Endpoint**.  
- Try accessing it via public IP → it should fail.

#### 8. Service Endpoint
- Create **Azure SQL** and configure a **Service Endpoint** from your VNet.  
- Ensure only that VNet can access the DB.

---

## 🎯 Final Outcomes
✅ Learners can design **secure, scalable, hybrid-ready Azure networks** including:
- VNets, Subnets, NSGs, Peering  
- Hub-Spoke design  
- Service & Private Endpoints  
- VPN Gateway hybrid connectivity  

---

## 🏁 Bonus Challenge
> Design a **complete Hub-Spoke network** with:
> - One Hub (Firewall + Bastion)  
> - Two Spokes (Web + DB)  
> - Private Endpoint for Storage  
> - Peering + NSG + Route Table setup  
> - Include a **network diagram + screenshots** as part of submission.  

---

### 🏆 Evaluation Criteria

| Skill | Weightage |
|-------|------------|
| **Conceptual Knowledge (Theory)** | 30% |
| **Scenario Understanding** | 30% |
| **Practical Execution (Labs)** | 40% |

---

📘 **Author:** Vishwa-Tech — *The Coders' Kingdom*  
💬 *Empowering learners to master Cloud Security & DevOps hands-on!*
