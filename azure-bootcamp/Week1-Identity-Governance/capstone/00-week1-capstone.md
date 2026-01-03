# 🏗️ **Week 1 Capstone — Identity‑First, Governance‑Ready Landing Zone**  
### *Zero secrets. Zero trust. Fully governed. Fully observable.*

> This is my Week 1 capstone for the Azure Bootcamp.  
> The full implementation will be published once all validation steps and diagrams are complete.

---

## 🎯 **Purpose of This Capstone**

This project brings together everything from Week 1:

- Identity fundamentals  
- Managed Identity + Key Vault  
- RBAC scopes  
- Resource locks  
- Azure Policy (Audit + Deny)  
- Access validation  
- Azure Monitor + Activity Logs  
- KQL queries  
- IaC (Bicep)  

The goal is to build a **secure, identity-first workload** that follows enterprise governance and observability patterns used in NZ/AU cloud environments.

---

## 🧱 **Architecture Overview**  
*(Coming Soon — diagram will be added here)*

This architecture includes:

- A VM with a **system-assigned Managed Identity**  
- Key Vault in **RBAC mode**  
- Storage account with identity-based access  
- RBAC assignments at correct scopes  
- Resource locks to protect critical resources  
- Azure Policy enforcing governance  
- Log Analytics Workspace for observability  
- Diagnostic settings for logs and metrics  

---

## 📂 **Repository Structure**

```
capstone/
├── 00-week1-capstone.md
├── architecture/              # Coming Soon
├── bicep/                     # IaC modules
├── governance/                # RBAC, locks, policies
├── observability/             # Logs + KQL
├── validation/                # End-to-end tests
└── docs/                      # Security + governance notes
```

This structure is designed for clarity, auditability, and professional presentation.

---

## 🚀 **What This Capstone Demonstrates**

### **Identity Layer**
- VM authenticates to Key Vault using Managed Identity  
- No secrets, no connection strings, no SAS tokens  

### **Governance Layer**
- RBAC least privilege  
- Resource locks (delete + read-only)  
- Azure Policy (Audit + Deny)  
- Compliance validation  

### **Observability Layer**
- Activity Logs → Log Analytics  
- Diagnostic settings enabled  
- KQL queries for deny, RBAC, lock, and Key Vault events  

### **IaC Layer**
- Modular Bicep deployment  
- Reusable modules for VM, KV, Storage, Identity, Diagnostics, Policy  

---

## 🧪 **Validation Plan**  
*(Coming Soon — screenshots + CLI output will be added)*

Validation will include:

- Managed Identity access to Key Vault  
- Managed Identity access to Storage  
- RBAC enforcement  
- Lock enforcement  
- Policy deny tests  
- Activity Log events  
- KQL queries returning expected results  

---

## 🔐 **Security & Governance Controls**  
*(Coming Soon — full documentation in `/docs`)*

This capstone aligns with:

- Zero Trust principles  
- Identity-first access  
- RBAC least privilege  
- Governance enforcement  
- Observability as a security requirement  

---

## 🧠 **Lessons Learned**  
*(Coming Soon — will be filled after full implementation)*

This section will capture:

- Identity-first design insights  
- Governance patterns  
- Observability best practices  
- IaC modularization lessons  

---

## 📌 **Completion Checklist**

| Item | Status |
|------|--------|
| Identity-first VM | ⏳ Coming Soon |
| Key Vault (RBAC mode) | ⏳ Coming Soon |
| Storage account | ⏳ Coming Soon |
| RBAC roles assigned | ⏳ Coming Soon |
| Locks applied | ⏳ Coming Soon |
| Policies assigned | ⏳ Coming Soon |
| Activity Logs → LAW | ⏳ Coming Soon |
| Diagnostic settings | ⏳ Coming Soon |
| KQL queries validated | ⏳ Coming Soon |
| VM retrieves KV secret | ⏳ Coming Soon |
| VM reads blob via OAuth | ⏳ Coming Soon |
| Bicep deployment modular | ⏳ Coming Soon |
| Architecture diagram added | ⏳ Coming Soon |

---

## ▶️ **Next Capstone (Week 2)**  
**Secure Hub-Spoke Network Architecture**  
(VNet, NSGs, Private Endpoints, Private DNS)

---

# 🎉 Your Final Week 1 Project Is Ready

You can now paste this entire content into:

```
Week1-Identity-Governance/capstone/00-week1-capstone.md
```