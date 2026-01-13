
# 🌐 Day 1 — Virtual Networks & Subnets (Portal)
*The network backbone of every secure Azure architecture.*

This lab establishes the foundation for your Azure network. You'll design and deploy a hub-and-spoke architecture, apply enterprise-grade address planning, and validate your setup using the Azure Portal and VS Code. All user accounts use the placeholder domain **@contoso.com** to avoid exposing the real Azure AD tenant domain. The baseline lab user is **alex.james@contoso.com**.

> **Note:** Steps 1 and 2 are performed by administrators with elevated privileges.

---


---

## 📋 Prerequisites

- **Azure Subscription** (Owner access)
- Basic familiarity with CIDR notation
- Test user `alex.james@contoso.com` created in Week 1
- Access to Azure Portal
- VS Code with Azure extensions

**⏱️ Estimated Time:** 30–45 minutes

---

## 👨‍💼 Admin Task — Step 1: Create Resource Group

1. Open Azure Portal  
2. Search for **Resource groups**  
3. Click **Create**  
4. Fill in:
   - Resource group: `rg-network-lab`
   - Region: Your preferred region  
5. Select **Review + Create** → **Create**

---

## 👨‍💼 Admin Task — Step 2: Assign Owner Role to Alex

1. Go to **rg-network-lab**  
2. Open **Access control (IAM)**  
3. Add role assignment → **Owner**  
4. Assign to `alex.james@contoso.com`  
5. Select **Review + assign**

---

## 🧪 Step 3: Login as Alex James

1. Open a private/incognito browser  
2. Go to **portal.azure.com**  
3. Sign in with `alex.james@contoso.com`  

All remaining steps are performed as Alex.

---


## 🎯 What You'll Learn

- How to design and deploy a Hub VNet and Spoke VNet
- How to apply a clean, scalable IP addressing strategy
- How to create `/16` workload subnets
- How to validate your network using Azure Portal and VS Code

---

## 🧠 Architecture Overview

```
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

| VNet | Address Space | Purpose |
|------|---------------|---------|
| Hub | `10.16.0.0/16` | Shared services, firewall, gateway |
| Spoke | `10.0.0.0/12` | App, data, private endpoints |

Subnets:

| Subnet | CIDR | Purpose |
|--------|------|---------|
| temp-subnet | `10.16.0.0/24` | Placeholder (Hub) |
| app-subnet | `10.1.0.0/16` | App tier |
| data-subnet | `10.2.0.0/16` | Data tier |
| private-endpoint-subnet | `10.3.0.0/16` | Private endpoints |

---

# ⚠️ Address Space Clarification — Avoiding Errors

Azure auto‑creates a default address space when creating a VNet.

### For Hub:
Azure usually auto‑populates:
```
10.0.0.0/16
```

You must edit this to:
```
10.16.0.0/16
```

### For Spoke:
Azure may auto‑populate:
```
10.0.0.0/24   ← common
```
or:
```
10.0.0.0/16   ← also common
```

Both are normal.

You must replace it with:
```
10.0.0.0/12
```

---

# ❗ Fixing the “default subnet” error (Spoke)

Azure auto‑creates this subnet:

```
default
10.0.0.0/24
```

This subnet **must be deleted**, because it blocks the `/12` address space.

If Azure shows:

> “Subnet 'default' is not valid because its IP address range is outside the IP address range of virtual network 'vnet-spoke'.”

### Fix:

1. Go to **vnet-spoke → Subnets**  
2. Delete the `default` subnet  
3. Return to **Address space**  
4. Replace the address space with:

```
10.0.0.0/12
```

5. Save  
6. Add your `/16` subnets normally  

---

# 🛠️ Step 4 — Create Hub VNet

1. Virtual Networks → **Create**  
2. Basics:
   - Name: `vnet-hub`
   - Resource group: `rg-network-lab`
3. IP Addresses:
   - Edit default → `10.16.0.0/16`
   - Add subnet:
     - Name: `temp-subnet`
     - Range: `10.16.0.0/24`
4. Select **Review + Create** → **Create**

---

# 🛠️ Step 5 — Create Spoke VNet

1. Virtual Networks → **Create**  
2. Basics:
   - Name: `vnet-spoke`
   - Resource group: `rg-network-lab`

---

## ✔ Fix the Address Space

Azure may auto‑populate:

```
10.0.0.0/24
```
or:
```
10.0.0.0/16
```

Replace it with:

```
10.0.0.0/12
```

If Azure blocks the change:

- Delete the `default` subnet  
- Try again  

---

## ✔ Add the Spoke Subnets

Add the following:

### app-subnet
```
10.1.0.0/16
```

### data-subnet
```
10.2.0.0/16
```

### private-endpoint-subnet
```
10.3.0.0/16
```

Azure may not show `/16` in the dropdown — type it manually.

---


## 🔍 Validation Checklist

| Item | Expected |
|------|----------|
| Hub VNet | `10.16.0.0/16` |
| temp-subnet | `10.16.0.0/24` |
| Spoke VNet | `10.0.0.0/12` |
| app-subnet | `10.1.0.0/16` |
| data-subnet | `10.2.0.0/16` |
| private-endpoint-subnet | `10.3.0.0/16` |
| default subnet removed | ✔ |

---


---

## 🎉 Summary

By the end of Day 1, you have:

- A clean Hub VNet (`10.16.0.0/16`)
- A scalable Spoke VNet (`10.0.0.0/12`)
- Three `/16` workload subnets
- Correct handling of Azure’s auto‑created default subnet
- A fully validated, enterprise‑grade network foundation

---

## ▶️ Next Lab

**Day 2 — NSGs & ASGs**  
[02-nsg-asg-basics.md](02-nsg-asg-basics.md)

---

## 🔗 Related Resources

