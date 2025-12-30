# Day 2 — Azure Key Vault + Managed Identity (VM → Key Vault Secret)

> Note: This lab continues from **Day 1**, using the same VM (`vm-identity-lab`) and Resource Group (`rg-identity-lab`).  
> All user accounts use the placeholder domain `@contoso.com` to avoid exposing my real Azure AD tenant domain.  
> Steps requiring IAM changes must be performed by a Global Administrator or User Access Administrator.

---

## Chapters to Read
- Chapter 10 — Secure Azure Resources with Azure Key Vault  
- Chapter 11 — Implement Managed Identities  

---

## Learning Objectives
- Deploy Azure Key Vault using RBAC authorization  
- Create and manage secrets  
- Assign Key Vault RBAC roles to a Managed Identity  
- Authenticate to Key Vault from a VM **without secrets**  
- Validate least‑privilege behavior  
- Troubleshoot Key Vault access issues  

---

# Lab Steps

---

## 1. Create Key Vault (Admin)

### Configuration
- **Name:** `kv-identity-lab`  
- **Resource Group:** `rg-identity-lab`  
- **Region:** Same as VM  
- **SKU:** Standard  
- **Soft Delete:** Enabled  
- **Purge Protection:** Optional  
- **Access Model:** **RBAC** (not Access Policies)

### Azure CLI (optional)
```bash
az keyvault create \
  --name kv-identity-lab \
  --resource-group rg-identity-lab \
  --location eastus \
  --enable-rbac-authorization true