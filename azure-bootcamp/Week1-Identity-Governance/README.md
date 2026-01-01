# 📘 Week 1 — Identity, RBAC & Managed Identity  
### *Identity-first. Secure-by-default. Architect-ready.*

Week 1 establishes the foundation for all Azure workloads.  
Identity is where access, automation, and security begin — so this week focuses on RBAC, Managed Identity, Key Vault, and the identity-driven patterns used in modern cloud environments.

Each lab is designed to be clear, repeatable, and aligned with real-world Azure architecture practices.

---

## 📋 Prerequisites

Before starting Week 1, ensure you have:

- **Azure Subscription** (Contributor or Owner access)
- **Azure CLI** installed  
  👉 https://learn.microsoft.com/en-us/cli/azure/install-azure-cli
- **Bicep CLI** (`az bicep install`)
- Basic familiarity with Azure Portal navigation

---

## 🎯 What You'll Learn This Week

- How Azure AD (Entra ID), RBAC, and role assignments work  
- How to enable and use **system-assigned managed identities**  
- How workloads authenticate to **Key Vault** and **Storage** without secrets  
- How to validate access using the **Portal**, **CLI**, and **REST API**  
- How to design identity-first architectures that scale  
- How to deploy identity components using **Bicep**  
- How to think like an architect when designing secure access flows  

---

## 🧪 Hands-On Labs (Week 1)

This week includes seven hands-on labs that build on each other.  
**Estimated time: 8–10 hours total (~1.5 hours per day).**

| Day | Topic | Duration | Lab File |
|-----|--------|----------|----------|
| **Day 1** | Identity Fundamentals + RBAC Basics | 1.5h | [01-identity-rbac-basics.md](./Day1/01-rbac-basics.md) |
| **Day 2** | Managed Identity + Key Vault | 1.5h | [02-managed-identity-keyvault.md](./Day2/02-keyvault-managed-identity.md) |
| **Day 3** | Azure AD Roles + RBAC Scopes | 1.5h | [03-azuread-roles-rbac-scopes.md](./Day3/03-azuread-roles-rbac-scopes.md) |
| **Day 4** | Azure Locks + Resource Policies | 1.5h | [04-locks-resource-policies.md](./Day4/04-locks-resource-policies.md) |
| **Day 5** | Access Validation (Portal + CLI) | 1.5h | [05-access-validation.md](./Day5/05-access-validation.md) |
| **Day 6** | Bicep Deployment — Identity Stack | 1.5h | [06-bicep-identity-stack.md](./Day6/06-bicep-identity-stack.md) |
| **Day 7** | Capstone Build — Identity-First Architecture | 2h | [Capstone README](./Day7/capstone-README.md) |

Each lab includes step-by-step instructions, validation steps, troubleshooting patterns, and CLI/Portal walkthroughs.

---

## 🏗️ Week 1 Capstone — Identity-First Secure Workload Architecture

A real-world scenario where a VM retrieves:

- Secrets from **Key Vault**  
- Configuration files from **Storage**  

…using **Managed Identity**, **RBAC**, and **zero secrets**.

This capstone demonstrates:

- Identity-based authentication  
- Least-privilege RBAC  
- Secure workload design  
- Modular Bicep deployment  
- End-to-end validation  

📁 **Capstone folder:**  
[./capstone/](./capstone/)

Includes:

- Architecture diagram  
- Bicep deployment  
- RBAC assignments  
- CLI + REST API validation  
- Full walkthrough in its own README  

---

## 🧹 Cleanup & Cost Management

⚠️ **Important:** Delete all resources after completing labs to avoid unnecessary Azure charges.

```powershell
az group delete --name <resource-group-name> --yes
```

---

## ☕ Week 1 Summary

By the end of Week 1, you will understand how Azure identity works in practice — not just conceptually, but through real workloads that authenticate and access resources securely.

This week sets the tone for the entire Boot Camp:  
**clean, secure, identity-first cloud engineering.**