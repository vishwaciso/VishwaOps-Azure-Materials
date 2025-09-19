# 🔐 Azure / Microsoft Entra — Add a Custom Domain & Use it for User UPNs (Step-by-step)

This README shows how to add and verify a custom domain in **Microsoft Entra ID (Azure AD)** and then how to **use that verified domain when creating users** (Portal, PowerShell, Azure CLI). It includes automation examples (Graph PowerShell), verification checks, and troubleshooting tips.

> **Quick summary:**  
> 1. Add the domain in the Entra admin center (or via Microsoft Graph).  
> 2. Azure gives you a TXT (or MX) record to publish at your DNS registrar — add it exactly.  
> 3. Verify the domain in Entra. After verification you can use the domain for user UPNs. :contentReference[oaicite:0]{index=0}

---

## Prerequisites
- You must be a **Global Administrator** or **Domain Name Administrator** in the tenant. :contentReference[oaicite:1]{index=1}  
- Access to the domain registrar (ability to add TXT or MX DNS records).  
- Optional for automation: **Microsoft Graph PowerShell** module installed, or ability to call Microsoft Graph REST.

---

# 1) Portal method (recommended for first-time / one-off)
1. Sign in to the **Microsoft Entra admin center**: `https://entra.microsoft.com`. :contentReference[oaicite:2]{index=2}  
2. Navigate: **Entra ID (Azure AD)** → **Domain names** (or *Custom domain names*) → **Add custom domain**.  
3. Enter your domain (e.g. `yourcompany.com`) and click **Add domain**. Entra will add the domain as *unverified* and show the DNS record(s) you must create. **Save/copy** the DNS details shown. :contentReference[oaicite:3]{index=3}  
4. At **your DNS registrar** (GoDaddy, Cloudflare, Azure DNS, etc.) create the **TXT** (or MX) record exactly as shown in the portal. Recommended TTL = **3600 seconds** (60 minutes). :contentReference[oaicite:4]{index=4}  
   - Example (generic):  
     - **Type:** TXT  
     - **Name / Host:** (use the name Azure shows — often blank / `@` or a special label)  
     - **Value:** the long verification string from Entra (copy/paste)  
     - **TTL:** 3600  
5. Back in Entra portal → select the domain → click **Verify**. If DNS propagated and the record exactly matches, the domain will become **Verified**. Propagation might take minutes to hours (sometimes longer depending on registrar). :contentReference[oaicite:5]{index=5}

---

# 2) Programmatic / PowerShell method (Microsoft Graph PowerShell)
Use this when automating or provisioning many tenants.

### Install & connect
```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
# interactive login (consent to Domain.ReadWrite.All when prompted)
Connect-MgGraph -Scopes "Domain.ReadWrite.All","Directory.ReadWrite.All"
