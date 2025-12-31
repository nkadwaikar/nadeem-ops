# 🚀 Cloud Engineering — Built With Precision (and the Occasional Coffee Spill ☕)

A growing collection of Azure labs, architectures, and Boot Camp notes — written to stay clean, practical, and easy to revisit.  
Built for the days when the cloud behaves, and the days when it needs a little extra coffee (or encouragement).

**This repository is for Azure administrators, cloud engineers, and AZ-104 candidates who want hands-on, production-style labs — not just exam notes.**

---

## 👋 About Me

I work with Azure services across identity, networking, compute, and security, and I enjoy turning complex cloud scenarios into clear, repeatable implementations — often fueled by strong coffee ☕.

The goal here is simple: documentation that’s lightweight, well-structured, and friendly enough that *future me* doesn’t have to reverse-engineer my own work — whether it’s a Monday morning or a late-night coffee session.

---

## 🎓 Azure Administrator Boot Camp (AZ-104 Track)

This repository tracks my full **Azure Administrator Boot Camp** — a structured, identity-first walkthrough of Azure’s core services.

Each week focuses on a major domain (Identity, Networking, Compute, Monitoring), and finishes with a **real-world capstone project deployed using Bicep**.

Every lab is designed to be:
- Clear  
- Repeatable  
- Practical in real environments  

All written with the same care I put into my coffee — precise, consistent, and energizing enough to keep learning fun.

---

## 🧪 How to Use This Repository

You can use this repo in two ways:

- **Follow the Boot Camp:** Start at Week 1 and progress sequentially  
- **Use it as a reference:** Jump directly to specific services or scenarios  

Each lab includes:
- Prerequisites  
- Step-by-step deployment  
- Validation and troubleshooting steps  
- Architecture context  
- Cleanup guidance where it makes sense  

> ☕ Pro tip: Keep a cup of coffee nearby — some labs are best enjoyed with caffeine and curiosity.

---

## 🧭 Full Multi-Week Roadmap (AZ-104 Aligned)

A high-level view of the Boot Camp structure:

---

### **Week 1 — Identity & Governance**  
[Identity, RBAC, Managed Identity](./Week1-Identity-Governance/README.md)  
- Entra ID fundamentals  
- Role-Based Access Control (RBAC)  
- Managed Identity patterns  

---

### **Week 2 — Networking & Security**  
- Virtual networks and subnets  
- Network security groups (NSGs)  
- Traffic flow and access control  

---

### **Week 3 — Compute, App Services & Storage**  
- Virtual machines  
- App Services  
- Azure Storage and static websites  

---

### **Week 4 — Monitoring, Backup & Governance**  
- Azure Monitor and Log Analytics  
- Alerts and diagnostics  
- Backup and recovery  

---

### 📦 What Each Week Includes

- ✅ 7 hands-on labs  
- 🏗️ One real-world capstone project  
- 📐 Architecture diagrams  
- 🔍 Validation steps  
- 📦 Full Bicep deployment  

> ☕ Optional: Coffee breaks between weeks are highly recommended for optimal learning.

---

## ✅ Completed Days
- **Day 1:** [RBAC, Managed Identity, Storage Access](./Week1-Identity-Governance/Day1-RBAC-Managed-Identity-Storage.md)
- **Day 2:** [Key Vault + Managed Identity](./Week1-Identity-Governance/Day2-KeyVault-Managed-Identity.md)
- **Day 3:** [Managed Identity → Storage Account (Blob Read Access)

This list grows as the Boot Camp progresses.  
> ☕ Some labs take longer — it’s okay to sip slowly and absorb the details.

---

## 📘 Featured Labs

### **Azure Front Door — Routing & Global Delivery**

A two-part guide covering routing and global content delivery for static websites:

**• Static Website Routing**  
Connecting Azure Front Door to a static website and validating routing end-to-end.

**• Modern CDN Delivery (Front Door Standard)**  
Azure CDN is retired for new deployments, and **Front Door Standard** now provides the modern CDN experience.

This lab covers:
- Global edge delivery  
- Caching behavior  
- Routing validation  
- The small quirks you only notice after going global  

📖 **[View Full Lab →](./labs/Azure%20Front%20Door-Static%20Website%20Hosting%20Lab.md)**  

> ☕ Fun fact: Front Door labs pair perfectly with a strong espresso — global delivery never tasted so good.

---

## 🛠️ Upcoming Labs

### **Azure Front Door Rules Engine — Practical Scenarios**

Real-world rule patterns including:
- Redirects and rewrites  
- Header manipulation  
- Cache overrides  
- The classic “why isn’t this rule firing yet?” troubleshooting flow  

---

### **Azure Front Door Premium — Private Link End-to-End Lab**

A deeper dive into secure global architectures using **Front Door Premium with Private Link**:
- Private origins  
- Locked-down storage accounts  
- Global delivery without exposing backend services  

> ☕ Advanced labs are best tackled with focus and your favorite cup of coffee nearby.

---

## 🧠 AZ-104 Skills Covered

- Manage Azure identities and governance  
- Implement and manage storage  
- Configure and manage virtual networking  
- Monitor and maintain Azure resources  

