---

# 📡 DNS Records in Domain Verification – MX vs TXT

When adding a **custom domain** to Microsoft Entra ID (Azure AD), Azure asks you to add a **DNS record** at your domain registrar.  
Two common types are **TXT** and **MX**. Both serve different primary purposes but can be used for verification.

---

## 🔹 TXT Record
- **Purpose:** General-purpose text record in DNS.  
- **Common Uses:**
  - Domain ownership verification (Azure AD, Google, AWS, etc.)
  - SPF (Sender Policy Framework) → helps prevent email spoofing
  - DKIM / DMARC email authentication
- **Example (Azure verification TXT):**


Type: TXT
Name/Host: @
Value: MS=ms12345678
TTL: 3600


- **How Azure uses it:**  
- Azure checks the TXT record value at your DNS.  
- If the string matches what Azure provided, ownership is proven.  
- **Note:** TXT is the most common method Azure recommends.

---

## 🔹 MX Record
- **Purpose:** Mail Exchanger record → routes email for your domain.  
- **Common Uses:**
- Tells the internet which mail server handles emails for your domain.
- **Example (Azure verification MX):**

Type: MX
Name/Host: @
Value: ms12345678.msv1.invalid
Priority: 0
TTL: 3600


- **How Azure uses it:**  
- Sometimes Azure offers MX instead of TXT for domain verification.  
- The MX record is **not used for real mail routing**, only for verification in this case.  
- It will not affect your mail flow if configured exactly as shown.

---

## 📊 Side-by-Side Comparison

| Feature | TXT Record | MX Record |
|---------|------------|-----------|
| **Primary Purpose** | Stores text info in DNS (flexible usage) | Directs email traffic to mail servers |
| **Common Uses** | Ownership verification, SPF, DKIM, DMARC, general metadata | Email delivery (e.g., Gmail, Exchange Online) |
| **Used in Azure Verification?** | ✅ Yes (most common) | ✅ Yes (alternative) |
| **Impact on Email** | None (harmless text entry) | If misconfigured, could disrupt email delivery (only safe when using Azure-provided `msv1.invalid` target) |
| **Preferred for Verification** | ✅ TXT (simple & safe) | ⚠️ MX (works but less common) |

---

## 🔐 Real-World Guidance
- Always prefer **TXT** for Azure custom domain verification.  
- Use **MX** only if TXT is not possible with your DNS provider.  
- For production mail domains:  
- Ensure **real MX records** (for mail delivery) are still present.  
- The Azure verification MX record points to `*.msv1.invalid` which **does not route email** — so it’s safe alongside your real MX records.

---



