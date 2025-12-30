# Day 1 — Identity Fundamentals (RBAC, Entra Roles, Managed Identities)

> Note: All user accounts in this lab use the placeholder domain `@contoso.com` to avoid exposing my real Azure AD tenant domain.  
> Steps **1**, **2**, and **3.2** are performed by Global Administrators or administrators with the highest level of privilege.

---

## Chapters to Read
- Chapter 1 — Manage Azure AD Identities  
- Chapter 2 — Manage RBAC  

---

## Learning Objectives
- Understand Azure AD identity structure  
- Understand RBAC scopes and inheritance  
- Deploy and test Managed Identities  
- Validate access using Azure CLI  
- Observe least‑privilege behavior from a test user’s perspective  

---

# Lab Steps

---

## 1. Create BootCamp User (Admin)

- **User principal name:** `alex.james@contoso.com`  
- **Display name:** Alex James  
- **Role:** No admin roles  

This user will be used to validate RBAC behavior.

---

## 2. Create Resource Group
- **Resource group name:** `rg-identity-lab`

---

## 3. Assign RBAC Roles at Different Scopes (Admin)

Azure RBAC hierarchy:  
**Subscription → Resource Group → Resource**

### 3.1 Subscription Scope (Information Only)
- Role: **Reader**  
- Scope: Subscription  
- Effect: Would allow viewing all resources  
- **Do not assign this role** — included only to explain RBAC hierarchy.

---

Assign Alex the **Contributor** role at the resource group scope.  
This level of access is required for the lab so he can create and manage resources inside `rg-identity-lab`.

### 3.2 Resource Group Scope (Actual Assignment)
- **Role:** Contributor  
- **Scope:** `rg-identity-lab`  
- **Principal:** `alex.james@contoso.com`  

#### Expected Behavior
When Alex signs in:
- Only `rg-identity-lab` is visible  
- No other RGs appear  
- Attempts to access or create resources outside this RG result in **Access denied**  

This validates RBAC scoping and least privilege.

---

## 4. Validate RG-Level RBAC (Login as Test User)

Sign in as: `alex.james@contoso.com`

Steps:
1. Go to **Azure Portal → Resource Groups**  
2. Confirm only `rg-identity-lab` is visible  
3. Attempt to:  
   - View subscription settings  
   - Create a resource outside the RG  
   - Access another RG or resource  

**Expected Result:**  
`Access denied` — confirms correct RBAC enforcement.

---

## 5. Deploy VM with System‑Assigned Managed Identity (Admin)

### VM Configuration
- OS: Ubuntu Server 22.04 LTS  
- Name: `vm-identity-lab`  
- Resource Group: `rg-identity-lab`  
- Region: Same as storage account  
- Size: Standard_B1s  
- Disk: Standard HDD  
- Authentication: Password  
- Public IP: Enabled  

### Enable Managed Identity
- Identity → **System-assigned = On**

This allows the VM to authenticate to Azure resources without secrets.

---

## 6. Create Storage Account

- Name: `stidentitylab1234`  
- Resource Group: `rg-identity-lab`  
- Region: Same as VM  
- Redundancy: LRS  
- Account kind: StorageV2  
- Public access: Enabled  

### 6.1 Validate the Storage Account
- Create container: `labdata`  
- Upload a small test file (e.g., `test.txt`)  

---

## 7. Assign Storage Blob Data Reader to VM’s Managed Identity

- **Scope:** Storage Account  
- **Role:** Storage Blob Data Reader  
- **Principal:** `vm-identity-lab` (Managed Identity)  

**Effect:**  
VM can **read** blobs but cannot write or delete.

---

## 7.1 Least‑Privilege Validation (IAM Access Restrictions)

When Alex signs in and opens:

**Storage Account → Access Control (IAM)**

### Expected Result
Alex **cannot**:
- Assign roles  
- Remove roles  
- Modify IAM  
- View privileged assignments  

### Reason
Contributor **does not** include IAM permissions.  
IAM actions require:
- **User Access Administrator**, or  
- **Owner**, or  
- **Global Administrator**

Azure blocks IAM actions to prevent privilege escalation.

### Outcome
- RBAC is correctly scoped  
- Least‑privilege is enforced  
- Alex can manage resources but cannot modify IAM  

---

## Fixing Alex’s Access (Correct Role Combination)

To allow Alex to both **manage resources** and **assign RBAC roles**:

- Keep **Contributor** at the `rg-identity-lab` scope  
- Add **User Access Administrator** at the same scope  

### Delegation Model Used
**Allow user to assign all roles except privileged administrator roles (Recommended)**

This combination allows Alex to:
- Create and manage resources (Contributor)  
- Assign RBAC roles and manage IAM (User Access Administrator)  

Removing Contributor would prevent Alex from creating resources, so **both roles are required**.

---

# #8. Validate Access Using Managed Identity (From the VM)

This is the moment of truth — confirming that the VM’s system‑assigned managed identity can authenticate to Azure and read blob data **without** any keys, passwords, or secrets.

---

## 8.1 Connect to the VM

Use SSH from Cloud Shell or your local terminal:

```bash
ssh azureuser@<public-ip-of-vm>