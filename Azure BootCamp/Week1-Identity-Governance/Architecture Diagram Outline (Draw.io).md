# Architecture Diagram Outline — Identity + Governance

## Components to Include

### Identity Layer
- Entra ID tenant
- Users + Groups
- Entra Roles
- PIM (eligible → active flow)
- VM with System‑Assigned Managed Identity

### Access Control Layer
- RBAC scopes:
  - Subscription
  - Resource Group
  - Resource
- Role assignments:
  - Reader
  - Contributor
  - Storage Blob Data Reader

### Storage Layer
- Storage Account
- Replication (ZRS/GRS)
- Private Endpoint
- Private DNS Zone
- NSG (optional)

### Governance Layer
- Management Group
- Subscription under MG
- Built‑in policy (e.g., require tags)
- Custom policy (JSON)
- Compliance results

### Network Flow
- VM → Private Endpoint → Storage
- DNS resolution path
- Identity authentication path

### Recommended Diagram Layout
- **Top:** Management Group + Policies  
- **Middle:** Identity (Entra ID, PIM, RBAC)  
- **Bottom Left:** VM + Managed Identity  
- **Bottom Right:** Storage + Private Endpoint + DNS  
- **Arrows:**  
  - Identity → RBAC → Storage  
  - VM → Private Endpoint → Storage  
  - PIM → Role Activation  