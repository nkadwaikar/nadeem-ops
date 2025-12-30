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
- Region: East US2  
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

### 8 Connect to the VM

Use SSH from Cloud Shell or your local terminal:

```bash
ssh azureuser@<public-ip-of-vm>

**Once connected, your prompt should look like:

azureuser@vm-identity-lab:~$.


### 8.1 Connect to the VM

Use SSH from Cloud Shell or your local terminal:

```bash
ssh azureuser@<public-ip-of-vm>
```

Once connected, your prompt should look like:

```
azureuser@vm-identity-lab:~$
```

---

### 8.2 Install Azure CLI (Required on Ubuntu VMs)

Ubuntu VMs do **not** include Azure CLI by default. Install it:

```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

Verify installation:

```bash
az version
```

---

### 8.3 Authenticate Using the VM’s Managed Identity

Run the following command **inside the VM**:

```bash
az login --identity
```

**Expected Result:**  
Azure returns a JSON object showing:

- `"assignedIdentityInfo": "MSI"`
- `"name": "systemAssignedIdentity"`
- `"type": "servicePrincipal"`

This confirms the VM authenticated using its **system‑assigned managed identity**.

---

### 8.4 Access the Storage Account Using RBAC (No Keys)
*This is the moment of truth — confirming that the VM’s system‑assigned managed identity can authenticate to Azure and read blob data **without** any keys, passwords, or secrets
```bash
az storage blob list \
  --account-name <storageaccountname> \
  --container-name <containername> \
  --auth-mode login
```

**Expected Result:**  
- Blob list is returned successfully  
- No storage account keys or SAS tokens are used  
- No fallback warnings appear  
- Access is granted purely through the **Storage Blob Data Reader** role  

This confirms:
- Managed Identity is working  
- RBAC permissions are correct  
- Least‑privilege access is enforced  

---

### 8.5 Troubleshooting Managed Identity Access

#### **Issue: `az: command not found`**
Azure CLI is not installed.

Fix:
```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

---

#### **Issue: `AuthorizationPermissionMismatch`**
The VM’s managed identity does not have the required data‑plane role.

Fix: Assign **Storage Blob Data Reader** at the storage account or container scope.

---

#### **Issue: `ResourceNotFound`**
Incorrect storage account or container name.

Fix: Verify names in Azure Portal.

---

#### **Issue: Command falls back to account keys**
Cause:
- Not using `--auth-mode login`
- Running from Cloud Shell instead of the VM

Fix:
- Run commands **inside the VM**
- Always include:
```bash
--auth-mode login
```

---

#### **Issue: `az login --identity` returns a user instead of service principal**
Cause: Running in Cloud Shell.

Fix: SSH into the VM and retry.

---

### 8.6 Clean Up Resources (Recommended)

Once you have completed the lab and validated managed identity access, delete the resource group to avoid unnecessary costs:

```bash
az group delete \
  --name rg-identity-lab \
  --yes --no-wait
```
