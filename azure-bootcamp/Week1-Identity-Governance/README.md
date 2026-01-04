# 📘 Week 1 — Identity, RBAC & Managed Identity  
*Identity-first. Secure-by-default. Architect-ready.*

Week 1 establishes the foundation for all Azure workloads.  
Identity is where access, automation, and security begin — so this week focuses on RBAC, Managed Identity, Key Vault, and the identity-driven patterns used in modern cloud environments.

Each lab is designed to be clear, repeatable, and aligned with real-world Azure architecture practices.

---

## 📋 Prerequisites

Before starting Week 1, ensure you have:

- **Azure Subscription** (Contributor or Owner access)
- **Azure CLI** installed  
- **Bicep CLI** (`az bicep install`)
- Basic familiarity with Azure Portal navigation

---

## 🎯 What You'll Learn This Week

- How Azure AD (Entra ID), RBAC, and role assignments work  
- How to enable and use **system-assigned and user-assigned managed identities**  
- How workloads authenticate to **Key Vault** and **Storage** without secrets  
- How to validate access using the **Portal**, **CLI**, and **REST API**  
- How to design identity-first architectures that scale  
- How to deploy identity components using **modular Bicep**  
- How to think like an architect when designing secure access flows  

---

## 🧪 Hands-On Labs (Week 1)

This week includes hands-on labs that build on each other.  
**Estimated time: ~1.5 hours per lab.**

| Day | Topic | Lab File |
|-----|-------|----------|
| **Day 1** | Identity Fundamentals | [01-identity fundamentals.md](capstone/docs/01-identity%20fundamentals.md) |
| **Day 2** | Managed Identity + Key Vault | [02-managed Identity + Azure Key Vault (Secretless Authentication).md](capstone/docs/02-managed%20Identity%20+%20Azure%20Key%20Vault%20(Secretless%20Authentication).md) |
| **Day 3** | Azure AD Roles, RBAC & Scopes | [03-azuread-roles-rbac-scopes.md](capstone/docs/03-azuread-roles-rbac-scopes.md) |
| **Day 4** | Azure Locks + Resource Policies | [04-azurelocks-resource-policies.md](capstone/docs/04-azurelocks-resource-policies.md) |
| **Day 5** | Access Validation | [05-access-validation.md](capstone/docs/05-access-validation.md) |
| **Day 6** | Azure Monitor + Activity Logs | [06-azuremonitor-activity-logs.md](capstone/docs/06-azuremonitor-activity-logs.md) |
| **Day 7** | Bicep Deployment - Identity Stack | [07-bicep-beployment-identity-stack.md](capstone/docs/07-bicep-beployment-identity-stack.md) |

Each lab includes step-by-step instructions, validation steps, troubleshooting patterns, and CLI/Portal walkthroughs.

---

## 🏗️ Week 1 Capstone — Identity-First Secure Workload Architecture

A real-world scenario where a workload retrieves:

- Secrets from **Key Vault**  
- Configuration files from **Storage**  

…using **Managed Identity**, **RBAC**, and **zero secrets**.

This capstone demonstrates:

- Identity-based authentication  
- Least-privilege RBAC  
- Secure workload design  
- Modular Bicep deployment  
- End-to-end validation  

📁 **Capstone Documentation:**

- 🏗️ [Week 1 Capstone Overview](capstone/week1-capstone.md)
- 📘 [VS Code Deployment Workflow](capstone/docs/vscode-deployment-workflow.md)  
- 🔐 [Identity-First Access Flow](capstone/docs/identity-first-access-flow.md)  
- 🛡️ [Governance Flow Diagram](capstone/docs/governance-flow.md)  
- 📝 [Lessons Learned](capstone/docs/week1-lessons-learned.md)

📁 **Capstone Implementation:**

- Modular Bicep deployment (`capstone/bicep/`)  
- RBAC assignments  
- Resource locks  
- Governance controls  

---

## 🧹 Cleanup & Cost Management

⚠️ **Important:** Delete all resources after completing labs to avoid unnecessary Azure charges.

```bash
az group delete --name <resource-group-name> --yes
```

---

## 🎉 Week 1 Summary

By the end of Week 1, you will understand how Azure identity works in practice — not just conceptually, but through real workloads that authenticate and access resources securely.

You will have:

- A working identity-first architecture  
- A modular Bicep stack  
- RBAC-based access control  
- A Key Vault in RBAC mode  
- A managed identity with least-privilege permissions  
- Governance controls (locks + policies)  
- Observability via Azure Monitor + Log Analytics  
- A capstone folder ready for CI/CD  

This week sets the tone for the entire Boot Camp:  
**clean, secure, identity-first cloud engineering.**