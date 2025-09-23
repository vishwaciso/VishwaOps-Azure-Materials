# Azure CLI & PowerShell Commands Cheat Sheet

This guide provides commonly used **Azure CLI** and **Azure PowerShell** commands for corporate training.  
👉 In **Azure Cloud Shell**:  
- **Bash** → Only Azure CLI works  
- **PowerShell** → Both Azure CLI & PowerShell work  

---

## 🔹 Account, Tenant & Subscription

| Task | Azure CLI | Azure PowerShell |
|------|-----------|------------------|
| Login | `az login` | `Connect-AzAccount` |
| List tenants | `az account tenant list -o table` | `Get-AzTenant \| Format-Table Id, Domain, DisplayName` |
| List subscriptions | `az account list -o table` | `Get-AzSubscription \| Format-Table Name, Id, TenantId` |
| Set subscription | `az account set --subscription <SubID>` | `Set-AzContext -Subscription <SubID>` |
| Show current context | `az account show -o table` | `Get-AzContext` |

---

## 🔹 Resource Groups

| Task | Azure CLI | Azure PowerShell |
|------|-----------|------------------|
| Create resource group | `az group create --name MyRG --location eastus` | `New-AzResourceGroup -Name MyRG -Location eastus` |
| List resource groups | `az group list -o table` | `Get-AzResourceGroup \| Format-Table` |
| Delete resource group | `az group delete --name MyRG --yes --no-wait` | `Remove-AzResourceGroup -Name MyRG -Force` |

---

## 🔹 Virtual Machines (VMs)

| Task | Azure CLI | Azure PowerShell |
|------|-----------|------------------|
| Create VM | `az vm create --resource-group MyRG --name MyVM --image UbuntuLTS --admin-username azureuser --generate-ssh-keys` | `New-AzVM -ResourceGroupName MyRG -Name MyVM -ImageName UbuntuLTS -Location eastus` |
| List VMs | `az vm list -d -o table` | `Get-AzVM \| Format-Table Name, ResourceGroupName, Location` |
| Start VM | `az vm start --resource-group MyRG --name MyVM` | `Start-AzVM -ResourceGroupName MyRG -Name MyVM` |
| Stop VM | `az vm stop --resource-group MyRG --name MyVM` | `Stop-AzVM -ResourceGroupName MyRG -Name MyVM` |
| Delete VM | `az vm delete --resource-group MyRG --name MyVM --yes` | `Remove-AzVM -ResourceGroupName MyRG -Name MyVM -Force` |

---

## 🔹 Storage

| Task | Azure CLI | Azure PowerShell |
|------|-----------|------------------|
| Create storage account | `az storage account create --name mystorage123 --resource-group MyRG --location eastus --sku Standard_LRS` | `New-AzStorageAccount -ResourceGroupName MyRG -Name mystorage123 -Location eastus -SkuName Standard_LRS` |
| List storage accounts | `az storage account list -o table` | `Get-AzStorageAccount` |
| Show storage account keys | `az storage account keys list --account-name mystorage123 -o table` | `Get-AzStorageAccountKey -ResourceGroupName MyRG -Name mystorage123` |

---

## 🔹 Networking

| Task | Azure CLI | Azure PowerShell |
|------|-----------|------------------|
| List VNets | `az network vnet list -o table` | `Get-AzVirtualNetwork` |
| Create VNet | `az network vnet create --name MyVNet --resource-group MyRG --address-prefix 10.0.0.0/16 --subnet-name MySubnet --subnet-prefix 10.0.1.0/24` | `New-AzVirtualNetwork -Name MyVNet -ResourceGroupName MyRG -Location eastus -AddressPrefix 10.0.0.0/16 -Subnet @(New-AzVirtualNetworkSubnetConfig -Name MySubnet -AddressPrefix 10.0.1.0/24)` |
| List NSGs | `az network nsg list -o table` | `Get-AzNetworkSecurityGroup` |
| Create Public IP | `az network public-ip create --resource-group MyRG --name MyPublicIP` | `New-AzPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG -Location eastus -AllocationMethod Dynamic` |

---

## 🔹 RBAC (Roles & Access Control)

| Task | Azure CLI | Azure PowerShell |
|------|-----------|------------------|
| List role assignments | `az role assignment list -o table` | `Get-AzRoleAssignment` |
| Assign Reader role | `az role assignment create --assignee user@company.com --role Reader --scope /subscriptions/<SubID>` | `New-AzRoleAssignment -ObjectId <UserObjectId> -RoleDefinitionName Reader -Scope "/subscriptions/<SubID>"` |
| Assign Contributor role | `az role assignment create --assignee user@company.com --role Contributor --scope /subscriptions/<SubID>/resourceGroups/MyRG` | `New-AzRoleAssignment -ObjectId <UserObjectId> -RoleDefinitionName Contributor -Scope "/subscriptions/<SubID>/resourceGroups/MyRG"` |

---

## 🔹 Active Directory (AAD)

| Task | Azure CLI | Azure PowerShell |
|------|-----------|------------------|
| Show current user | `az ad signed-in-user show` | `Get-AzADUser -SignedIn` |
| Check if user is Member or Guest | `az ad signed-in-user show --query userType -o tsv` | `Get-AzADUser -ObjectId <UserObjectId> \| Select DisplayName, UserType` |
| List users | `az ad user list -o table` | `Get-AzADUser` |

---

## 🔹 Notes
- **CLI is cross-platform** (works in Bash, PowerShell, Linux, Mac, Windows).  
- **PowerShell is native for automation** if your org already uses PowerShell scripts.  
- Both tools manage the **same resources** — choose based on preference.  

---
