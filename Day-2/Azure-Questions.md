# ❓ Azure Tenant, Management Groups, Subscriptions & Resource Groups – Real-Time Questions  

This file contains **40 scenario-based interview/practical questions** related to Azure **Tenant, Management Groups (MG), Subscriptions, and Resource Groups (RG)**.  

---

## 🔹 Tenant & Identity  
1. Your company has 3 different Azure Tenants for HR, Finance, and IT. How would you decide whether to consolidate them or keep them separate?  
2. A user in your Tenant needs access to another company’s Azure subscription. How can cross-tenant access be configured?  
3. If an employee leaves the company, what happens to resources created under their account in the Tenant?  
4. Can one Azure Tenant have multiple domains? If yes, how would you configure and use them in user management?  
5. Your security team wants centralized identity across multiple Tenants. Which Azure features would you use?  
6. In a multi-tenant SaaS application, how do you isolate customer data and subscriptions under one Azure Tenant?  
7. What’s the difference between Azure Tenant vs Subscription, and when would you need multiple tenants instead of multiple subscriptions?  
8. How would you set up MFA (Multi-Factor Authentication) at the Tenant level for all subscriptions?  
9. A consulting firm has multiple clients with different Tenants. How would you manage your consultants’ access across those tenants?  
10. How do you restrict guest users from accessing resources outside their assigned subscription within your Tenant?  

---

## 🔹 Management Groups (MG)  
11. Your company has 5 subscriptions. How would you use Management Groups to apply a consistent security policy?  
12. How do you enforce that all new subscriptions created in your organization inherit tagging policies automatically?  
13. A compliance officer wants to audit security settings across 10 subscriptions. How can MG help in centralizing this?  
14. Can a single subscription be part of two Management Groups at the same time? Why or why not?  
15. You need to apply a policy that blocks the creation of public IPs across all subscriptions. At what MG level would you apply this policy?  
16. How would you structure Management Groups for a multinational company with regions: Americas, EMEA, and APAC?  
17. Your company uses both production and non-production subscriptions. How would you structure Management Groups for this use case?  
18. Can RBAC roles be assigned at a Management Group level? If yes, what’s a real-world example?  
19. A developer team wants to test a new Azure service in a sandbox subscription. How can MG help ensure this doesn’t violate compliance rules?  
20. If you delete a Management Group, what happens to the subscriptions under it?  

---

## 🔹 Subscriptions  
21. What is the main reason a company might use multiple Azure subscriptions instead of one large subscription?  
22. Can a subscription exist without being associated with a Tenant? Why or why not?  
23. A finance team wants to track costs separately for HR, IT, and R&D. How would you design subscriptions to meet this requirement?  
24. What’s the maximum number of subscriptions you can have in a Tenant, and what real-world challenge does this solve?  
25. Can you move resources from one subscription to another? If yes, what are the limitations?  
26. A project team’s subscription is nearing its quota limits. What steps would you take to fix this?  
27. If a subscription is disabled due to non-payment, what happens to the resources inside it?  
28. How do you consolidate billing across multiple subscriptions for a single organization?  
29. A customer needs isolation of workloads for compliance reasons but doesn’t want multiple Tenants. Would you use subscriptions or RGs? Why?  
30. Can you assign different Azure AD tenants to the same subscription over time? What are the risks?  

---

## 🔹 Resource Groups (RG)  
31. Can one resource in Azure exist in multiple Resource Groups? Why or why not?  
32. What happens if you delete a Resource Group that contains multiple resources?  
33. A project team asks if they can move a VM from one RG to another. What’s your answer and why?  
34. If two teams share the same subscription, how would you use RGs to separate their workloads?  
35. How do RBAC role assignments differ when applied at the RG level vs subscription level?  
36. Can an RG contain resources from multiple regions? If yes, what are the risks?  
37. How would you organize RGs for a project lifecycle: Dev, Test, Staging, and Prod?  
38. What’s the best way to apply cost tracking for different applications inside the same subscription using RGs?  
39. If an RG is deleted accidentally, how can you recover it?  
40. A team wants to group resources by application instead of environment. How would you design RGs for this case?  

---

📌 These questions are designed for **real-world interview & project discussions** to test knowledge of **Tenant, Management Groups, Subscriptions, and Resource Groups in Azure**.  

