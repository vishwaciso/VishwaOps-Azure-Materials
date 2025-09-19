📂 Azure RBAC – Subscription, Resource Group & Resource Scope

This guide explains how RBAC (Role-Based Access Control) works across Subscriptions, Resource Groups (RGs), and Resources, and how to assign a user (e.g., Mukesh) to specific scopes.

🔑 RBAC Hierarchy in Azure

RBAC roles in Azure are hierarchical:

Management Group
   └── Subscription
         └── Resource Group (RG)
               └── Resource (VM, Storage, SQL, etc.)


✅ If a role is assigned at a higher scope (e.g., Subscription), it is inherited by all lower levels (RGs, resources).

✅ If a role is assigned at a lower scope (e.g., RG), it applies only there and does not affect others.

🎯 Example – Assign Mukesh to Only Two RGs

Instead of giving Mukesh access to the entire subscription, you can assign him only to specific RGs.

Step 1: Open the Subscription

Go to Azure Portal
.

Navigate to Subscriptions → Select your subscription.

Step 2: Navigate to Resource Groups

Inside the subscription → Resource groups.

Select the RG (e.g., Dev-RG).

Go to Access control (IAM) → Add role assignment.

Choose a role (e.g., Contributor) → Assign to Mukesh.

Step 3: Repeat for Second RG

Go to another RG (e.g., Test-RG) → Assign Reader role to Mukesh.

✅ Now Mukesh only sees Dev-RG (Contributor) and Test-RG (Reader).

🔗 Can One RG Belong to Multiple Subscriptions?

❌ No.

A Resource Group belongs to only one Subscription.

You cannot attach a single RG to multiple subscriptions.

👉 But:

You can assign Mukesh access to multiple RGs across different subscriptions.

⚡ Real-Time Example Scenarios
Scope	Example	Mukesh’s Role
Subscription	Entire Prod Subscription	Contributor (access to all RGs & resources)
Resource Group	Dev-RG only	Contributor
Another RG	Test-RG only	Reader
Resource	One VM inside Prod-RG	Virtual Machine Contributor
🖼️ Visual Diagram
Subscription-A
 ├── RG1 (Dev-RG) → Mukesh = Contributor
 ├── RG2 (Test-RG) → Mukesh = Reader
 └── RG3 (Finance-RG) → No Access

Subscription-B
 ├── RG1 (Storage-RG) → Mukesh = Contributor
 └── RG2 (App-RG) → No Access


➡️ Mukesh only sees RGs where roles are assigned, not the entire subscription.
