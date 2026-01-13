# 🔐 **Day 2 — Network Security Groups (NSGs) & Application Security Groups (ASGs)**  
### *Micro‑segmentation and workload‑aware security in Azure.*

> **Note:** All steps today are performed as **alex.james@contoso.com** unless otherwise stated.  
> This lab builds directly on the VNets and subnets created on Day 1.

---

## 📋 **Prerequisites**

Before starting this lab, ensure you have:

- Completed **Day 1 — VNet & Subnet Design**  
- Hub VNet: `10.16.0.0/16`  
- Spoke VNet: `10.0.0.0/12`  
- Subnets:
  - `app-subnet` → `10.1.0.0/16`
  - `data-subnet` → `10.2.0.0/16`
  - `private-endpoint-subnet` → `10.3.0.0/16`
- At least one VM in:
  - `app-subnet`
  - `data-subnet`

**⏱️ Estimated Time:** 45–60 minutes

---

## 🎯 **Objectives**

By the end of this lab, you will:

- Understand the purpose of NSGs and ASGs  
- Create workload‑aware ASGs  
- Apply NSGs to subnets for layered security  
- Implement least‑privilege rules between app and data tiers  
- Validate effective security rules  
- Prepare for Azure Firewall integration on Day 4

## 🧠 **Concept Overview**

### **NSGs (Network Security Groups)**  
NSGs filter traffic at the **subnet** or **NIC** level.  
They operate like stateless firewall rules.

### **ASGs (Application Security Groups)**  
ASGs group **VM NICs** logically (e.g., “app servers”, “data servers”).  
They allow you to write rules like:

```
Allow asg-app → asg-data on port 1433
```

This is cleaner and more scalable than using IP addresses.

---

## 🧩 **Step 1 — Create Application Security Groups**

### **Create ASG for App Tier**

1. Go to **Application Security Groups**
2. Click **Create**
3. Fill in:
   - **Name:** `asg-app`
   - **Resource group:** `rg-network-lab`
   - **Region:** Same as VNets
4. Click **Review + Create** → **Create**

### **Create ASG for Data Tier**

Repeat the steps with:

- **Name:** `asg-data`

---

## 🧩 **Step 2 — Assign VMs to ASGs**

### **Assign App VM to `asg-app`**

1. Go to **Virtual machines**
2. Select your **App VM**
3. Go to **Networking**
4. Under **Application security groups**, click **Configure**
5. Select **asg-app**
6. Save

### **Assign Data VM to `asg-data`**

Repeat the steps for the Data VM.

---

## 🧩 **Step 3 — Create NSGs for Subnets**

We will create two NSGs:

- `nsg-app`
- `nsg-data`

### **Create NSG for App Subnet**

1. Go to **Network security groups**
2. Click **Create**
3. Fill in:
   - **Name:** `nsg-app`
   - **Resource group:** `rg-network-lab`
4. Click **Review + Create** → **Create**

### **Create NSG for Data Subnet**

Repeat with:

- **Name:** `nsg-data`

---

## 🧩 **Step 4 — Associate NSGs with Subnets**

### **Associate `nsg-app` with `app-subnet`**

1. Open **nsg-app**
2. Go to **Subnets**
3. Click **Associate**
4. Select:
   - **VNet:** `vnet-spoke`
   - **Subnet:** `app-subnet`

### **Associate `nsg-data` with `data-subnet`**

Repeat for `nsg-data`.

---

## 🧩 **Step 5 — Create Least‑Privilege NSG Rules**

### **Rule 1 — Allow App → Data (Port 1433)**

In **nsg-data → Inbound security rules**:

| Setting | Value |
|---------|--------|
| Source | Application Security Group |
| Source ASG | `asg-app` |
| Destination | Application Security Group |
| Destination ASG | `asg-data` |
| Protocol | TCP |
| Port | 1433 |
| Action | Allow |
| Priority | 200 |

### **Rule 2 — Deny Data → App**

In **nsg-app → Inbound security rules**:

| Setting | Value |
|---------|--------|
| Source | ASG |
| Source ASG | `asg-data` |
| Destination | ASG |
| Destination ASG | `asg-app` |
| Protocol | Any |
| Port | Any |
| Action | Deny |
| Priority | 300 |

### **Rule 3 — Allow outbound to Azure Firewall (Day 4)**

In both NSGs:

| Setting | Value |
|---------|--------|
| Destination | IP Address |
| IP | `<Azure Firewall private IP>` (placeholder for Day 4) |
| Port | Any |
| Action | Allow |
| Priority | 100 |

---

## 🔍 **Step 6 — Validate Effective Security Rules**

### **Using Azure Portal**

1. Go to **App VM → Networking**
2. Click **Effective security rules**
3. Confirm:
   - App → Data allowed on 1433  
   - Data → App denied  
   - Outbound allowed only to firewall (placeholder)  

### **Using VM Testing (Optional)**

From App VM:

```
Test-NetConnection <DataVMPrivateIP> -Port 1433
```

Expected: **Success**

From Data VM:

```
Test-NetConnection <AppVMPrivateIP> -Port 1433
```

Expected: **Blocked**

---

## 🎉 ** Today you learned:**

You now have:

- Logical workload groups using ASGs  
- Subnet-level filtering using NSGs  
- Least‑privilege rules between app and data tiers  
- A security foundation ready for Azure Firewall on Day 4  
- Hands-on experience with micro‑segmentation  

