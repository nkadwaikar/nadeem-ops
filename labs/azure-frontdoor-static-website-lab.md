
# Azure Front Door + Static Website Hosting Lab

Welcome to this hands-on lab demonstrating how to publish a static website using **Azure Storage Static Website Hosting** and deliver it globally through **Azure Front Door (Standard/Premium)**. This guide includes deployment, validation, troubleshooting, and key lessons learned.

---

## Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [1. Deploy Static Website](#1-deploy-static-website)
   - [1.1 Create Resource Group](#11-create-resource-group)
   - [1.2 Create Storage Account](#12-create-storage-account)
   - [1.3 Enable Static Website](#13-enable-static-website)
   - [1.4 Upload Website Files](#14-upload-website-files)
- [2. Configure Azure Front Door](#2-configure-azure-front-door)
   - [2.1 Create Front Door Profile](#21-create-front-door-profile)
   - [2.2 Create Origin Group + Origin](#22-create-origin-group--origin)
   - [2.3 Create Route](#23-create-route)
   - [2.4 Purge Cache](#24-purge-cache)
- [3. Validation & Troubleshooting](#3-validation--troubleshooting)
   - [3.1 Initial 404 Behavior](#31-initial-404-behavior)
   - [3.2 Configuration Verification](#32-configuration-verification)
   - [3.3 Successful Propagation](#33-successful-propagation)
- [4. Lessons Learned](#4-lessons-learned)

---

## Overview

This lab demonstrates how to:

- Host a static website using Azure Storage
- Publish it globally through Azure Front Door
- Validate routing and caching
- Troubleshoot propagation delays
- Interpret Front Door response headers

The final result is a globally distributed static website with edge caching and HTTPS enforcement.

---

## Architecture

```
Client
    ↓
Azure Front Door Endpoint
    ↓
Route
    ↓
Origin Group
    ↓
Static Website Endpoint (Storage Account)
    ↓
$web Container → index.html
```

---

## 1. Deploy Static Website

### 1.1 Create Resource Group

Create a dedicated resource group to isolate all lab components.

### 1.2 Create Storage Account

- Create a Storage Account (any region, LRS redundancy)
- Keep defaults unless required otherwise

### 1.3 Enable Static Website

1. Open the Storage Account
2. Go to **Static Website**
3. Enable it
4. Set:
    - **Index document:** `index.html`
    - **Error document:** optional

Static website endpoint example:

```
https://<storage-account>.z13.web.core.windows.net/
```

### 1.4 Upload Website Files

1. Go to **Containers → `$web`**
2. Upload `index.html` to the root
3. Validate:
    - Correct name
    - Correct size
    - Blob type: Block blob

Test the origin directly:

```bash
curl -I https://<storage-account>.z13.web.core.windows.net/
```

Expected:

```
HTTP/1.1 200 OK
```

---

## 2. Configure Azure Front Door

### 2.1 Create Front Door Profile

1. Create a new Azure Front Door (Standard/Premium) profile
2. Add an endpoint:

```
<frontdoor-endpoint>.z01.azurefd.net
```

### 2.2 Create Origin Group + Origin

#### Origin Group

Create a new origin group.

#### Origin

Add an origin with:

| Setting | Value |
|---------|-------|
| Origin type | Custom |
| Origin hostname | `<storage-account>.z13.web.core.windows.net` |
| Origin host header | Same as hostname |
| HTTPS port | 443 |
| Health probe | Default |

Ensure the origin shows **Healthy**.

### 2.3 Create Route

Configure the route:

| Setting | Value |
|---------|-------|
| Enable route | Yes |
| Domains | Select Front Door endpoint |
| Patterns to match | `/*` |
| Accepted protocols | HTTP and HTTPS |
| Redirect to HTTPS | Enabled |
| Origin group | Select origin group |
| Origin path | *Leave empty* |
| Forwarding protocol | **HTTPS only** |
| Caching | Enabled |

Save the route.

### 2.4 Purge Cache

Go to **Caching → Purge** and purge:

```
/*
```

This clears stale configuration and content.

---

## 3. Validation & Troubleshooting

### 3.1 Initial 404 Behavior

Testing the endpoint:

```bash
curl -I https://<frontdoor-endpoint>.z01.azurefd.net/
```

Observed:

```
HTTP/2 404
x-cache: CONFIG_NOCACHE
```

**Meaning:**
- Front Door edge POPs do not yet have the route configuration
- This is a propagation delay, not a misconfiguration

Testing `/index.html`:

```bash
curl -I https://<frontdoor-endpoint>.z01.azurefd.net/index.html
```

Same result → confirms the route has not propagated.

### 3.2 Configuration Verification

Validated:

- Static website endpoint returns `200 OK`
- `$web` contains `index.html`
- Route provisioning state: **Succeeded**
- Domain correctly associated
- Forwarding protocol correct
- Origin group correctly linked
- No origin path set
- No private endpoints or firewall restrictions

**Conclusion:** Configuration is correct. The issue is propagation delay.

### 3.3 Successful Propagation

After waiting and periodically testing:

```bash
curl -I https://<frontdoor-endpoint>.z01.azurefd.net/
```

Final successful response:

```
HTTP/2 200
content-length: <size>
x-cache: TCP_MISS
```

**Interpretation:**
- Route is active
- Origin is serving content
- Front Door is delivering the static website globally
- `TCP_MISS` = first fetch from origin
- Future requests will show `TCP_HIT` as caching activates

---

## 4. Lessons Learned

1. **`CONFIG_NOCACHE` = No active route at the edge** - Indicates a propagation delay, not a configuration error

2. **Always validate the origin independently** - If the static website endpoint returns `200 OK`, the storage configuration is correct

3. **Forwarding protocol must match the origin** - Static website endpoints require HTTPS

4. **Leave Origin Path empty** - Static website hosting handles `/` → `/index.html`

5. **Propagation delays can be longer than expected** - After multiple edits or purges, Front Door may enter a deep global sync cycle

6. **Avoid changing configuration during propagation** - Once the configuration is correct, wait for propagation to complete

7. **Headers reveal the system state:**
    - `CONFIG_NOCACHE` → no route propagated
    - `TCP_MISS` → route active
    - `TCP_HIT` → cached at edge

8. **Costs remain predictable** - Propagation delays and 404s do not generate data-transfer charges

