# 🌐 Week 2 — Azure Networking & Security  
*Private. Segmented. Identity-first. Architect-ready.*

> 🚧 **STATUS: IN DEVELOPMENT**  
> Week 2 is currently being built. Daily labs and capstone documentation are in progress.

Week 2 builds the secure network backbone for all future workloads.  
You'll design and deploy a **hub-spoke architecture** with NSGs, private endpoints, and DNS — all validated manually in the Portal, then automated with Bicep on Capstone Day.

---

## 📋 Prerequisites

Before starting Week 2, ensure you have:

- **Azure Subscription** (Contributor or Owner access)  
- Basic familiarity with Azure networking concepts  
- Test user `alex.james@contoso.com` created (from Week 1)
- VS Code with Azure extensions (for Capstone Day)  
- Bicep CLI installed (`az bicep install`)  

---

## 🧭 Weekly Flow

| Day | Topic | Method | Status |
|-----|-------|--------|--------|
| **Day 1** | VNet & Subnet Design | Portal | ✅ [01-vnet-subnet-basics.md](capstone/docs/01-vnet-subnet-basics.md) |
| **Day 2** | NSGs + ASGs | Portal | 🚧 In Progress |
| **Day 3** | Hub-Spoke Peering | Portal | 🚧 Coming Soon |
| **Day 4** | Private Endpoints | Portal | 🚧 Coming Soon |
| **Day 5** | Private DNS Zones | Portal | 🚧 Coming Soon |
| **Day 6** | Network Observability | Portal | 🚧 Coming Soon |
| **Day 7** | Capstone: Full Network Stack in Bicep | VS Code + Bicep | 🚧 Coming Soon |

---

## 🏗️ Week 2 Capstone — Secure Hub-Spoke Architecture  
*A production-grade network baseline*

> 🚧 **Capstone documentation coming soon**

You'll deploy:

- Hub VNet  
- Spoke VNet  
- Peering  
- NSGs  
- Private Endpoint  
- Private DNS Zone  
- Diagnostics  
- Identity-first access validation  

---

## 📂 Folder Structure

```plaintext
Week2-Networking-Security/
├── README.md
└── capstone/
    ├── architecture/
    │   ├── week2-network-architecture.drawio
    │   └── week2-network-architecture.png
    │
    ├── docs/
    │   ├── 01-vnet-subnet-basics.md ✅
    │   ├── 02-nsg-asg-basics.md 🚧
    │   ├── 03-hub-spoke-peering.md 🚧
    │   ├── 04-private-endpoints.md 🚧
    │   ├── 05-private-dns.md 🚧
    │   ├── 06-network-observability.md 🚧
    │   └── 07-bicep-network-stack.md 🚧
    │
    ├── bicep/
    │   ├── main.bicep
    │   └── modules/
    │       ├── vnet.bicep
    │       ├── nsg.bicep
    │       ├── peering.bicep
    │       ├── private-endpoint.bicep
    │       ├── private-dns.bicep
    │       └── diagnostics-network.bicep
    │
    └── week2-capstone.md 🚧
```

---

## 🎯 What You'll Learn This Week

- How to design and implement VNets with proper subnet segmentation
- How to secure network traffic using NSGs and ASGs
- How to build hub-spoke topologies with VNet peering
- How to configure private endpoints for PaaS services
- How to set up Private DNS zones for name resolution
- How to implement network observability and diagnostics
- How to automate network infrastructure using modular Bicep

---

## 🧹 Cleanup & Cost Management

⚠️ **Important:** Delete all resources after completing labs to avoid unnecessary Azure charges.

```bash
az group delete --name <resource-group-name> --yes
```

---

## 🎉 Summary

Week 2 is about building a secure, segmented, identity-first network baseline.  
You'll learn the architecture visually in the Portal, then automate it with Bicep — just like real cloud engineers do.

By the end of Week 2, you will have:

- A working hub-spoke network architecture
- Proper network segmentation with NSGs
- Private connectivity to PaaS services
- Network monitoring and diagnostics
- A modular Bicep stack for network infrastructure
- Production-ready network patterns for future workloads