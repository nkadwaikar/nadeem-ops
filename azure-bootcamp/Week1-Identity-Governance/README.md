# 📘 Week 1 - Identity, RBAC & Managed Identity  
### *Identity-first. Portal-first. Coffee-powered.*

Week 1 lays the foundation for everything that follows.  
Azure identity is where access, automation, and security all begin — so this week focuses on RBAC, Managed Identity, Key Vault, and secure access patterns that real workloads rely on.

Every lab is written to be clear, repeatable, and friendly enough that even a low‑caffeine version of me can follow it.

---

## 📋 Prerequisites

Before starting Week 1, ensure you have:

- **Azure Subscription** (with Contributor or Owner role)
- **Azure CLI** installed ([install guide](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli))
- **Bicep CLI** (`az bicep install`)
- Basic understanding of Azure Portal navigation

---

## 🎯 What You'll Learn This Week

- How Azure AD, RBAC, and role assignments actually work  
- How to enable and use **system-assigned managed identities**  
- How workloads authenticate to **Key Vault** and **Storage** without secrets  
- How to validate access using the **Portal**, **CLI**, and **REST API**  
- How to structure identity-first architectures that scale  
- How to deploy the entire environment using **Bicep**

---

## 🧪 Hands‑On Labs

This week includes seven hands‑on labs that build on each other. **Estimated time: 8–10 hours total (~1.5 hours per day).**

| Day | Topic | Duration | Lab Files |
|-----|-------|----------|-----------|
| **Day 1** | RBAC + Managed Identity + Storage | 1.5h | [`(./azure-bootcamp/Week1-Identity-Governance/01-rbac-basics.md)`](./Day1-RBAC-MI-Storage/) |
| **Day 2** | Azure Key Vault + Managed Identity | 1.5h | [`(./azure-bootcamp/Week1-Identity-Governance/02-keyvault-managed-identity.md)`](./Day2-KeyVault-MI/) |
| **Day 3** | Managed Identity → Storage (Blob Read Access) | 1.5h | Pending |
| **Day 4** | RBAC Scopes Deep Dive | 1.5h | Pending |
| **Day 5** | Azure AD Basics (Users, Groups, Roles) | 1.5h | Pending |
| **Day 6** | Access Control Validation (Portal + CLI) | 1.5h | Pending |
| **Day 7** | Bicep Deployment: Identity + Key Vault + Storage | 2h | Pending |

**Each lab includes:** step‑by‑step instructions, validation steps, notes, and CLI/Portal walkthroughs.

---

## 🏗️ Week 1 Capstone — Secure Workload Identity Architecture

A real‑world scenario where a VM retrieves:

- Secrets from Key Vault  
- Config files from Storage  

...using **Managed Identity**, **RBAC**, and **zero secrets**.

**Prerequisites:** Complete Days 1–7 (or have prior knowledge of RBAC + Managed Identity).

📁 **Capstone folder:**  
[Week 1 Capstone — Secure Workload Identity Architecture](./capstone/)

Includes:

- Architecture diagram  
- Bicep deployment  
- RBAC assignments  
- CLI + REST API validation  
- Full walkthrough in its own README  

---

## 🧹 Cleanup & Cost Management

⚠️ **Important:** Delete all resources after completing labs to avoid unexpected Azure charges.

Cleanup all resources with:
```powershell
az group delete --name <resource-group-name> --yes
```

---

## ☕ Week 1 Summary

By the end of Week 1, you'll understand how Azure identity actually works — not just in theory, but in the way real workloads authenticate and access resources.  
This week sets the tone for the entire Boot Camp: clean, secure, identity‑first cloud engineering.