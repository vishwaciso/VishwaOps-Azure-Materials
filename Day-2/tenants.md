# ☁️ Azure Tenants — Complete Deep Dive

> **Updated:** September 2025  
> Author: Vishwanath  

This guide explains **all types of Azure Tenants** from scratch, with **real-time examples**, **use cases**, and a **visual diagram** for workshops.

---

## 🌍 What is a Tenant?

A **Tenant** in Azure = a **dedicated instance of Microsoft Entra ID (formerly Azure AD)**.  
It represents an **organization or identity boundary**.  

👉 Think of a Tenant as a **container for users, apps, and policies**.

---

## 🏷️ Types of Tenants in Azure

### 🔹 1. Default Tenant
- **Definition:** Created automatically when you sign up for Azure with an email (Gmail, Outlook, etc.).
- **Use Case:** Learning, testing, or free trial subscriptions.
- **Outcome:** Basic playground.  
- **Example:** Vishwanath signs up with Gmail → gets `vishwatenant.onmicrosoft.com`.

---

### 🔹 2. Organizational Tenant
- **Definition:** Tied to a company’s custom domain (like `abc.com`).
- **Use Case:** Corporate identity and governance.
- **Outcome:** Central place for employees and apps.  
- **Example:** ABC Corp creates `abc.com` tenant → employees log in as `user@abc.com`.

---

### 🔹 3. Personal Tenant
- **Definition:** Created when individuals use personal emails.
- **Use Case:** Dev/test, hobby projects.
- **Outcome:** Sandbox for individuals.  
- **Example:** Vishwanath uses `vishwa@gmail.com` to create a VM.

---

### 🔹 4. Single-Tenant Application Tenant
- **Definition:** App registered in Entra ID **restricted to one tenant**.
- **Use Case:** Internal apps for employees only.
- **Outcome:** Secure enterprise-only apps.  
- **Example:** ABC Payroll app → only `abc.com` users can log in.

---

### 🔹 5. Multi-Tenant Application Tenant
- **Definition:** App accessible by users from **multiple tenants**.
- **Use Case:** SaaS providers serving multiple organizations.
- **Outcome:** Shared SaaS apps.  
- **Example:** Healthcare SaaS app → Hospitals A, B, C log in with their tenants.

---

### 🔹 6. B2B (Business-to-Business) Tenant
- **Definition:** Invite **external users (partners, vendors)** into your tenant as guests.
- **Use Case:** External collaboration without giving full control.
- **Outcome:** Controlled external access.  
- **Example:** ABC invites `user@xyz.com` to access `ABC-Dev-RG`.

---

### 🔹 7. B2C (Business-to-Consumer) Tenant
- **Definition:** Special tenant for **customer-facing apps**.
- **Use Case:** Customers log in with Google, Facebook, etc.
- **Outcome:** Secure, scalable identity for apps.  
- **Example:** ABC Patient Portal lets patients log in with Gmail.

---

### 🔹 8. Lighthouse (Cross-Tenant Management)
- **Definition:** Lets service providers or central IT manage multiple tenants from one control plane.
- **Use Case:** Cross-tenant visibility and governance.
- **Outcome:** Simplified multi-tenant management.  
- **Example:** ABC IT manages **ABC India Tenant + ABC US Tenant** from one Lighthouse tenant.

---

## 📊 Summary Table

| Tenant Type              | Who Uses It               | Purpose                        | Example |
|---------------------------|---------------------------|--------------------------------|---------|
| Default Tenant            | Individuals               | Sandbox, free trial            | Vishwanath’s trial tenant |
| Organizational Tenant     | Enterprises               | Corporate governance           | ABC Corp `abc.com` |
| Personal Tenant           | Individuals               | Hobby/dev projects             | Vishwanath with Gmail |
| Single-Tenant Application | Enterprises               | Internal apps only             | ABC Payroll app |
| Multi-Tenant Application  | SaaS Providers            | Apps across orgs               | Healthcare SaaS app |
| B2B Tenant                | Enterprises + Partners    | Guest access                   | Invite vendor |
| B2C Tenant                | Enterprises + Consumers   | Customer login                 | Patient Portal |
| Lighthouse                | MSPs, Central IT          | Manage multiple tenants        | ABC IT managing clients |

---

## 🎯 Hands-On Training Flow

1. Create a **Default Tenant** (using Gmail).  
2. Set up **Organizational Tenant** (with `abc.com`).  
3. Register a **Single-Tenant App**.  
4. Register a **Multi-Tenant App**.  
5. Enable **B2B Guest Access**.  
6. Enable **B2C Consumer Login**.  
7. Configure **Lighthouse for Cross-Tenant Management**.  

---

## 🗺️ Visual Diagram (Mermaid)

```mermaid
flowchart TD

    subgraph AzureTenants["Azure Tenant Types"]
        A1[Default Tenant] --> A2[Personal Tenant]
        A1 --> A3[Organizational Tenant]
    end

    subgraph Applications["Applications"]
        B1[Single-Tenant App]
        B2[Multi-Tenant App]
    end

    subgraph Collaboration["External Collaboration"]
        C1[B2B Tenant]
        C2[B2C Tenant]
    end

    subgraph Management["Cross-Tenant Management"]
        D1[Azure Lighthouse]
    end

    A3 --> B1
    A3 --> B2
    A3 --> C1
    A3 --> C2
    A3 --> D1

    A2 --> B1
    A2 --> B2
    A2 --> C2
