# Day 1 — Identity Fundamentals (RBAC, Entra Roles, Managed Identities)

## Chapters to Read
- Chapter 1 — Manage Azure AD Identities
- Chapter 2 — Manage RBAC

## Learning Objectives
- Understand Azure AD identity structure
- Understand RBAC scopes and inheritance
- Deploy and test Managed Identities
- Validate access using Azure CLI

## Lab Steps
1. Create Resource Group: `rg-identity-lab`
2. Assign RBAC roles at different scopes (Subscription → RG → Resource)

   ### Assign RBAC Roles at Different Scopes — Example

   Azure RBAC hierarchy:
   **Subscription → Resource Group → Resource**  
   Permissions flow downward (inheritance), never upward.

   **Subscription Scope Example**
   - Role: Reader  
   - Scope: Subscription  
   - Effect: User can view everything in the subscription  
   - Portal: Subscriptions → Access Control (IAM) → Add Role Assignment  

   **Resource Group Scope Example**
   - Role: Contributor  
   - Scope: Resource Group (`rg-identity-lab`)  
   - Effect: User can manage only resources inside this RG  

   **Resource Scope Example**
   - Role: Storage Blob Data Reader  
   - Scope: Storage Account (`stidentity123`)  
   - Effect: VM Managed Identity can read blobs only  

3. Deploy VM with System‑Assigned Managed Identity
4. Create Storage Account
5. Assign **Storage Blob Data Reader** to VM identity
6. Validate access:
   ```bash
   az login --identity
   az storage blob list --account-name <name> --container-name <container>