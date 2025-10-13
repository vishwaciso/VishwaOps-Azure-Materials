🧠 Assessment Plan — Azure Networking Module
🗂️ 1. Assessment Format
Type	Purpose	Example Count
Theory (MCQs + Short answers)	Check conceptual understanding	10–12 Questions
Scenario-based Questions	Check problem-solving & design thinking	3–5 Questions
Lab Tasks (Hands-On)	Check practical Azure skills	3–5 Tasks
💡 Section 1: Theory / MCQ Questions (Basic Understanding)

What is the purpose of a Virtual Network (VNet) in Azure?
a) Provide compute resources
b) Provide isolated network environment
c) Store data
d) Manage subscriptions

Which component divides a VNet into smaller logical segments?
a) Peering
b) Subnets
c) NSG
d) Route Table

What is the default direction for NSG rules if not specified?
a) Inbound
b) Outbound
c) Both
d) None

You can connect two VNets using ________.
a) Peering
b) Load balancer
c) Application Gateway
d) Azure Policy

Which Azure tool helps diagnose and monitor network traffic?
a) Azure Advisor
b) Network Watcher
c) Monitor Logs
d) Sentinel

What is the difference between Private Endpoint and Service Endpoint? (Short Answer)

What happens if you apply an NSG rule with deny RDP (3389) on a subnet where a VM is hosted?

Why is Hub-Spoke architecture preferred in enterprise environments?

In Azure, how can you restrict a Storage Account to accept only internal VNet traffic?

Define VNet Peering and mention one real-time use case.

🧩 Section 2: Scenario-Based Questions (Intermediate Level)

You have 2 VNets in different regions — Prod-VNet and Dev-VNet. You want secure communication between them without using the internet.
👉 What Azure feature will you use and why?

Your application has a Web tier and a Database tier. You want only the Web tier to communicate with the DB tier, and block everything else.
👉 Which Azure networking features will you configure?

A company wants to connect its on-premises data center to Azure securely.
👉 Which service would you use and what are the key components?

You have multiple Spoke VNets (Finance, HR, IT) that need to share security policies and internet access via a central firewall.
👉 How will you design the architecture?

You want to allow only HTTP (port 80) traffic and deny SSH (port 22) on your Linux VM.
👉 How can this be done using NSG rules?

🧑‍💻 Section 3: Hands-On / Lab Assessment Tasks
🧩 Basic Level

VNet + Subnets Creation

Create a VNet named CorpVNet with two subnets: WebSubnet and DBSubnet.

Deploy one VM in each subnet.

Ping between them and show subnet-level isolation.

NSG Rule Control

Create an NSG for WebSubnet.

Deny inbound RDP (3389) and test remote connection → it should fail.

Modify NSG to allow RDP → it should succeed.

⚙️ Intermediate Level

VNet Peering

Create VNetA and VNetB.

Peer them and ensure VMs in both VNets can communicate using private IPs.

VPN Gateway Hybrid

Create a VPN Gateway and connect to a local VM acting as an on-prem network.

Verify hybrid connectivity.

Priority Rules

Create NSG rules where HTTP is allowed and SSH is denied.

Test both using a browser and SSH client.

🏗️ Advanced Level

Hub-Spoke Architecture

Create a Hub VNet with Azure Firewall or NVA.

Connect 2 Spoke VNets via peering.

Route traffic through the Hub for inspection.

Private Endpoint

Create an Azure Storage Account and add a Private Endpoint.

Try accessing it via public IP → it should fail.

Service Endpoint

Create Azure SQL and configure a Service Endpoint from your VNet.

Ensure only that VNet can access the DB.
