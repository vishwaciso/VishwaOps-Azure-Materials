# 🌐 Azure Networking & PaaS Labs — Hands-On Corporate Training

Welcome! This repository contains **3 progressive Azure labs** for corporate training:

1. **Hub-Spoke Architecture Lab**
2. **Private Endpoint Lab (Storage Account)**
3. **Service Endpoint Lab (Storage Account)**

**Region:** East US  
**Environment:** GUI-only (Azure Portal)

---

## 📖 Table of Contents

1. [Scenario 1: Hub-Spoke Architecture](#scenario-1---hub-spoke-architecture-lab)
2. [Scenario 2: Private Endpoint Lab](#scenario-2---private-endpoint-lab-azure-storage)
3. [Scenario 3: Service Endpoint Lab](#scenario-3---service-endpoint-lab-azure-storage)
4. [Cheat Sheet: Service Endpoint vs Private Endpoint](#cheat-sheet-service-endpoint-vs-private-endpoint)
5. [Tips & Break/Fix Challenges](#tips--breakfix-challenges)

---

## Scenario 1 — Hub-Spoke Architecture Lab

### 🎯 Objective
Design an **Enterprise-Grade Hub-Spoke Network**:

- Hub VNet with **Azure Firewall**
- Two Spoke VNets connected via **VNet Peering**
- All traffic forced through the firewall

### 🧭 IP & Naming Blueprint

| Resource | Name | Address Space | Resource Group |
|----------|------|---------------|----------------|
| Hub VNet | vnet-hub | 10.0.0.0/16 | rg-hub |
| Subnet | AzureFirewallSubnet | 10.0.0.0/26 | rg-hub |
| Subnet | hub-shared | 10.0.1.0/24 | rg-hub |
| Spoke VNet1 | vnet-spoke1 | 10.1.0.0/16 | rg-spoke1 |
| Subnet | spoke1-app | 10.1.1.0/24 | rg-spoke1 |
| Spoke VNet2 | vnet-spoke2 | 10.2.0.0/16 | rg-spoke2 |
| Subnet | spoke2-app | 10.2.1.0/24 | rg-spoke2 |
| Firewall | azfw-hub | - | rg-hub |
| Public IP | pip-firewall | Standard | rg-hub |
| Route Table | rt-spoke-default | Default → Firewall | rg-hub |

### 🚀 Steps

1. **Create Resource Groups:** `rg-hub`, `rg-spoke1`, `rg-spoke2`  
2. **Create Hub VNet** with subnets: `AzureFirewallSubnet` (10.0.0.0/26) + `hub-shared` (10.0.1.0/24)  
3. **Create Spoke VNets** and subnets (`spoke1-app`, `spoke2-app`)  
4. **Deploy Azure Firewall** with public IP `pip-firewall`  
5. **Create Route Table** `rt-spoke-default` and add route `0.0.0.0/0 → Firewall Private IP`  
6. **Associate Route Table** to spoke subnets  
7. **Peer Hub ↔ Spokes** (enable “Allow forwarded traffic”)  
8. **Deploy Test VMs** (no public IP) and validate effective routes  
9. **Verify traffic flows via firewall** (curl or NSG diagnostics)

✅ Outcome: Learners can design a secure, scalable Hub-Spoke architecture.

---

## Scenario 2 — Private Endpoint Lab (Azure Storage)

### 🎯 Objective
Secure a **Storage Account** so traffic flows only via **Private Endpoint**.

### 🧭 Resource Blueprint

| Item | Name / Value |
|------|--------------|
| Resource Group | rg-private |
| VNet | vnet-lab 10.10.0.0/16 |
| Subnet | app-subnet 10.10.1.0/24 |
| Storage Account | stpriv\<yourid> |
| Private Endpoint | pe-stpriv |
| Private DNS Zone | privatelink.blob.core.windows.net |
| Test VM | vm-app |

### 🚀 Steps

1. Create **Resource Group** `rg-private`  
2. Create **VNet** `vnet-lab` and subnet `app-subnet`  
3. Create **Storage Account** `stpriv<yourid>`  
4. Disable **public network access**  
5. Create **Private Endpoint** in `app-subnet` (integrate with private DNS)  
6. Deploy **VM in VNet** and test blob access  
7. Validate **public access denied** from outside VNet

✅ Outcome: Learners implement **zero-trust networking**.

---

## Scenario 3 — Service Endpoint Lab (Azure Storage)

### 🎯 Objective
Restrict Storage Account to **VNet/subnet access** using **Service Endpoints**.

### 🧭 Resource Blueprint

| Item | Name / Value |
|------|--------------|
| Resource Group | rg-service |
| VNet | vnet-se-lab 10.20.0.0/16 |
| Subnet | app-subnet 10.20.1.0/24 |
| Storage Account | stse<yourid> |
| Service Endpoint | Enabled on subnet |
| Test VM | vm-app-se |

### 🚀 Steps

1. Create **Resource Group** `rg-service`  
2. Create **VNet** `vnet-se-lab` + subnet `app-subnet`  
3. Create **Storage Account** `stse<yourid>`  
4. Enable **Service Endpoint** for Microsoft.Storage on `app-subnet`  
5. Configure **Storage Firewall** → allow only VNet/subnet  
6. Deploy **VM in subnet** and validate connectivity  
7. Optional: test access from outside VNet — public access may still work

✅ Outcome: Learners understand Service Endpoint behavior vs Private Endpoint.

---

## Cheat Sheet — Service Endpoint vs Private Endpoint

Service Endpoint (VNet Trusted)
+----------------+ +----------------+
| VNet Subnet |------------| Storage/SQL |
+----------------+ +----------------+
VM inside VNet ✅ Access
Outside VNet ⚠️ Access may still work

Private Endpoint (Private IP in VNet)
+----------------+ +----------------+
| VNet Subnet |------------| Storage/SQL |
+----------------+ +----------------+
VM inside VNet ✅ Access
Outside VNet ❌ Access Blocked



| Feature | Service Endpoint | Private Endpoint |
|---------|----------------|----------------|
| Private IP in VNet | ❌ | ✅ |
| DNS change required | ❌ | ✅ |
| Public endpoint | Exists | Can be disabled |
| Security | Subnet trust only | Zero-trust |
| Ease of setup | ✅ Simple | ⚠️ More steps |

---

## Tips & Break/Fix Challenges

| Broken Lab | Symptom | Learner Fix |
|-----------|---------|-------------|
| Route Table missing | Traffic bypass firewall | Associate correct RT |
| Private Endpoint DNS not working | VM cannot resolve storage | Check private DNS integration |
| Service Endpoint firewall misconfigured | VM from other subnet can access | Verify selected VNet/subnet only |
| Public access bypass | External VM can access storage | Compare Service Endpoint vs Private Endpoint |

---

## ✅ Trainer Notes

- Encourage learners to **compare Scenario 2 vs Scenario 3**  
- Show **VM outside VNet** trying to access both storage accounts  
- Discuss **zero-trust principles** and **corporate design implications**  
- Use **Break & Fix challenges** for interactive sessions

---

🎉 **You now have a single, comprehensive README** ready for **corporate Azure networking & PaaS training**.  

---




