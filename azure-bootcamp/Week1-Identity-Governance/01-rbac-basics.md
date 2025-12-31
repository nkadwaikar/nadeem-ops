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
- Observe least‑privilege behavior from a test user's perspective  

---

## Lab Steps

---

## 1. Create BootCamp User (Admin)

- **User principal name:** `alex.james@contoso.com`  
- **Display name:** Alex James  
- **Role:** No admin roles  

This user will be used to validate RBAC behavior.

---

## 2. Create Resource Group

1. Open **Azure Portal**  
2. Search for **Resource groups**  
3. Select **Create**  
4. Fill in:
  - **Name:** `rg-bootcamp`
  - **Region:** your preferred region (e.g., East US)
5. Click **Review + Create → Create**

---

## 3. Assign RBAC Roles at Different Scopes (Admin)

Azure RBAC hierarchy:  
**Subscription → Resource Group → Resource**

### 3.1 Subscription Scope (Information Only)

- Role: **Reader**  
- Scope: Subscription  
- Effect: Would allow viewing all resources  
- **Do not assign this role** — included only to explain RBAC hierarchy.

### 3.2 Resource Group Scope (Actual Assignment)

Assign Alex the **Contributor** role at the resource group scope. This level of access is required for the lab so he can create and manage resources inside `rg-bootcamp`.

- **Role:** Contributor  
- **Scope:** `rg-bootcamp`  
- **Principal:** `alex.james@contoso.com`  

#### Expected Behavior

When Alex signs in:
- Only `rg-bootcamp` is visible  
- No other RGs appear  
- Attempts to access or create resources outside this RG result in **Access denied**  

This validates RBAC scoping and least privilege.

---

## 4. Validate RG-Level RBAC (Login as Test User)

Sign in as: `alex.james@contoso.com`

**Steps:**
1. Go to **Azure Portal → Resource Groups**  
2. Confirm only `rg-bootcamp` is visible  
3. Attempt to:  
  - View subscription settings  
  - Create a resource outside the RG  
  - Access another RG or resource  

**Expected Result:**  
`Access denied` — confirms correct RBAC enforcement.

---

## 5. Deploy VM with System‑Assigned Managed Identity (Admin)

### 5.1 VM Configuration

1. Go to **Virtual machines**
2. Select **Create → Azure virtual machine**

**Basics tab**
- Resource group: `rg-bootcamp`
- VM name: `vm-bootcamp`
- Region: same as RG
- Image: **Ubuntu Server 22.04 LTS**
- Size: Standard_B1s (cost‑effective)
- Authentication: **SSH public key**
- Username: `azureuser`
- SSH key: **Generate new key pair** → name it `bootcamp-key`

Click **Next** until **Review + Create**, then **Create**.  
Download the SSH key when prompted.

### 5.2 Enable Managed Identity

1. Open **vm-bootcamp**
2. Left menu → **Identity**
3. Under **System assigned**, switch to **On**
4. Click **Save**

This identity will be used to authenticate to Azure without credentials.

### 5.3 Connect to the VM

1. Go to **vm-bootcamp**
2. Select **Connect → SSH**
3. Copy the SSH command
4. Run it locally with your private key

---

## 6. Create Storage Account

- Name: `stbootcamp1234`  
- Resource Group: `rg-bootcamp`  
- Region: Same as VM  
- Redundancy: LRS  
- Account kind: StorageV2  
- Public access: Enabled  

### 6.1 Validate the Storage Account

- Create container: `labdata`  
- Upload a small test file (e.g., `test.txt`)  

---

## 7. Assign Storage Blob Data Reader to VM's Managed Identity

- **Scope:** Storage Account  
- **Role:** Storage Blob Data Reader  
- **Principal:** `vm-bootcamp` (Managed Identity)  

**Effect:**  
VM can **read** blobs but cannot write or delete.

---

## 8. Install Azure CLI (Required on Ubuntu VMs)

Ubuntu VMs do **not** include Azure CLI by default. Install it:

```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

Verify installation:

```bash
az version
```

### 8.1 Authenticate Using the VM's Managed Identity

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

### 8.2 Access the Storage Account Using RBAC (No Keys)

Verify that the VM's managed identity can authenticate and read blob data **without** any keys, passwords, or secrets:

```bash
az storage blob list \
  --account-name <storageaccountname> \
  --container-name <containername> \
  --auth-mode login
```

---

## 9. Troubleshooting Managed Identity Access

### 9.1 Issue: `az: command not found`

Azure CLI is not installed.

**Fix:**
```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

### 9.2 Issue: `AuthorizationPermissionMismatch`

The VM's managed identity does not have the required data‑plane role.

**Fix:** Assign **Storage Blob Data Reader** at the storage account or container scope.

### 9.3 Issue: `ResourceNotFound`

Incorrect storage account or container name.

**Fix:** Verify names in Azure Portal.

### 9.4 Issue: Command falls back to account keys

**Cause:**
- Not using `--auth-mode login`
- Running from Cloud Shell instead of the VM

**Fix:**
- Run commands **inside the VM**
- Always include `--auth-mode login`

---

## 10. Clean Up Resources (Recommended)

Once you have completed the lab, delete the resource group to avoid unnecessary costs:

```bash
az group delete \
  --name rg-bootcamp \
  --yes --no-wait
```
