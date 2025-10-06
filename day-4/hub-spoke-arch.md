# 🏗️ Azure Hub-Spoke Network — Hands-On Challenge (GUI Only)

## 🎯 Final Mission

Design an **Enterprise-Grade Hub-Spoke Network in Azure** where:

- A **Hub VNet** contains an **Azure Firewall**
- Two **Spoke VNets** are connected to the Hub via **VNet Peering**
- **All traffic from both spokes is forced through the Firewall**
- You **verify routing, connectivity & firewall control**

Region for all resources: **East US**

---

## 🧭 IP & Naming Blueprint (Follow Exactly)

| Resource Type | Name | Address Space / Notes | Resource Group |
|---------------|------|----------------------|----------------|
| Hub VNet | `vnet-hub` | 10.0.0.0/16 | `rg-hub` |
| Subnet | `AzureFirewallSubnet` | 10.0.0.0/26 (**exact name & size required**) | `rg-hub` |
| Subnet | `hub-shared` | 10.0.1.0/24 | `rg-hub` |
| Spoke VNet 1 | `vnet-spoke1` | 10.1.0.0/16 | `rg-spoke1` |
| Subnet | `spoke1-app` | 10.1.1.0/24 | `rg-spoke1` |
| Spoke VNet 2 | `vnet-spoke2` | 10.2.0.0/16 | `rg-spoke2` |
| Subnet | `spoke2-app` | 10.2.1.0/24 | `rg-spoke2` |
| Public IP | `pip-firewall` | SKU: Standard | `rg-hub` |
| Azure Firewall | `azfw-hub` | Placed in `vnet-hub` | `rg-hub` |
| Route Table | `rt-spoke-default` | Default → Firewall | `rg-hub` or `rg-spoke1` |

---

## 🚀 Level 1 — Create Resource Groups

**Portal → Resource Groups → + Create → (Repeat for all)**

- `rg-hub`
- `rg-spoke1`
- `rg-spoke2`

✅ **Checkpoint:** All 3 resource groups exist in **East US**

---

## 🚀 Level 2 — Build the Hub VNet

**Portal → Create a Resource → Virtual Network**

- Name: `vnet-hub`
- Resource Group: `rg-hub`
- Address space: `10.0.0.0/16`
- Delete default subnet → Add:
  - Subnet 1: `AzureFirewallSubnet` → `10.0.0.0/26` **(Critical Rule!)**
  - Subnet 2: `hub-shared` → `10.0.1.0/24`

✅ **Checkpoint:** Subnets list shows **exactly** those two entries.

---

## 🚀 Level 3 — Build Spoke VNets

Repeat the above process for:

| VNet | Resource Group | Address Space | Subnet Name | Subnet Range |
|------|----------------|---------------|-------------|--------------|
| `vnet-spoke1` | `rg-spoke1` | 10.1.0.0/16 | `spoke1-app` | 10.1.1.0/24 |
| `vnet-spoke2` | `rg-spoke2` | 10.2.0.0/16 | `spoke2-app` | 10.2.1.0/24 |

✅ **Checkpoint:** Each VNet must have only **one subnet**.

---

## 🚀 Level 4 — Deploy Azure Firewall

1. **Create Public IP** → `pip-firewall`  
   - SKU: Standard  
   - Static

2. **Create Azure Firewall**
   - Name: `azfw-hub`
   - Resource Group: `rg-hub`
   - VNet: `vnet-hub` → it should auto-detect `AzureFirewallSubnet`
   - Attach `pip-firewall`

⏳ Wait for deployment...

✅ **Checkpoint:** Firewall should show **Private IP + Public IP**

---

## 🚀 Level 5 — Create Route Table for Spokes

**Portal → Route Tables → + Create → `rt-spoke-default`**

Then:

**Routes → + Add Route**

| Name | Address Prefix | Next Hop Type | Next Hop Address |
|------|---------------|---------------|------------------|
| default-to-firewall | 0.0.0.0/0 | Virtual appliance | `<FIREWALL_PRIVATE_IP>` |

✅ **Checkpoint:** Only **one route** exists.

---

## 🚀 Level 6 — Associate Route Table

Associate `rt-spoke-default` to:

- `vnet-spoke1 / spoke1-app`
- `vnet-spoke2 / spoke2-app`

✅ **Checkpoint:** Both subnets show route table attached.

---

## 🚀 Level 7 — Peer Hub ↔ Spokes

For each spoke:

### Hub → Spoke Peering

- Go to `vnet-hub → Peerings → + Add`
- Remote VNet: `vnet-spoke1` (repeat for spoke2)
- ✅ Enable **Allow forwarded traffic**
- (Optional for future VPN demo: Allow gateway transit)

### Spoke → Hub Peering

- Reverse peering from spoke → hub (portal usually auto-creates — verify!)

✅ **Checkpoint:** Peering status must be **Connected** on both sides.

---

## 🚀 Level 8 — Deploy Test VMs (No Public IPs)

| VM Name | Resource Group | VNet | Subnet | Public IP |
|---------|----------------|------|--------|-----------|
| `vm-spoke1` | `rg-spoke1` | vnet-spoke1 | spoke1-app | ❌ Disabled |
| `vm-spoke2` | `rg-spoke2` | vnet-spoke2 | spoke2-app | ❌ Disabled |

⚡ **Access Method:** Use **Azure Bastion** or temporarily assign public IP.

---

## 🔎 Level 9 — Validate Routing

On VM → Networking → **Effective Routes**

✅ Must show:

| Prefix | Next Hop Type | Next Hop Address |
|--------|----------------|------------------|
| 0.0.0.0/0 | Virtual appliance | `<Firewall Private IP>` |

---

## 🔥 Bonus Challenge — Prove Traffic Goes Through Firewall

From VM terminal (Linux):

```bash
curl https://ifconfig.co


| Challenge                         | Expected Failure    | Fix                  |
| --------------------------------- | ------------------- | -------------------- |
| Remove route table                | VMs bypass firewall | Re-associate RT      |
| Disable "Allow forwarded traffic" | VM-to-VM breaks     | Re-enable in peering |
| Change next-hop wrong             | No internet         | Correct firewall IP  |
