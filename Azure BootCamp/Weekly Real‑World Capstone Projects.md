
# 📘 **Week 1 Capstone — Secure Workload Identity Architecture**  
### *Identity, RBAC, Managed Identity, Key Vault, Storage*

**Scenario:**  
A development team needs a secure way for their VM‑based application to read secrets and configuration files without storing credentials.

**Deliverables:**
- Key Vault (RBAC mode)  
- VM with system‑assigned managed identity  
- Secret stored in Key Vault  
- Storage Account with private container  
- RBAC assignments:
  - Key Vault Secrets Officer (admin)
  - Key Vault Secrets User (VM)
  - Storage Blob Data Reader (VM)
- VM retrieves:
  - Secret from Key Vault  
  - Config file from Storage  
- REST API validation (OAuth token → Storage)  
- **Day 7 Bicep:** Deploy the entire environment declaratively  

**Portfolio Artifact:**  
“Secure Workload Identity Architecture on Azure — End‑to‑End Implementation”

---

# 📗 **Week 2 Capstone — Secure Network Architecture with Private Endpoints**  
### *VNets, NSGs, routing, private endpoints, DNS*

**Scenario:**  
A company wants to secure all traffic to Key Vault and Storage by removing public access and routing everything through private endpoints.

**Deliverables:**
- Hub VNet + spoke VNet  
- Subnets for workloads, private endpoints, and management  
- NSGs + ASGs  
- Route tables (UDRs)  
- Private endpoints for:
  - Key Vault  
  - Storage  
- Private DNS Zones + auto‑registration  
- VM in spoke network accessing Key Vault/Storage privately  
- **Day 7 Bicep:** VNet + NSGs + Private Endpoints + DNS  

**Portfolio Artifact:**  
“Zero‑Trust Network Architecture with Private Endpoints on Azure”

---

# 📘 **Week 3 Capstone — Scalable Compute + Secure Storage Architecture**  
### *VMSS, Load Balancer, disks, snapshots, storage security*

**Scenario:**  
A production web application must scale automatically and store logs/configuration securely.

**Deliverables:**
- VM Scale Set (Linux or Windows)  
- Load Balancer (public or internal)  
- Autoscale rules  
- Managed disks + snapshots  
- Storage Account with:
  - Containers  
  - File shares  
  - Lifecycle policies  
  - Firewall rules  
- VMSS identity accessing Storage  
- **Day 7 Bicep:** VMSS + LB + Storage + Policies  

**Portfolio Artifact:**  
“Highly Available Compute Architecture with Secure Storage on Azure”

---

# 📙 **Week 4 Capstone — Monitoring, Backup & Automation Baseline**  
### *Azure Monitor, Log Analytics, Alerts, Backup, Automation*

**Scenario:**  
An operations team needs a monitoring and backup baseline for all production workloads.

**Deliverables:**
- Log Analytics Workspace  
- Diagnostic settings for:
  - VM  
  - Storage  
  - Key Vault  
  - Network resources  
- Metric alerts + Log alerts  
- Action Groups (email/SMS/webhook)  
- Recovery Services Vault  
- VM backup + File share backup  
- Automation Account:
  - Update management  
  - Runbook (e.g., stop/start VMs)  
- **Day 7 Bicep:** LAW + Diagnostics + Alerts + Backup Policies  

**Portfolio Artifact:**  
“Enterprise Monitoring & Backup Baseline for Azure Workloads”

---

# 🎯 Why Weekly Capstones Are a Game‑Changer

- You produce **4 real-world architectures** in 4 weeks  
- Each capstone becomes a **GitHub portfolio project**  
- Each one maps directly to AZ‑104 exam domains  
- You build confidence through repetition  
- You learn portal → CLI → Bicep → architecture  
- You demonstrate architect‑level thinking  
