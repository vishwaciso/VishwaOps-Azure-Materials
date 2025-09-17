# 🔐 Shared Responsibility Model (Extended for All Cloud Services)

Cloud is powerful ⚡ but **security is never 100% handled by the provider**.  
The **Shared Responsibility Model (SRM)** explains **who secures what**.

---

## 📌 What is Shared Responsibility?
- **Provider (AWS, Azure, GCP, etc.):** Secures the **underlying cloud infrastructure**.  
- **Customer (You):** Secures **your data, access, and configs**.  

👉 Without this separation → **security gaps → breaches**.  

---

## 🌩️ Service Models & Responsibilities  

Here’s the **full spectrum**:  

| Model | Provider Secures (✅ of the Cloud) | Customer Secures (✅ in the Cloud) | When to Use | Where It Fits | How to Secure | Outcome | Expected Output |
|-------|-----------------------------------|------------------------------------|-------------|---------------|---------------|---------|-----------------|
| **IaaS** (Infrastructure as a Service) | Physical infra, network, hypervisor | OS, patches, apps, data, IAM | When you need flexibility to manage infra | EC2, Azure VM, GCP Compute Engine | Patch OS, configure firewalls, encrypt disks | Flexible + scalable infra | VM that is secure, patched, and app-ready |
| **PaaS** (Platform as a Service) | Runtime, middleware, infra | App code, data, IAM, configs | When devs want to focus on apps, not infra | AWS Elastic Beanstalk, Azure App Service | Secure APIs, rotate keys, encrypt DB | Faster app delivery | Working secure app without managing servers |
| **SaaS** (Software as a Service) | Whole app stack (infra + app) | User access, data governance | When you need ready-to-use apps | Gmail, Office365, Salesforce | Strong passwords, MFA, DLP policies | Zero infra management | Business-ready app with secure data |
| **CaaS** (Containers as a Service) | Container orchestration (EKS, GKE), infra | Container images, app code, network policies | When running Docker/Kubernetes apps | AWS EKS, Azure AKS, GCP GKE | Secure Dockerfiles, scan images, apply RBAC | Portable, scalable microservices | Secured container workloads |
| **FaaS** (Functions as a Service / Serverless) | Runtime, scaling, infra | Function code, IAM, data | When event-driven or serverless workloads | AWS Lambda, Azure Functions | Write secure code, validate input, IAM roles | Pay-per-execution cost savings | Auto-scaling secure function execution |
| **NaaS** (Network as a Service) | Core network, backbone infra | Config, routing rules, access controls | When extending WAN, VPN, SD-WAN, 5G | AWS VPC Lattice, Cloudflare, Megaport | Secure routing, apply firewall rules, segment traffic | Global secure connectivity | Optimized, secure enterprise networking |

---

## 🎯 Why We Need This

- Providers **cannot secure your app/data** → privacy & compliance.  
- Customers **cannot secure physical infra** → provider’s domain.  
- Both must **work together** for full security coverage.  

👉 Example:  
- AWS secures EC2 infra.  
- You patch EC2 OS + configure Security Groups.  
- **Only then** → workload is secure.  

---

## 🛠️ Tools for Each Cloud Service Model

| Model | AWS Tools | Azure Tools | GCP Tools |
|-------|-----------|------------|-----------|
| **IaaS** | AWS Inspector, Systems Manager, Nessus | Azure Security Center, Azure Monitor, Azure Automation | Google Cloud Security Scanner, Cloud Monitoring, Forseti Security |
| **PaaS** | AWS Config, Secrets Manager | Azure Policy, Key Vault, App Insights | Cloud Deployment Manager, Secret Manager, Cloud Logging |
| **SaaS** | CASB, DLP, Okta, MFA tools | Microsoft Defender for Office 365, Conditional Access, Intune | Google Workspace Security Center, BeyondCorp, DLP API |
| **CaaS** | Twistlock (Prisma), Aqua Security, Falco | Azure Defender for Containers, Azure Policy, K8s Security Center | GKE Security Posture, Binary Authorization, Forseti Security |
| **FaaS** | AWS X-Ray, IAM, CloudWatch logs | Azure Monitor, Application Insights, Managed Identities | Cloud Functions IAM, Cloud Logging, Cloud Trace |
| **NaaS** | AWS Network Firewall, Cloudflare Zero Trust | Azure Firewall, Azure Front Door, Azure DDoS Protection | Cloud Armor, VPC Service Controls, Cloud CDN |
 

---

## 📊 Visual: Responsibility by Service Model

```mermaid
flowchart LR
    A[Provider] -->|Infra| I(IaaS)
    A -->|Runtime| P(PaaS)
    A -->|App| S(SaaS)
    A -->|Orchestration| C(CaaS)
    A -->|Runtime Events| F(FaaS)
    A -->|Core Network| N(NaaS)
    
    I -->|OS, Apps, Data| Customer
    P -->|App, Data| Customer
    S -->|User Access, Data| Customer
    C -->|Container Images, RBAC| Customer
    F -->|Function Code, Data| Customer
    N -->|Routing, Access Control| Customer
