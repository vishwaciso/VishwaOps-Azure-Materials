# 🖥️ Azure VPN Gateway — Hybrid Lab (GUI Mode)

## 🎯 Objective

Create a **Site-to-Site (S2S) VPN** between Azure and an **on-premises emulator** (local VM or another Azure VM) — using only the **Azure Portal (GUI)**.

---

## 🧩 Architecture

```
[On-Prem Emulator VM] (10.99.0.0/24)
       |  🔐 IPsec/IKE tunnel
       |
[Azure VPN Gateway] (Public IP)
       |
[Azure VNet]
  ├── GatewaySubnet (10.1.255.0/27)
  └── AppSubnet     (10.1.0.0/24)
```

---

## 🪜 Step-by-Step Guide (Azure Portal GUI)

### ✅ **Step 1: Create a Resource Group**

* Go to **Azure Portal → Resource Groups → + Create**
* **Name:** `rg-vpnlab`
* **Region:** East US (or your preferred region)
* Click **Review + Create → Create**

---

### 🌐 **Step 2: Create a Virtual Network**

1. Navigate to **Virtual Networks → + Create**
2. Fill in:

   * **Resource Group:** `rg-vpnlab`
   * **Name:** `lab-vnet`
   * **Region:** East US
3. Under **IP Addresses tab:**

   * Address space: `10.1.0.0/16`
4. Under **Subnets tab:**

   * Add subnet → Name: `app-subnet` → Prefix: `10.1.0.0/24`
   * Add subnet → Name: **`GatewaySubnet`** → Prefix: `10.1.255.0/27`
5. Click **Review + Create → Create**

---

### 🚀 **Step 3: Create a VPN Gateway**

1. Go to **Create a resource → Networking → Virtual Network Gateway**
2. Fill details:

   * **Name:** `lab-vnet-gateway`
   * **Region:** East US
   * **Gateway type:** VPN
   * **VPN type:** Route-based
   * **SKU:** VpnGw1 (lowest cost for lab)
   * **Virtual network:** `lab-vnet`
   * **Public IP address:** +Create new → name `lab-gw-pip`
   * **Enable BGP:** No
3. Click **Review + Create → Create**

   * ⏳ Wait 20–30 minutes for provisioning.

---

### 🏠 **Step 4: Create a Local Network Gateway**

1. Search **Local Network Gateway → + Create**
2. Enter:

   * **Name:** `onprem-localgw`
   * **Region:** East US
   * **IP address:** `<Public IP of On-Prem Emulator>`
   * **Address space:** `10.99.0.0/24`
   * **Resource Group:** `rg-vpnlab`
3. Click **Review + Create → Create**

---

### 🔗 **Step 5: Create the VPN Connection**

1. Go to **Virtual Network Gateway → Connections → + Add**
2. Enter:

   * **Name:** `site2site-conn`
   * **Connection type:** Site-to-site (IPSec)
   * **Local network gateway:** `onprem-localgw`
   * **Shared key (PSK):** `MyVeryStrongPSK123!`
3. Click **OK / Create**
4. Wait until connection appears under *Connections* list.

---

### 🧰 **Step 6: Configure the On-Prem Emulator**

#### Option A — Another Azure VM (Recommended)

1. Create Ubuntu VM (with Public IP).
2. Enable IP forwarding:

   * Go to **Networking → Network Interface → IP Configurations → Enable IP forwarding** ✅
3. SSH into the VM:

   ```bash
   sudo apt update && sudo apt install -y strongswan
   sudo sysctl -w net.ipv4.ip_forward=1
   ```
4. Edit `/etc/ipsec.conf`:

   ```text
   config setup
     charondebug="ike 2, knl 2, cfg 2"

   conn azure
     keyexchange=ikev2
     ike=aes256-sha1-modp1024!
     esp=aes256-sha1-modp2048!
     left=%defaultroute
     leftsubnet=10.99.0.0/24
     right=<Azure VPN Gateway Public IP>
     rightsubnet=10.1.0.0/16
     authby=secret
     auto=start
   ```
5. Edit `/etc/ipsec.secrets`:

   ```text
   : PSK "MyVeryStrongPSK123!"
   ```
6. Restart strongSwan:

   ```bash
   sudo systemctl restart strongswan
   sudo ipsec statusall
   ```

#### Option B — Local VM (Home/Office)

* Port forward UDP **500** and **4500** to your VM.
* Allow ESP protocol on firewall.
* Use the same strongSwan config.

---

### 🔍 **Step 7: Verify Connection**

1. Go to **Virtual Network Gateway → Connections → site2site-conn**.
2. Status should show ✅ **Connected**.
3. Test connectivity:

   ```bash
   ping 10.1.0.4   # example VM IP in app-subnet
   ```
4. (Optional) Deploy a test VM inside Azure AppSubnet and ping it from emulator VM.

---

### 🧹 **Step 8: Cleanup**

To avoid charges:

```
Azure Portal → Resource Groups → rg-vpnlab → Delete
```

---

## 🏁 **Outcome**

✅ You successfully built a **Hybrid Network** using Azure VPN Gateway GUI.
You now understand:

* Azure VNet, GatewaySubnet, and VPN Gateway creation.
* Local Network Gateway and shared-key S2S setup.
* How to emulate on-prem connections securely.

---

## 💡 Next Steps

* Enable **BGP** for dynamic routing.
* Connect multiple spoke VNets through Hub VPN.
* Add **Private Endpoints** and test hybrid access.
* Automate this setup using Azure CLI or Terraform.

---

🧱 *Author: BinnBash Academy | Azure Hybrid Networking Lab (Portal Edition)*
