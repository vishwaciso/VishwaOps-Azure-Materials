# Cloud Introduction

> Foundations you need before diving into AWS.

---

## 🌩️ What is Cloud?
Cloud computing is the **delivery of IT resources (compute, storage, networking, databases, analytics, etc.) over the internet** with **pay-as-you-go pricing**.

## 🌩️ Cloud is a collection of domains !!

### Why?
- No need to buy and maintain expensive hardware.
- Scale up/down based on demand.
- Focus on business, not infrastructure.

### When?
- Startups → Launch quickly without upfront capital.
- Enterprises → Modernize applications, reduce costs, innovate faster.
- Students/learners → Practice on-demand, temporary resources.

### Where?
- Global cloud providers like **AWS, Azure, GCP**, with multiple regions across the world.

### Example:
- Netflix → Runs its video streaming on AWS to serve millions of users globally.
- A student → Spins up an EC2 instance for a Python project and deletes it when done.

**Outcome:** Flexible, scalable, cost-efficient infrastructure available instantly.

---

## 🏗️ Cloud Service Models
Cloud services are offered in multiple layers:

### 1. Infrastructure as a Service (IaaS)
- Raw compute, storage, networking resources.
- You manage OS, applications, data.
- **Example:** AWS EC2, Google Compute Engine, Azure VM.  
**Use Case:** Hosting custom applications, experimenting with OS-level control.  
**Outcome:** Maximum flexibility, but more responsibility.

### 2. Platform as a Service (PaaS)
- Pre-built environment for app development.
- Provider manages OS, runtime, scaling.
- **Example:** AWS Elastic Beanstalk, Google App Engine.  
**Use Case:** Developers who just want to push code without managing infra.  
**Outcome:** Faster development cycles.

### 3. Software as a Service (SaaS)
- Fully managed apps accessible over internet.
- You just use the software.
- **Example:** Gmail, Zoom, Salesforce.  
**Use Case:** Businesses wanting ready-to-use software.  
**Outcome:** No infra headaches, pay per user or subscription.

### 4. Container as a Service (CaaS)
- Container management & orchestration provided as a service.
- Provider manages container runtime, orchestration (Kubernetes, Docker Swarm).
- **Example:** AWS EKS, Google Kubernetes Engine (GKE), Azure AKS.  
**Use Case:** Microservices-based applications, containerized workloads.  
**Outcome:** Simplified container deployment, scaling, and management.

### 5. Function / Serverless as a Service (FaaS)
- Serverless execution model: just upload code, runs on demand.
- No server management, fully event-driven.
- **Example:** AWS Lambda, Azure Functions, Google Cloud Functions.  
**Use Case:** Event-driven apps, APIs, scheduled jobs.  
**Outcome:** Pay only per execution, no infra management.

### 6. Network as a Service (NaaS)
- Provides networking services like VPN, bandwidth, firewalls, load balancing.
- Delivered via subscription or pay-per-use.
- **Example:** AWS VPC, Cloudflare, Akamai.  
**Use Case:** Secure connectivity, CDN, network isolation.  
**Outcome:** Simplifies networking without owning hardware.

---

## 🌍 Deployment Models
Different ways cloud can be deployed:

- **Public Cloud** → Services offered to anyone over internet.  
  *Example: AWS, Azure, GCP.*  
  ✅ Scalable, cost-effective.  
  ❌ Less control.  

- **Private Cloud** → Dedicated cloud infra for one organization.  
  *Example: VMware vSphere on-premises.*  
  ✅ High security, control.  
  ❌ Expensive.  

- **Hybrid Cloud** → Mix of public + private.  
  *Example: Sensitive workloads on private, scale-out workloads on AWS.*  
  ✅ Balance of cost & control.  

- **Multi-Cloud** → Using multiple providers.  
  *Example: AWS for storage, Azure for AI services.*  
  ✅ Avoid vendor lock-in.  
  ❌ Complexity in management.  

- **Community Cloud** → Shared infrastructure for organizations with common needs (e.g., government, healthcare, education).  
  *Example: Government agencies in the EU sharing a compliance-focused cloud.*  
  ✅ Cost shared, compliance maintained.  
  ❌ Limited to community scope.  

---

## 🔐 Shared Responsibility Model
Cloud security is **shared** between **provider** and **customer**:

- **Provider (AWS, Azure, GCP)** → Responsible for security **of** the cloud  
  (Data center, hardware, global network, physical security).

- **Customer (You)** → Responsible for security **in** the cloud  
  (Configuring IAM, managing OS patches, encrypting data, securing apps).

**Example:**  
- AWS secures EC2 infrastructure.  
- You must configure your EC2 instance firewall (Security Groups).  

**Outcome:** Secure workloads when both parties play their role.

---

## ⚖️ Benefits & Trade-offs
**Benefits:**
- Elasticity → Scale up/down instantly.  
- Agility → Deploy apps globally in minutes.  
- Cost savings → Pay only for usage.  
- Reliability → Multi-AZ and global backups.  

**Trade-offs:**
- Less visibility compared to on-prem infra.  
- Vendor lock-in if using only one provider.  
- Learning curve for teams.

---


