# **Day 3 — Microsoft Entra ID Roles + RBAC Scopes (Hands‑On Lab)**  
### *Directory roles vs resource roles. Control plane vs data plane. Identity clarity unlocked.*

> This lab builds on Day 1 (RBAC Basics) and Day 2 (Managed Identity + Key Vault).  
> All user accounts use the placeholder domain `@contoso.com` to avoid exposing my real Microsoft Entra ID tenant domain.  
> Steps requiring IAM changes must be performed by an administrator with elevated privileges.

---

## 📚 Chapters to Read
- **Chapter 5 — Manage Microsoft Entra ID Roles**  
- **Chapter 6 — Understand RBAC Scopes**  
- **Chapter 7 — Control Plane vs Data Plane Permissions**

---

## 🎯 Learning Objectives

By the end of this lab, you will:

- Understand the difference between **Microsoft Entra ID roles** and **Azure RBAC roles**
- Assign directory roles and resource roles to different users
- Validate permissions from the user's perspective
- Understand control‑plane vs data‑plane access
- Observe least‑privilege behavior in real time

This is one of the most important identity concepts in Azure.

---

# 🧪 Lab Steps

---

## **1. Create a Second Test User (Admin)**

This user will test Microsoft Entra ID directory roles.

- **User principal name:** `emma.lee@contoso.com`  
- **Display name:** Emma Lee  
- **Role:** No admin roles  

This keeps the test clean and predictable.

---

## **2. Assign a Microsoft Entra ID Role (Directory Role)**

Assign Emma the **User Administrator** role.

**Azure Portal → Microsoft Entra ID → Roles and administrators → User Administrator**

Add assignment:

- **User:** `emma.lee@contoso.com`

### Expected Behavior

Emma can:

- Create users  
- Reset passwords  
- Manage groups  

Emma **cannot**:

- Access Azure resources  
- Create VMs  
- Modify resource groups  
- Access Key Vault  

This demonstrates the separation between **identity management** and **resource management**.

---

## **3. Validate Microsoft Entra ID Role Permissions (Login as Emma)**

Sign in as: `emma.lee@contoso.com`

### ✔ Allowed Actions

1. Go to **Microsoft Entra ID → Users**
2. Create a new user (e.g., `test.user@contoso.com`)
3. Reset a password
4. Add user to a group

### ❌ Denied Actions

Try to:

- Open **Subscriptions**
- Open **Resource groups**
- Create a VM
- Access Key Vault

Expected:  
`Access denied` — Emma has **no RBAC roles**.

---

## **4. Assign RBAC Role to Emma (Admin)**

Assign Emma **Reader** at the subscription scope.

**Azure Portal → Subscriptions → Access Control (IAM) → Add role assignment**

- **Role:** Reader  
- **Scope:** Subscription  
- **Principal:** `emma.lee@contoso.com`

### Expected Behavior

Emma can now:

- View all resource groups  
- View all resources  
- View VM details  
- View Key Vault (but not secrets)

Emma still **cannot**:

- Create resources  
- Modify resources  
- Read Key Vault secrets  
- Assign roles  

---

## **5. Compare Emma vs Alex (From Day 1)**

| User | Microsoft Entra ID Role | RBAC Role | What They Can Do |
|------|----------------|-----------|------------------|
| **Alex** | None | Contributor (RG) | Full control inside `rg-bootcamp` |
| **Emma** | User Administrator | Reader (Subscription) | Manage users, view resources only |

### Key Insight

- Microsoft Entra ID roles do **not** grant resource access  
- RBAC roles do **not** grant directory access  

They are **completely separate permission systems**.

---

## **6. Control Plane vs Data Plane (Hands‑On)**

### 🔹 Control Plane  
Managing Azure resources:

- Create VM  
- Delete RG  
- Assign RBAC  
- Modify networking  

Controlled by **Azure RBAC**.

### 🔹 Data Plane  
Accessing the data inside a resource:

- Reading a blob  
- Retrieving a Key Vault secret  
- Querying a database  

Controlled by **resource‑specific roles**, such as:

- Storage Blob Data Reader  
- Key Vault Secrets User  
- Cosmos DB Reader  

### Hands‑On Validation

1. Emma opens the Key Vault → **Allowed** (control plane: Reader)  
2. Emma tries to read a secret → **Denied** (data plane: no role)  
3. VM identity reads the secret → **Allowed** (Key Vault Secrets User)  
4. Alex (Contributor) tries to read the secret → **Denied** (Contributor ≠ data‑plane access)

This is exactly how Azure enforces **zero trust**.

---

## **7. Troubleshooting Scenarios**

### Scenario 1  
User can see a resource but cannot modify it.  
**Cause:** Reader role assigned  
**Fix:** Assign Contributor

---

### Scenario 2  
User can manage Key Vault but cannot read secrets.  
**Cause:** Missing data‑plane role  
**Fix:** Assign Key Vault Secrets User

---

### Scenario 3  
User can manage users but cannot access resources.  
**Cause:** Microsoft Entra ID role only  
**Fix:** Assign RBAC role

---

## **8. Clean Up (Optional)**

```bash
az role assignment delete --assignee emma.lee@contoso.com --role Reader
```

---

## 📌 **Day 3 Summary**

Today you learned:

- The difference between **Microsoft Entra ID roles** and **Azure RBAC roles**
- How directory roles affect identity management
- How RBAC roles affect resource access
- How scope inheritance works
- How control‑plane and data‑plane permissions differ
- Why least‑privilege requires both systems to be configured correctly

This knowledge is essential for real‑world cloud architecture and all three certifications.

---

## ▶️ Next Lab

**Day 4 — Azure Locks + Resource Policies**  
See: [04-locks-resource-policies.md](04-locks-resource-policies.md)

---

## 🔗 Related Labs

- [Day 1 — RBAC Basics](01-rbac-basics.md)
- [Day 2 — Managed Identity + Key Vault](02-managed-identity-keyvault.md)