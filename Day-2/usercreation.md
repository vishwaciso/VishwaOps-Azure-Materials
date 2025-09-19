# Azure — Create Multiple Users (Step-by-step)

This README explains how to create multiple users in **Microsoft Entra ID (Azure AD)** after signing in to your Azure account.  
It includes three methods:
- **Portal (Bulk create CSV)** — easiest for admins who prefer GUI  
- **PowerShell (Microsoft Graph)** — recommended for robust automation & licensing  
- **Azure CLI** — simple scripting from shell

> **Prerequisites**
> - You must be signed in as at least a **User Administrator** (or Global Admin) in the tenant. :contentReference[oaicite:0]{index=0}  
> - Tools (choose what you need):
>   - Azure Portal (Microsoft Entra admin center) — no install needed. :contentReference[oaicite:1]{index=1}  
>   - Azure CLI (`az`) — install from Microsoft docs. :contentReference[oaicite:2]{index=2}  
>   - Microsoft Graph PowerShell (`Microsoft.Graph`) — install via PowerShell gallery. :contentReference[oaicite:3]{index=3}

---

## Option A — Portal: Bulk create (CSV) — Quick GUI method

1. Sign in to the Microsoft Entra admin center: `https://entra.microsoft.com` (or Azure portal → Entra ID / Users). :contentReference[oaicite:4]{index=4}  
2. Go to **Entra ID (Azure AD)** → **Users** → **Bulk create**.  
3. Click **Download** to get the official CSV template. **Do not remove the first two rows** (version & headers) — the portal requires them. :contentReference[oaicite:5]{index=5}  
4. Edit the downloaded CSV:
   - Required fields (minimum): **Name (displayName)**, **User principal name (userPrincipalName)**, **Initial password**, **Block sign in (Yes/No)**.  
   - Fill one row per user (replace example row).
5. Upload the CSV back in **Bulk create** and submit. Portal will validate your file; fix errors if shown and re-submit. After completion, check **Bulk operation results** for details. :contentReference[oaicite:6]{index=6}

### Example (CSV tips)
- Use the template from Microsoft (keeps first two rows intact).  
- Example content (note: real template uses more exact header formatting — always download the template first):

```csv
# (downloaded template contains a version row and header row)
Name [displayName] Required,User principal name [userPrincipalName] Required,Initial password [passwordProfile] Required,Block sign in [accountEnabled] Required
"John Doe","john.doe@contoso.onmicrosoft.com","P@ssw0rd!","No"
"Jane Smith","jane.smith@contoso.onmicrosoft.com","P@ssw0rd!","No"
