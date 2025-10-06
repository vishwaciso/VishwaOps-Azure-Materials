# 🔒 Azure Private Endpoint Lab — Hands-On Challenge (GUI Only)

## 🎯 Final Mission

Implement **Private Endpoint** access to an **Azure Storage Account** so that:

- The storage account is accessible **only** from your VNet via a **Private Endpoint** (Private Link).
- Public network access is **disabled** and requests from the public internet are denied.
- Learners validate connectivity from a VM inside the VNet and confirm public access is blocked.

**Region:** East US

**Why this matters:** Private Endpoints place a private IP in your VNet for Azure services so traffic traverses Microsoft’s backbone — removing public exposure. 

---

## 🧭 Names & IP Plan (copy/paste)

| Item | Name / Value |
|------|--------------|
| Resource Group | `rg-private` |
| VNet | `vnet-lab` — `10.10.0.0/16` |
| Subnet (apps) | `app-subnet` — `10.10.1.0/24` |
| Storage Account | `stpriv\<your initials\>` (use globally unique name) |
| Private Endpoint | `pe-stpriv` |
| Private DNS Zone | `privatelink.blob.core.windows.net` (auto created or manual) |
| Test VM | `vm-app` (no public IP recommended) |

---

## 🚀 Level 0 — Prep (one-time)

1. Portal → **Resource groups** → **+ Create** → `rg-private` (Region: East US).  
2. Portal → **Virtual networks** → **+ Create** → `vnet-lab` (10.10.0.0/16). Add subnet:
   - `app-subnet` → 10.10.1.0/24

✅ **Checkpoint:** RG & VNet exist in East US.

> References: Microsoft tutorials explain these prerequisites for private endpoint workflows. 

---

## 🚀 Level 1 — Create the Storage Account

1. Portal → **Storage accounts** → **+ Create**.  
   - Resource group: `rg-private`  
   - Name: `stpriv<yourid>` (must be globally unique)  
   - Region: **East US**  
   - Performance/Replication: pick Standard / LRS for lab  
2. Create the account and wait for deployment.

✅ **Checkpoint:** Storage account `stpriv...` appears in portal.

> Tip: For labs, use Blob (general-purpose v2) type; you’ll create a container to test later. 

---

## 🚀 Level 2 — Disable Public Network Access (Lock it down)

1. Portal → **Storage accounts** → select your storage account.  
2. In the left menu: **Networking** → **Firewalls and virtual networks**.  
3. Under **Public network access**, select **Disabled**.  
4. **Save**.

✅ **Checkpoint:** The storage account now rejects public network access; any attempt from the internet will be denied. 

> Teaching note: disabling public access is the critical step that ensures the only way to reach the storage is via a private endpoint (or allowed Microsoft service exceptions). Demonstrate the change by trying to access blob endpoint from your laptop (should fail). 

---

## 🚀 Level 3 — Create the Private Endpoint (Portal)

1. Portal → Search **Private endpoints** → **+ Create**. (Or: Storage account → Networking → Private endpoint connections → **+ Private endpoint**). 
2. **Basics**:
   - Subscription, Resource group: `rg-private`
   - Name: `pe-stpriv`
   - Region: **East US**
3. **Resource** tab:
   - Resource type: **Microsoft.Storage/storageAccounts**
   - Resource: select `stpriv...`
   - Target sub-resource: choose `blob` (or `file`, `queue` as needed)
4. **Networking** tab:
   - Virtual network: `vnet-lab`
   - Subnet: `app-subnet`
   - Option: Enable **Integrate with private DNS zone** (recommended) — portal can create / link `privatelink.blob.core.windows.net` for you. (If not, you must create a Private DNS zone and link it.) 
5. **Review + Create** → **Create**.

✅ **Checkpoint:** Private endpoint `pe-stpriv` is provisioned and has a private IP in `app-subnet`.

---

## 🚀 Level 4 — Verify DNS (Private FQDN resolves to the Private IP)

Private Endpoint depends on DNS so that `storageaccount.blob.core.windows.net` resolves to the private IP.

**Portal auto-link path (recommended):** When creating the private endpoint, choose **Integrate with private DNS zone** — the portal will create the zone `privatelink.blob.core.windows.net` and add the `A` record that maps your storage account FQDN to the private IP. 

**Manual approach (if you skipped auto integration):**

1. Portal → **Private DNS zones** → **+ Create** → `privatelink.blob.core.windows.net`.  
2. In the zone, **+ Record set** → Name = `<your storage account>` (no suffix), type = A, value = `<private IP from private endpoint>` (portal shows this).  
3. Link the DNS zone to `vnet-lab` (Virtual network links → +).

**Validation (from VM):**

- On `vm-app` (inside `vnet-lab`), run:
  ```bash
  nslookup <stpriv>.blob.core.windows.net


🔎 Level 5 — Test Connectivity from VM (inside VNet)

Deploy a Linux VM (vm-app) into vnet-lab → app-subnet (no public IP recommended; use Bastion for interactive access).

SSH via Bastion / Jump host.

On vm-app:

# Optional: install azure-cli or curl
curl -I https://<stpriv>.blob.core.windows.net/<container>/<blob>


Or use az storage blob download with a SAS token (if configured).

✅ Expected: Request succeeds (HTTP 200 / blob returned) because traffic flows over the private link. DNS resolves to private IP.

🔥 Level 6 — Prove Public Access is Blocked

From outside your VNet (your laptop / home PC):

Attempt:

curl -I https://<stpriv>.blob.core.windows.net/<container>/<blob>


✅ Expected: Connection is refused or 403/404 — public network access is disabled, so external requests cannot reach the resource. (If you previously used a public access policy, you may need to revoke it.)

Extra verification: Portal → Storage account → Networking → Check if there are any allowed networks — confirm that only Private Endpoint appears.

Reference: Microsoft tutorial shows the disable-public-access + private endpoint flow and testing steps.

🧨 Break & Fix Challenges (Trainer Playbook)
Broken Lab	Symptom	Learner Fix
DNS not resolving to private IP	nslookup returns public IP	Create/Link Private DNS zone privatelink.blob.core.windows.net to vnet-lab or enable auto integration on PE
Public access still allowed	External curl returns 200	Re-check Storage Networking → Public network access = Disabled; remove any firewall rules allowing "All networks"
VM cannot reach storage	Timeout / Connection refused	Check subnet NSG, UDRs, and if private endpoint NIC shows healthy status in portal
Wrong sub-resource chosen	Access to blob fails but file works	Re-create or add additional Private Endpoint for blob sub-resource
✅ Final Outcome (What learners will demonstrate)

They can create a storage account and private endpoint via the Azure Portal.

They can disable public network access on the storage account to force traffic through Private Link.

They can configure or confirm Private DNS so the storage FQDN resolves to the private IP and validate access from an in-VNet VM.
