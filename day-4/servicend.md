# 🔗 Azure Storage Service Endpoint Lab — Hands-On Challenge (GUI Only)

## 🎯 Final Mission

Implement **Service Endpoint** access to an **Azure Storage Account** so that:

- The storage account only allows traffic from your **VNet/subnet**.
- Public network access is still present, but restricted via Service Endpoint firewall rules.
- Learners validate connectivity from a VM inside the VNet and observe public network behavior.

**Region:** East US

**Learning Objective:** Understand **Service Endpoints vs Private Endpoints** in practice and see how they control traffic.

---

## 🖼️ Cheat Sheet — Service Endpoint vs Private Endpoint



               +------------------------+
               |  Azure PaaS Resource   |
               |  (Storage / SQL / etc)|
               +------------------------+
                          ▲
                          │ Public IP still exists
                          │ (traffic restricted via firewall)
                          │
             Service Endpoint│
                          │
+----------------+ +----------------+
| VNet Subnet |------------| Trusted Access |
| 10.10.1.0/24 | | via Service EP |
+----------------+ +----------------+
VM inside VNet
Access Allowed ✅

Outside VNet
Access may still work if public endpoint enabled

               +------------------------+
               |  Azure PaaS Resource   |
               |  (Storage / SQL / etc)|
               | Private IP assigned   |
               +------------------------+
                          ▲
                          │
                          │
                          │
+----------------+ +----------------+
| VNet Subnet |------------| Private Access |
| 10.10.1.0/24 | | via Private IP |
+----------------+ +----------------+
VM inside VNet
Access Allowed ✅

Outside VNet
Access Blocked ❌



| Feature | Service Endpoint | Private Endpoint |
|---------|----------------|----------------|
| Private IP in VNet | ❌ No | ✅ Yes |
| DNS change required | ❌ No | ✅ Yes (Private DNS) |
| Public endpoint | Exists (restricted via firewall) | Can be disabled |
| Security | Subnet trust only | Zero-trust, fully private |
| Ease of setup | ✅ Simple | ⚠️ More steps |
| Use Case | Quick subnet restriction | Full private/internal access enforcement |

---

## 🧭 Resource Blueprint (copy/paste)

| Item | Name / Value |
|------|--------------|
| Resource Group | `rg-service` |
| VNet | `vnet-se-lab` — 10.20.0.0/16 |
| Subnet | `app-subnet` — 10.20.1.0/24 |
| Storage Account | `stse<your initials>` (must be globally unique) |
| Service Endpoint | Enabled for Storage on subnet |
| Test VM | `vm-app-se` (no public IP recommended) |

---

## 🚀 Level 0 — Prep

1. Portal → **Resource groups** → **+ Create** → `rg-service` (East US)  
2. Portal → **Virtual networks** → **+ Create** → `vnet-se-lab`  
   - Address space: 10.20.0.0/16  
   - Subnet: `app-subnet` → 10.20.1.0/24

✅ **Checkpoint:** RG & VNet exist in East US.

---

## 🚀 Level 1 — Create the Storage Account

1. Portal → **Storage accounts** → **+ Create**  
   - Resource group: `rg-service`  
   - Name: `stse<yourid>` (globally unique)  
   - Region: East US  
   - Performance: Standard, Replication: LRS  
2. Deploy and wait for completion

✅ **Checkpoint:** Storage account appears in portal.

---

## 🚀 Level 2 — Enable Service Endpoint

1. Portal → **Virtual Networks → vnet-se-lab → Subnets → app-subnet → Service endpoints → + Add**  
2. Select **Microsoft.Storage**  
3. Save changes

✅ **Checkpoint:** Subnet now has Service Endpoint enabled for Storage.

---

## 🚀 Level 3 — Configure Storage Firewall

1. Portal → **Storage Account → Networking → Firewalls and virtual networks**  
2. Select **Selected networks**  
3. Add `vnet-se-lab / app-subnet` under **Virtual Networks**  
4. Keep **Public network access enabled** (Service Endpoint restricts traffic, public still exists)  
5. Save

✅ **Checkpoint:** Only VNet/subnet traffic allowed via Service Endpoint; other subnets are denied unless public endpoint allowed.

---

## 🚀 Level 4 — Deploy Test VM

| VM Name | Resource Group | VNet | Subnet | Public IP |
|---------|----------------|------|--------|-----------|
| `vm-app-se` | `rg-service` | vnet-se-lab | app-subnet | ❌ Disabled |

Access VM via **Bastion** for testing.

---

## 🔎 Level 5 — Test Connectivity

1. SSH into `vm-app-se`  
2. Test blob access:

```bash
az storage container create --account-name stse<yourid> --name test-container
az storage blob upload --account-name stse<yourid> --container-name test-container --name test.txt --file ./test.txt
