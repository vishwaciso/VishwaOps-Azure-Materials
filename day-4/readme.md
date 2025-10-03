<!-- Header Banner -->

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1e3c72,100:2a5298&height=200&section=header&text=🌐%20Azure%20VNet%20—%20Portal%20(GUI)%20Step-by-Step&fontSize=36&fontColor=fff&animation=twinkling" />
</p>

# Azure VNet — Portal (GUI) Step-by-Step

> A copy-paste friendly `README.md` section that shows **exact GUI clicks** & visuals you follow in the Azure Portal to create a VNet, add subnets, attach NSGs/ASGs and verify everything.

---

## 📋 Table of contents

* [About / Purpose](#about--purpose)
* [Prerequisites](#prerequisites)
* [Step-by-step: Create Resource Group](#step-by-step-create-resource-group)
* [Step-by-step: Create Virtual Network (VNet)](#step-by-step-create-virtual-network-vnet)
* [Add / Edit Subnets (GUI)](#add--edit-subnets-gui)
* [Create and Attach an NSG (Network Security Group)](#create-and-attach-an-nsg-network-security-group)
* [Create an ASG (Application Security Group) and add NICs](#create-an-asg-application-security-group-and-add-nics)
* [Optional: Create Azure Firewall (GUI) — hub use-case](#optional-create-azure-firewall-gui---hub-use-case)
* [Verify & Troubleshoot (GUI checks)](#verify--troubleshoot-gui-checks)
* [Cleanup (delete resources)](#cleanup-delete-resources)

---

## About / Purpose

This `README` provides **pure GUI (Portal) steps** so anyone (including non-CLI users) can follow along and create a working Azure Virtual Network topology for dev/test or demo purposes.

Example outcome:

```
rg-myproject
└─ vnet-myproject  (10.10.0.0/16)
   ├─ web-subnet    (10.10.1.0/24)  -> NSG: nsg-web
   ├─ app-subnet    (10.10.2.0/24)  -> NSG: nsg-app, ASG: asg-app
   └─ db-subnet     (10.10.3.0/24)  -> NSG: nsg-db
```

---

## Prerequisites

* Azure account and access to [[https://portal.azure.com](https://portal.azure.com)].
* Role: **Owner** or **Contributor** (Network Contributor if restricted) on the subscription or resource group.
* Browser (Chrome/Edge) signed in to the correct subscription.

---

## Step-by-step: Create Resource Group

1. Open the Azure Portal: `https://portal.azure.com`.
2. In the left-hand menu, click **Resource groups**.
3. Click **+ Create**.
4. Fill:

   * **Subscription** → select your subscription
   * **Resource group** → `rg-myproject` (example)
   * **Region** → `East US` (choose one region)
5. Click **Review + Create** → click **Create**.

---

## Step-by-step: Create Virtual Network (VNet)

1. In the Portal top search bar, type **Virtual networks** and click the service.
2. Click **+ Create** → **Virtual network**.

**TAB: Basics**

* **Subscription** → choose your subscription
* **Resource group** → `rg-myproject`
* **Name** → `vnet-myproject`
* **Region** → same as RG (e.g., `East US`)

Click **Next: IP addresses** (button at the bottom).

**TAB: IP addresses**

* **Address space** → `10.10.0.0/16` (example)
* Under **Subnets**, click **+ Add subnet**

  * **Subnet name** → `web-subnet`
  * **Subnet address range** → `10.10.1.0/24`
  * Click **Add**

(You can add more subnets here or add later)

Click **Next: Security** → leave defaults (Basic DDoS) → **Next: Tags** → skip or add tags → **Review + Create** → **Create**.

**Wait a few seconds**; Deployment will complete and VNet will appear in the resource group.

---

## Add / Edit Subnets (GUI)

To add subnets after creating the VNet:

1. Open the **vnet-myproject** resource.
2. In the left blade, click **Subnets**.
3. Click **+ Subnet**.

   * **Name**: `app-subnet`
   * **Address range**: `10.10.2.0/24`
4. Click **Save** (or Add).

Repeat for `db-subnet` → `10.10.3.0/24`.

**Notes**:

* Use `GatewaySubnet` (exact name) only if you plan to deploy gateways.
* If you plan to use Azure Firewall later, create a dedicated subnet named **AzureFirewallSubnet** with at least `/26` size.

---

## Create and Attach an NSG (Network Security Group)

### Create NSG (GUI)

1. In the portal search bar, type **Network security groups** → open it.
2. Click **+ Create**.
3. Fill:

   * **Subscription** / **Resource group** → `rg-myproject`
   * **Name** → `nsg-web` (example)
   * **Region** → same region
4. Click **Review + Create** → **Create**.

### Add rules to NSG (example: allow HTTP/HTTPS to web)

1. Open **nsg-web**.
2. Under **Settings**, click **Inbound security rules** → **+ Add**.
3. Example rule to allow HTTP:

   * **Source**: Any
   * **Source port ranges**: *
   * **Destination**: Any
   * **Destination port ranges**: `80`
   * **Protocol**: `TCP`
   * **Action**: `Allow`
   * **Priority**: `300` (lower numeric = higher priority)
   * **Name**: `Allow-HTTP`
4. Click **Add**.

### Associate NSG with a Subnet (GUI)

1. Open **vnet-myproject** → click **Subnets**.
2. Click the subnet row (e.g., `web-subnet`).
3. In the subnet blade, find **Network security group** dropdown and select **nsg-web**.
4. Click **Save**.

**Alternative**: Associate NSG to a VM NIC by going to the VM → Networking → Attach NIC NSG.

---

## Create an ASG (Application Security Group) and add NICs

### Create ASG

1. Search **Application security groups** in the portal and open it.
2. Click **+ Create**.
3. Fill:

   * **Subscription / Resource group** → `rg-myproject`
   * **Name** → `asg-app`
4. Click **Review + Create** → **Create**.

### Add a NIC or VM to ASG

* When creating a VM via Portal: on the **Networking** tab, there is an **Application security groups** section — tick `asg-app` to add.
* For an existing VM:

  1. Open the VM → **Networking** → click the NIC link.
  2. On the NIC page, click **IP configurations** → select the IP configuration.
  3. Under **Application security groups**, click **+ Add** and choose `asg-app` → Save.

### Use ASG in NSG rules

* When creating NSG rules, you can pick `Source` or `Destination` as Application Security Group and select `asg-app` instead of IP addresses. This simplifies multi-tier rules.

---

## Optional: Create Azure Firewall (GUI) — hub use-case

> Use Azure Firewall when you need centralized, stateful, application-aware inspection (FQDN filtering, SNAT/DNAT, threat intel). For hub-and-spoke, place firewall in hub VNet.

### Create Firewall Subnet

1. In your hub VNet, go to **Subnets** → **+ Subnet**.
2. **Name** it exactly: `AzureFirewallSubnet`.
3. Use a prefix at least `/26` (e.g., `10.10.254.0/26`) and **Save**.

### Deploy Azure Firewall (GUI)

1. Search **Firewall** or **Azure Firewall** in the portal.
2. Click **+ Create** → **Firewall**.
3. Fill the form:

   * **Subscription / Resource group**: `rg-myproject`
   * **Name**: `fw-hub`
   * **Region**: same region
   * **Virtual network**: pick the hub VNet that includes `AzureFirewallSubnet`
   * **Public IP**: create a new public IP for NAT/egress
4. Click **Review + Create** → **Create**.

**Important**: Do **not** attach an NSG to `AzureFirewallSubnet`. Firewall needs to control traffic. Configure UDRs (user-defined routes) on spoke subnets to route to firewall as next hop if performing centralized inspection.

---

## Verify & Troubleshoot (GUI checks)

* **VNet**: Open `vnet-myproject` → check **Overview** for address space and subnets.
* **Subnet**: Open a subnet → check NSG association shown on the subnet blade.
* **NSG effective rules**: Open a VM NIC → **Effective security rules** to see the combined effect of NSG rules and ASG membership.
* **Network Watcher**: Use **IP flow verify**, **Next hop**, **Connection troubleshoot** to debug connectivity.
* **Deploy a test VM** in `web-subnet` and try to reach `80/443` from Internet (if you allowed it).

---

## Cleanup (delete resources)

1. If this was a test, you can delete the whole resource group to remove everything: Portal → Resource groups → open `rg-myproject` → **Delete resource group**.
2. Confirm by typing the resource group name and delete.

---

## Quick copy-paste example (names you can use)

```
Resource Group: rg-myproject
VNet: vnet-myproject (10.10.0.0/16)
Subnets:
  - web-subnet  (10.10.1.0/24)  -> NSG: nsg-web
  - app-subnet  (10.10.2.0/24)  -> NSG: nsg-app, ASG: asg-app
  - db-subnet   (10.10.3.0/24)  -> NSG: nsg-db
Optional: AzureFirewallSubnet (10.10.254.0/26) for Azure Firewall
```

---

## Want this combined with the earlier **Firewall vs NSG vs ASG** comparison or with the CLI/Terraform snippets?

I can add them as sections in the same `README.md`. Tell me which extra sections to include and I’ll append them.

---

*End of GUI step-by-step README content.*
