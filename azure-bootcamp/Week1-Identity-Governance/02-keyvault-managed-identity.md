
# Day 2 — Azure Key Vault + Managed Identity (Admin Identity + VM Workload Identity)

> This lab continues from **Day 1**, using the same VM (`vm-bootcamp`) and Resource Group (`rg-bootcamp`).  
> All user accounts use the placeholder domain `@contoso.com` to avoid exposing my real Azure AD tenant domain.  
> Steps requiring IAM changes must be performed by a Global Administrator or User Access Administrator.

---

## Chapters to Read
- **Chapter 10 — Secure Azure Resources with Azure Key Vault**  
- **Chapter 11 — Implement Managed Identities**

---

## 1. Learning Objectives

By the end of this combined Day 2 lab, you will:

- Validate Azure CLI context (tenant + subscription + identity).
- Confirm visibility of the lab Key Vault.
- Understand how RBAC affects Key Vault data‑plane operations.
- Create and read a secret using an **admin identity**.
- Enable and validate a **system‑assigned managed identity** on a VM.
- Assign least‑privilege RBAC roles for Key Vault access.
- Retrieve a Key Vault secret using the **VM’s managed identity**.
- Troubleshoot real-world `ForbiddenByRbac` and identity‑context issues.

This completes the full Key Vault identity lifecycle.

---

## 2. Lab Setup and Assumptions

**Resources:**

- **Resource group:** `rg-bootcamp`
- **Key Vault:** `kv-identity-lab1`
- **Location:** `eastus`
- **VM:** `vm-bootcamp` (Linux)
- **Secret:** `db-password` (created during this lab)

**Access model:**

- Key Vault uses **Azure RBAC** (not access policies).
- Admin identity has rights to manage RBAC.
- VM will authenticate using its **system-assigned managed identity**.

---

# Part 1 — Admin Identity → Key Vault

## 3. Validate Azure CLI Context on the VM

All operations are run from **inside** the VM (`vm-bootcamp`).

### 3.1 Check current account context

```bash
az account show
```

Confirm:

- `tenantId` matches the intended admin tenant.  
- `id` (subscriptionId) matches the subscription hosting `rg-bootcamp`.  
- `user.name` reflects your admin identity.  

If incorrect:

```bash
az logout
az login --tenant <ADMIN-TENANT-ID>
```

---

## 4. Verify Key Vault Visibility

```bash
az keyvault list -o table
```

Expected output:

```
Location    Name              ResourceGroup
----------  ----------------  ---------------
eastus      kv-identity-lab1  rg-bootcamp
```

If empty → tenant/subscription mismatch.

---

## 5. First Attempt to Create a Secret (Expected Failure)

```bash
az keyvault secret set \
  --vault-name kv-identity-lab1 \
  --name db-password \
  --value "P@ssw0rd123!"
```

Expected error:

```
ForbiddenByRbac
Caller is not authorized to perform action
Assignment: (not found)
```

### Interpretation

- Authentication succeeded  
- Key Vault exists  
- **Authorization failed**  
- Admin identity lacks Key Vault data‑plane RBAC  

---

## 6. Assign RBAC Permissions for the Admin Identity

Azure Portal →  
**Key Vault → kv-identity-lab1 → Access control (IAM)**

Add role assignment:

- **Role:** `Key Vault Secrets Officer`  
- **Assign access to:** User  
- **User:** admin@contoso.com  
- **Scope:** This resource  

Wait 30–60 seconds for RBAC propagation.

---

## 7. Successful Secret Creation

```bash
az keyvault secret set \
  --vault-name kv-identity-lab1 \
  --name db-password \
  --value "P@ssw0rd123!"
```

Expected output includes:

- `created` timestamp  
- `id` of the secret  
- `value` returned  

---

## 8. Validate Secret Retrieval (Admin Identity)

```bash
az keyvault secret show \
  --vault-name kv-identity-lab1 \
  --name db-password \
  --query value -o tsv
```

Expected:

```
P@ssw0rd123!
```

Admin identity → Key Vault is now fully validated.

---

# Part 2 — VM Managed Identity → Key Vault

## 9. Enable the VM’s Managed Identity

Azure Portal →  
**Virtual Machines → vm-bootcamp → Identity**

- System assigned: **On**  
- Save  

Azure creates a service principal for the VM.

---

## 10. Assign Key Vault RBAC to the VM Identity

Azure Portal →  
**Key Vault → kv-identity-lab1 → Access control (IAM)**

Add role assignment:

- **Role:** `Key Vault Secrets User`  
- **Assign access to:** Managed identity  
- **Identity:** vm-bootcamp  
- **Scope:** This resource  

This grants **read-only** access to secrets.

---

## 11. Log In Using the VM’s Managed Identity

SSH into the VM:

```bash
az login --identity --allow-no-subscriptions
```

Expected:

```
"user": {
  "assignedIdentityInfo": "MSI",
  "name": "systemAssignedIdentity",
  "type": "servicePrincipal"
}
```

This confirms Azure CLI is now acting **as the VM**.

---

## 12. Retrieve the Secret Using the VM Identity

```bash
az keyvault secret show \
  --vault-name kv-identity-lab1 \
  --name db-password \
  --query value -o tsv
```

Expected:

```
P@ssw0rd123!
```

This validates:

- VM identity authentication  
- RBAC permissions  
- Key Vault access  
- Zero credentials used  

This is the exact pattern used by production workloads.

---
## 13. Clean Up Resources (Recommended)

Once you have completed the lab, delete the resource group to avoid unnecessary costs:

```bash
az group delete \
  --name rg-bootcamp \
  --yes --no-wait
```

---

# 14. Troubleshooting Notes

### Issue  
```
ForbiddenByRbac
Caller is not authorized
```

**Cause:** Missing RBAC assignment  
**Fix:** Assign `Key Vault Secrets Officer` (admin) or `Key Vault Secrets User` (VM)

---

### Issue  
```
No access was configured for the managed identity
```

**Cause:** VM identity has no subscription-level roles  
**Fix:**  

```bash
az login --identity --allow-no-subscriptions
```

---


# 15. Completion Criteria

You have completed Day 2 when:

✔ Admin identity can create and read secrets  
✔ VM identity is enabled  
✔ VM identity has Key Vault Secrets User role  
✔ `az login --identity` succeeds  
✔ VM retrieves `db-password` successfully  
✔ No credentials or secrets were stored anywhere  
