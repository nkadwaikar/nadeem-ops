# 🏗️ Week 1 Capstone — Secure Workload Identity Architecture  
### *Zero secrets. Full control. Identity‑first.* ☕

This capstone brings together everything learned in Week 1.  
You will build a **production-grade identity architecture** where a VM securely retrieves:

- Secrets from **Azure Key Vault**  
- Configuration files from **Azure Storage**  

…using **Managed Identity**, **RBAC**, and **zero stored credentials**.

This pattern is widely used in modern Azure workloads.

---

## ⏱️ Estimated Time
30–45 minutes (including deployment and validation)  
> ☕ Pro tip: keep a cup of coffee nearby — watching RBAC and token flows is oddly satisfying.

---

## 📋 Prerequisites

Before starting, ensure you have:

- **Azure CLI** installed ([download](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli))  
- **Bicep CLI** installed (`az bicep install`)  
- An **Azure subscription** with Contributor or Owner role  
- **jq** (optional, for JSON parsing in validation)  

---

## 🎯 Capstone Objectives

By completing this capstone, you will:

- Deploy a VM with a **system-assigned managed identity**  
- Configure **Key Vault (RBAC mode)** for secret retrieval  
- Configure **Storage Account** for blob access  
- Assign **least-privilege RBAC roles** at the correct scopes  
- Validate access using **Azure CLI** and **OAuth tokens**  
- Deploy the entire environment using **Bicep**

---

## 🧱 Architecture Overview

The architecture includes:

- **Virtual Machine** with system-assigned Managed Identity  
- **Key Vault (RBAC mode)** storing secrets  
- **Storage Account** with a private container  
- **RBAC assignments** for Key Vault + Storage  
- **Bicep deployment** for full automation  

> This pattern eliminates secrets entirely — the VM authenticates using Azure AD tokens.

---

## 📐 Architecture Diagram Conventions

- **Blue boxes:** Compute / VMs  
- **Green boxes:** Identity services (Key Vault, Managed Identity)  
- **Yellow boxes:** Storage or data endpoints  
- **Arrows:** Data / authorization flow  

**Diagram file:** [architecture-diagram.drawio](./architecture-diagram.drawio)

---

## 📂 Capstone Files

- **[main.bicep](./main.bicep)** — deploys the full environment (VM, Key Vault, Storage Account)  
- **[validation.md](./validation.md)** — step-by-step CLI and REST API validation commands  

---

## 🚀 Deployment Steps

### 1. Deploy the environment using Bicep

```bash
az deployment group create --resource-group <rg-name> --template-file main.bicep
```

This will deploy:

- Virtual Machine with system-assigned Managed Identity
- Key Vault in RBAC mode
- Storage Account with a private container

### 2. Assign RBAC roles

- Key Vault Secrets User → VM managed identity
- Storage Blob Data Reader → VM managed identity

### 3. Add a secret to Key Vault

```bash
az keyvault secret set --vault-name <keyvault-name> --name "app-secret" --value "mySuperSecretValue"
```

### 4. Upload a config file to Storage

```bash
az storage blob upload --account-name <storage-account> --container-name <container-name> --name "appsettings.json" --file ./appsettings.json
```

### 5. Validate access from the VM

SSH into the VM and retrieve the secret:

```bash
az vm run-command invoke --resource-group <rg-name> --name <vm-name> --command-id RunShellScript --scripts "az keyvault secret show --vault-name <keyvault-name> --name app-secret"
```

Download the blob using OAuth token:

```bash
az storage blob download --container-name <container-name> --name "appsettings.json" --file ./downloaded-appsettings.json --auth-mode login --account-name <storage-account>
```

> ☕ Optional: sip a coffee while your tokens flow — it's oddly satisfying to see RBAC in action.

---

## ⚠️ Common Issues & Troubleshooting

| Issue                              | Solution                                                  |
| ---------------------------------- | --------------------------------------------------------- |
| RBAC role not taking effect        | Wait 2–3 minutes for role propagation                     |
| "Not authorized to perform action" | Verify role assignment scope matches resource             |
| Bicep deployment fails             | Check Azure CLI version: `az version`                     |
| Key Vault access denied            | Ensure VM's managed identity is assigned the correct role |

---

## 🔍 Validation Checklist

From the VM, verify:

- ✅ Can the VM retrieve a Key Vault secret? (`az keyvault secret show --name app-secret`)
- ✅ Can the VM read a blob from Storage? (Download via SAS or OAuth)
- ✅ Are no secrets stored on the VM?
- ✅ Are RBAC roles scoped correctly? (`az role assignment list --scope <resource-id>`)
- ✅ Does the Bicep deployment output expected values?

> ☕ Optional: Validate with a coffee in hand — seeing tokens work feels rewarding.

---

## 🎓 AZ-104 Skills Practiced

- **Implement and manage Azure identities and governance** (RBAC, Managed Identity)
- **Implement and manage storage** (Blob access, least-privilege roles)
- **Monitor and troubleshoot Azure resources** (validation via CLI & tokens)
- **Deploy infrastructure using Bicep** (IaC)

---

## 📝 Capstone Summary

This capstone demonstrates a core Azure pattern:

> **Workloads authenticate using Managed Identity, not secrets.**

You now have a **secure, repeatable identity architecture** suitable for real-world environments — and a strong portfolio piece to show your expertise.
