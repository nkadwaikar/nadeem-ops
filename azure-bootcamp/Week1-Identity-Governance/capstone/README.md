# 🏗️ Week 1 Capstone — Secure Workload Identity Architecture  
### *Zero secrets. Full control. Identity‑first.*

This capstone brings together everything learned in Week 1.  
You will build a real‑world identity architecture where a VM securely retrieves:

- Secrets from **Azure Key Vault**  
- Configuration files from **Azure Storage**  

…using **Managed Identity**, **RBAC**, and **zero stored credentials**.

This is a production‑grade pattern used across modern Azure workloads.

---

## 🎯 Capstone Objectives

By completing this capstone, you will:

- Deploy a VM with a **system‑assigned managed identity**  
- Configure **Key Vault (RBAC mode)** for secret retrieval  
- Configure **Storage Account** for blob access  
- Assign least‑privilege RBAC roles at the correct scopes  
- Validate access using **Azure CLI** and **OAuth tokens**  
- Deploy the entire environment using **Bicep**

---

## 🧱 Architecture Overview

The architecture includes:

- **Virtual Machine** with system‑assigned MI  
- **Key Vault (RBAC mode)** storing secrets  
- **Storage Account** with a private container  
- **RBAC assignments** for Key Vault + Storage  
- **Bicep deployment** for full automation  

This pattern eliminates secrets entirely — the VM authenticates using Azure AD tokens.

---

## 📂 Capstone Folder

Your capstone folder includes the core files needed to deploy and validate the architecture:

- **architecture-diagram.drawio** — high‑level identity flow  
- **main.bicep** — deploys the full environment  
- **validation.md** — CLI + REST API validation steps  

---

## 🚀 Deployment Steps (High‑Level)

1. **Deploy the environment using Bicep**  
   - VM with Managed Identity  
   - Key Vault (RBAC mode)  
   - Storage Account + container  

2. **Assign RBAC roles**  
   - Key Vault Secrets User  
   - Storage Blob Data Reader  

3. **Add a secret to Key Vault**  
   - e.g., `app-secret`  

4. **Upload a config file to Storage**  
   - e.g., `appsettings.json`  

5. **Validate access from the VM**  
   - Retrieve Key Vault secret  
   - Download blob using OAuth token  

---

## 🔍 Validation Checklist

From the VM:

- Can the VM retrieve a Key Vault secret?  
- Can the VM read a blob from Storage?  
- Are no secrets stored on the VM?  
- Are RBAC roles scoped correctly?  
- Does the Bicep deployment output expected values?  

If all answers are **yes**, your identity architecture is working.

---

## 📝 Capstone Summary

This capstone demonstrates a core Azure pattern:

> **Workloads authenticate using Managed Identity, not secrets.**

You now have a secure, repeatable identity architecture that scales across real‑world environments — and a strong portfolio piece to show it.