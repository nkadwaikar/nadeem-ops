
# Week 1 Capstone Project — Secure Workload Identity Architecture on Azure
*Boot Camp: Identity, RBAC & Managed Identity — Week 1*

> This capstone project consolidates all identity concepts from Week 1:
> - Azure AD identities  
> - RBAC  
> - Key Vault  
> - Managed Identities  
> - Storage Account (RBAC mode)  
> - Identity-based access (CLI + REST)  
>
> The goal is to build a **real-world, production-grade identity architecture** where a VM-based workload securely retrieves secrets and configuration files without storing credentials.

---

# 1. Scenario Overview

A development team is deploying an application on a VM.  
The application needs to:

- Retrieve a database password from **Azure Key Vault**
- Read a configuration file from **Azure Storage**
- Use **no secrets, no keys, no connection strings**

Your task is to design and implement a **secure, identity-based architecture** using:

- Azure AD  
- RBAC  
- Managed Identity  
- Key Vault  
- Storage Account  

This is a real-world pattern used across enterprise Azure environments.

---

# 2. Architecture Diagram (Conceptual)

```
+-----------------------------+
| Azure AD                    |
|  - Admin Identity           |
|  - VM Managed Identity      |
+-----------------------------+
             |
             | Issues OAuth Tokens
             v
+-----------------------------+
| Virtual Machine (vm-bootcamp)
|  - System-assigned MI
+-----------------------------+
      |                     |
      | Auth via MI         | Auth via MI
      v                     v
+-------------+       +----------------+
| Key Vault   |       | Storage Account|
| Secrets     |       | Blob Container |
+-------------+       +----------------+
```

---

# 3. Capstone Objectives

By completing this capstone, you will:

- Build a secure identity architecture using Azure AD + RBAC  
- Configure Key Vault for RBAC-based secret access  
- Configure Storage Account for identity-based blob access  
- Enable and validate VM Managed Identity  
- Assign least-privilege RBAC roles  
- Validate access using:
  - Azure CLI (`--auth-mode login`)
  - REST API (OAuth token → Storage)  
- Produce a **portfolio-ready architecture document**  
- (Day 7) Deploy the entire environment using **Bicep**

---

# 4. Deliverables 

Your final capstone submission includes:

### **A. Architecture Document**
- Overview  
- Diagram  
- Identity flow  
- RBAC assignments  
- Security considerations  

### **B. Hands-On Implementation**
- Key Vault (RBAC mode)  
- Storage Account (private container)  
- VM with system-assigned MI  
- Secret stored in Key Vault  
- Blob stored in Storage  
- RBAC assignments:
  - Key Vault Secrets Officer (admin)
  - Key Vault Secrets User (VM)
  - Storage Blob Data Reader (VM)

### **C. Validation Evidence**
- CLI output (secret retrieval)  
- CLI output (blob download)  
- REST API output (OAuth token → Storage)  

### **D. Day 7 Bicep Deployment**
A single Bicep deployment that creates:

- Key Vault  
- VM with MI  
- Storage Account  
- RBAC assignments  
- Container + sample blob (optional)

This becomes a **GitHub portfolio artifact**.

---

# 5. Step-by-Step Implementation

This capstone reuses the validated steps from Days 1–3.

### **Step 1 — Create Key Vault (Portal)**  
- RBAC mode  
- Soft delete + purge protection enabled  

### **Step 2 — Create Storage Account (Portal)**  
- Standard LRS  
- Private container `app-data`  

### **Step 3 — Upload Test Artifacts**
- Secret: `db-password`  
- Blob: `config.json`  

### **Step 4 — Enable VM Managed Identity**
- System-assigned MI → On  

### **Step 5 — Assign RBAC Roles**
| Resource | Role | Identity |
|----------|------|----------|
| Key Vault | Key Vault Secrets Officer | admin@contoso.com |
| Key Vault | Key Vault Secrets User | vm-bootcamp |
| Storage Account | Storage Blob Data Reader | vm-bootcamp |

### **Step 6 — Validate Access from VM**
- `az login --identity`  
- Retrieve secret  
- Download blob  
- REST API validation  

### **Step 7 — Bicep Deployment (Day 7)**
Deploy the entire architecture declaratively.

---

# 6. Validation Checklist

You have successfully completed the Week 1 Capstone when:

✔ VM retrieves Key Vault secret using MI  
✔ VM downloads blob using MI  
✔ REST API call succeeds with OAuth token  
✔ No keys, SAS tokens, or connection strings used  
✔ RBAC assignments follow least privilege  
✔ Architecture diagram created  
✔ Bicep deployment completed  
✔ Documentation added to portfolio  

---

# 7. Security Considerations (Real-World)

- No secrets stored on VM  
- No access keys used  
- RBAC-only access  
- Managed Identity lifecycle managed by Azure  
- Key Vault protected by RBAC + soft delete  
- Storage Account protected by RBAC (no public access)  
- Identity-based access is fully auditable  

---

# 8. Final Deliverable Summary

Your Week 1 Capstone includes:

- **Architecture diagram**  
- **Identity flow explanation**  
- **RBAC matrix**  
- **Portal configuration steps**  
- **CLI validation**  
- **REST API validation**  
- **Bicep deployment (Day 7)**  

