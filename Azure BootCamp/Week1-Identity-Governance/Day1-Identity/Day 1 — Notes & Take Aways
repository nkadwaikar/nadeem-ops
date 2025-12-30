# Day 1 — Notes & Key Takeaways

## 1. Identity Hierarchy (Tenant → Directory → Subscription)

- A Microsoft Entra **Tenant** has a **1:1 relationship** with the Entra Directory.
- The Directory stores **Users, Groups, Devices, Service Principals, Managed Identities**.
- A single Directory can be associated with **multiple Azure Subscriptions** (1:M mapping).
- Subscriptions inherit identity and RBAC from the Directory.
- Resource Groups and Resources sit under the subscription and follow RBAC inheritance.

**Takeaway:**  
Identity lives at the **tenant level**, authorization lives at the **subscription/resource** level.

---

## 2. RBAC Scopes and Inheritance

- RBAC hierarchy: **Subscription → Resource Group → Resource**.
- Permissions flow **downward only**, never upward.
- Subscription-level roles apply to all RGs and resources.
- Resource Group roles apply only to resources inside that RG.
- Resource-level roles enforce **least privilege** and override inherited permissions.

**Takeaway:**  
Assign roles at the **lowest scope possible** to reduce blast radius and maintain governance.

---

## 3. Privileged Administrator Roles (High-Impact)

These roles have tenant-wide authority and must be tightly controlled:

- **Global Administrator**
- **Privileged Role Administrator**
- **User Access Administrator**
- **Security Administrator**

**Key Findings:**

- These roles can modify identity, security, and governance settings.
- They require MFA and should be activated through **PIM**.
- Assign sparingly to reduce risk and maintain compliance.

**Takeaway:**  
Privileged roles should be **rare, temporary, and monitored**.

---

## 4. Job Function Roles (Operational, Least Privilege)

These roles support day-to-day operations without granting excessive access:

- **Virtual Machine Contributor**
- **Storage Account Contributor**
- **Network Contributor**
- **Website Contributor**

**Key Findings:**

- These roles support separation of duties.
- They limit blast radius by restricting access to specific resource types.
- Ideal for DevOps, operations, and engineering teams.

**Takeaway:**  
Use job-function roles for operational tasks and reserve privileged roles for governance.

---

## 5. Managed Identity Access Pattern (Day 1 Lab)

- A **System-Assigned Managed Identity** is automatically created when enabled on a VM.
- It allows the VM to authenticate to Azure services **without secrets or credentials**.
- Assigning **Storage Blob Data Reader** at the storage account or container scope enables secure blob access.
- Validation commands used:

```bash
az login --identity
az storage blob list \
  --account-name <name> \
  --container-name <container> \
  --auth-mode login