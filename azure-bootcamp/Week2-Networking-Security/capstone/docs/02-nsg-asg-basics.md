
# 🔐 Day 2 — NSGs & ASGs (Portal)
*Securing workloads with modular network controls.*

This lab builds on your hub-and-spoke network by introducing Network Security Groups (NSGs) and Application Security Groups (ASGs) for micro-segmentation and subnet-level security. You’ll work as `alex.james@contoso.com` with Owner access, and validate everything using Azure Portal and VS Code.

---


---

## 📋 Prerequisites

- Day 1 lab completed (Hub & Spoke VNets with subnets)
- Signed in as `alex.james@contoso.com`
- Resource group: `rg-network-lab`
- VNets:
   - `vnet-hub` → `10.16.0.0/16`
   - `vnet-spoke` → `10.0.0.0/12`
- Subnets:
   - `app-subnet` → `10.1.0.0/16`
   - `data-subnet` → `10.2.0.0/16`
   - `private-endpoint-subnet` → `10.3.0.0/16`

---


## 🎯 What You'll Learn

- How to create three NSGs (App, Data, Private Endpoint)
- How to create three ASGs (App, Data, Private Endpoint)
- How to associate NSGs with subnets
- How to validate NSG rules and ASG membership
- How to prepare for Day 3: peering and firewall

---

## 🧠 Architecture Overview

```plaintext
vnet-spoke
├── app-subnet (NSG: nsg-app, ASG: asg-app)
├── data-subnet (NSG: nsg-data, ASG: asg-data)
└── private-endpoint-subnet (NSG: nsg-private, ASG: asg-private)
```

---

# 🛠️ Step 1 — Create NSGs

Repeat the following steps for each NSG:

### NSG: `nsg-app`

1. Go to **Networking → Network security groups**  
2. Click **Create**  
3. Fill in:
   - Name: `nsg-app`
   - Resource group: `rg-network-lab`
   - Region: Same as VNet  
4. Click **Review + Create** → **Create**

Repeat for:

- `nsg-data`  
- `nsg-private`

---

# 🛠️ Step 2 — Create ASGs

Repeat the following steps for each ASG:

### ASG: `asg-app`

1. Go to **Networking → Application security groups**  
2. Click **Create**  
3. Fill in:
   - Name: `asg-app`
   - Resource group: `rg-network-lab`
   - Region: Same as VNet  
4. Click **Review + Create** → **Create**

Repeat for:

- `asg-data`  
- `asg-private`

---

# 🛠️ Step 3 — Associate NSGs with Subnets

### Associate `nsg-app` with `app-subnet`

1. Go to **Virtual networks → vnet-spoke → Subnets**  
2. Select `app-subnet`  
3. Under **Network security group**, choose `nsg-app`  
4. Save

Repeat for:

- `data-subnet` → `nsg-data`  
- `private-endpoint-subnet` → `nsg-private`

---

# 🛠️ Step 4 — Add NSG Rules (Optional for Day 2)

You can optionally add basic rules to each NSG:

### Example: Allow RDP from your IP

1. Go to `nsg-app` → **Inbound security rules**  
2. Click **Add**  
3. Fill in:
   - Name: `Allow-RDP`
   - Priority: `100`
   - Source: `IP Addresses` → your public IP  
   - Destination: `Any`
   - Port: `3389`
   - Protocol: `TCP`
   - Action: `Allow`  
4. Save

Repeat for other NSGs if needed.

---

# 🛠️ Step 5 — Validate ASGs (Optional for Day 2)

ASGs are used in NSG rules to group workloads.  
You’ll assign VMs to ASGs on Day 3.

For now, confirm:

- `asg-app`, `asg-data`, `asg-private` exist  
- Region matches VNet  
- Resource group is correct

---


## 🔍 Validation Checklist

| Item | Expected |
|------|----------|
| NSGs created | `nsg-app`, `nsg-data`, `nsg-private` |
| ASGs created | `asg-app`, `asg-data`, `asg-private` |
| NSGs associated | Each NSG linked to correct subnet |
| ASGs validated | Exist, correct region, correct RG |
| No errors | ✔ |

---


---

## 🎉 Summary

By the end of Day 2, you have:

- Modular NSGs for each workload tier
- ASGs ready for VM grouping
- Subnet-level security enforcement
- A clean foundation for Day 3 peering and firewall rules

---

## ▶️ Next Lab

**Day 3 — Hub-Spoke Architecture & Peering**  
[03-hub-spoke-peering.md](03-hub-spoke-peering.md)

---

## 🔗 Related Resources