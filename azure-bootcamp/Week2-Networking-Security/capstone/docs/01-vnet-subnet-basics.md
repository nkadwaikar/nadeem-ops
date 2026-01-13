
# 🌐 Day 1 — VNet & Subnet Design (Portal)
*The network backbone of every secure Azure architecture.*

> **Note:** All user accounts in this lab use the placeholder domain **@contoso.com**. The baseline lab user is **alex.james@contoso.com**.
> 
> **Steps 1 and 2 are performed by administrators with elevated privileges.**

---

## 📋 Prerequisites

Before starting this lab, ensure you have:

- **Azure Subscription** (**Contributor** or **Owner** access)
- Basic familiarity with IP addressing (**CIDR** notation)
- Test user **alex.james@contoso.com** created (from Week 1)
- Access to **Azure Portal**
- **VS Code** with Azure extensions (for validation)

**⏱️ Estimated Time:** 30–45 minutes

---

## 👨‍💼 Step 1: Create Resource Group (Admin)

**Performed by an administrator (not the student user).**

**Using Azure Portal:**
1. **Open** Azure Portal
2. **Search** for **Resource groups**
3. **Click** **Create**
4. **Fill in:**
   - **Subscription:** Select your subscription
   - **Resource group:** `rg-network-lab`
   - **Region:** Your preferred region (e.g., East US)
5. **Click** **Review + Create** → **Create**

*This resource group will host all Week 2 networking components.*

---

## 👨‍💼 Step 2: Assign Contributor Role to Alex (Admin)

**Using Azure Portal:**
1. **Go to** **Resource groups** → `rg-network-lab`
2. **Click** **Access control (IAM)**
3. **Click** **Add** → **Add role assignment**
4. **Select** **Contributor**
5. **Search for** `alex.james@contoso.com` and assign

---

## 🧪 Step 3: Login as Alex (Student)

1. **Open** a private/incognito browser window
2. **Go to** **portal.azure.com**
3. **Sign in** with **alex.james@contoso.com**
4. **Accept** any first-time login prompts

*All remaining steps in this lab are performed as alex.james@contoso.com.*

---

## 🎯 Objectives

By the end of this lab, you will:

- **Design** a clean, scalable IP addressing strategy
- **Create** a **Hub VNet** and **Spoke VNet** using enterprise ranges
- **Segment** the spoke into `/16` subnets for App, Data, and Private Endpoints
- **Validate** deployments using Azure Portal and VS Code Azure Explorer

---

## 🧠 Architecture Overview

```plaintext
                ┌──────────────────────────────┐
                │            HUB VNET           │
                │         10.16.0.0/16          │
                └───────────────┬──────────────┘
                                │ Peering (Day 3)
                                ▼
                ┌──────────────────────────────┐
                │          SPOKE VNET           │
                │         10.0.0.0/12           │
                └──────────────────────────────┘
```

---

## 📐 IP Addressing Strategy

| VNet   | Address Space   | Purpose                                 |
|--------|-----------------|-----------------------------------------|
| **Hub**   | `10.16.0.0/16`   | Shared services, firewall, gateway (future) |
| **Spoke** | `10.0.0.0/12`    | Workloads, app/data tiers, private endpoints |

Subnets:

| Subnet                   | CIDR              | Purpose                        |
|--------------------------|-------------------|--------------------------------|
| `temp-subnet`            | `10.16.0.0/24`    | Placeholder (replaced on Day 3) |
| `app-subnet`             | `10.1.0.0/16`     | App workloads                   |
| `data-subnet`            | `10.2.0.0/16`     | Data workloads                  |
| `private-endpoint-subnet`| `10.3.0.0/16`     | Private endpoints               |

---

## 🛠️ Step 4: Create Hub VNet

> **Note:** Azure requires at least one subnet when creating a VNet. We will create a **temporary subnet** that will be replaced later.

**Using Azure Portal:**
1. **Go to** **Virtual Networks** → **Create**
2. **Basics tab:**
   - **Resource group:** `rg-network-lab`
   - **Name:** `vnet-hub`
   - **Region:** Same as resource group
3. **IP Addresses tab:**
   - **Address space:** `10.16.0.0/16`
   - **Add subnet:**
     - Name: `temp-subnet`
     - Range: `10.16.0.0/24`
4. **Click** **Review + Create** → **Create**

---

## 🛠️ Step 5: Create Spoke VNet

**Using Azure Portal:**
1. **Go to** **Virtual Networks** → **Create**
2. **Basics tab:**
   - **Resource group:** `rg-network-lab`
   - **Name:** `vnet-spoke`
   - **Region:** Same as hub
3. **IP Addresses tab:**
   - **Address space:** `10.0.0.0/12`
   - **Add subnet:** `app-subnet` → `10.1.0.0/16`
   - **Add subnet:** `data-subnet` → `10.2.0.0/16`
   - **Add subnet:** `private-endpoint-subnet` → `10.3.0.0/16`
4. **Click** **Review + Create** → **Create**

---

## 🔍 Validation Steps

### In Azure Portal
- **Confirm** both VNets exist in `rg-network-lab`
- **Confirm** all subnets are created
- **Confirm** address spaces match your plan

### In VS Code Azure Explorer
- **Expand** your resource group `rg-network-lab`
- **Confirm** `vnet-hub` and `vnet-spoke` appear
- **Expand** each VNet to see subnets

---

## 🧹 Cleanup (Optional)

To clean up after the lab (**admin task**):

```bash
az group delete --name rg-network-lab --yes
```

---

## 🎉 Today you learned:

- A scalable, enterprise‑grade IP addressing plan
- A hub VNet with a minimal placeholder subnet
- A spoke VNet with three `/16` workload subnets
- Hands-on experience creating VNets as a non-admin user with Contributor access
