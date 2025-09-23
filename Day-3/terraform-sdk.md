# Terraform Azure Resource Group Creation

This repository demonstrates how to create an **Azure Resource Group** using **Terraform**.
It includes prerequisites, Terraform setup, files structure, and step-by-step commands to deploy resources.

---

## Prerequisites

Before starting, ensure you have the following:

1. **Azure Account** – with a valid subscription.
2. **Terraform Installed** – Check version:

```bash
terraform -version
```

3. **Azure CLI Installed** – Optional but recommended:

```bash
az --version
```

4. **Azure Login** – You can use interactive login or Service Principal:

**Interactive Login:**

```bash
az login
```

**Service Principal (for automation):**

```bash
az ad sp create-for-rbac --name "terraform-sp" --role="Contributor" --scopes="/subscriptions/<SUBSCRIPTION_ID>"
```

You will get the following credentials:

* `appId` → Client ID
* `password` → Client Secret
* `tenant` → Tenant ID
* `subscriptionId` → Subscription ID

---

## Terraform Files Structure

```
terraform-rg/
├── main.tf
├── variables.tf
└── provider.tf
```

---

### 1. provider.tf

```hcl
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 3.0"
    }
  }
  required_version = ">= 1.5.0"
}

provider "azurerm" {
  features {}

  # Optional if using Service Principal
  subscription_id = "<YOUR_SUBSCRIPTION_ID>"
  client_id       = "<YOUR_CLIENT_ID>"
  client_secret   = "<YOUR_CLIENT_SECRET>"
  tenant_id       = "<YOUR_TENANT_ID>"
}
```

---

### 2. variables.tf

```hcl
variable "rg_name" {
  description = "Name of the resource group"
  default     = "myResourceGroup"
}

variable "location" {
  description = "Azure region"
  default     = "East US"
}
```

---

### 3. main.tf

```hcl
resource "azurerm_resource_group" "example" {
  name     = var.rg_name
  location = var.location
}
```

---

## Terraform Commands

1. **Initialize Terraform**

```bash
terraform init
```

2. **Preview changes**

```bash
terraform plan
```

3. **Apply to create Resource Group**

```bash
terraform apply
```

Type `yes` when prompted.

4. **Verify in Azure CLI**

```bash
az group show --name myResourceGroup
```

---

## Notes

* Use `az login` for local interactive authentication.
* For automated deployments (CI/CD), use **Service Principal** credentials in `provider.tf`.
* Terraform state is stored locally by default (`terraform.tfstate`). Use **remote backend** for team collaboration.

---

## Optional Enhancements

* Create multiple resource groups dynamically using `for_each` or `count`.
* Integrate with CI/CD pipelines to automate deployments.
* Use `terraform fmt` to format code and `terraform validate` to validate configurations.

---

> This setup is ready to use and can be directly applied in your Azure subscription.
