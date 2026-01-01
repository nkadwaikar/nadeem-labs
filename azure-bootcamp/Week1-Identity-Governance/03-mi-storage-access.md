This lab focuses on **Azure AD roles vs RBAC roles**, **scope boundaries**, and **how identity permissions differ between control‑plane and data‑plane operations** — a critical concept for AZ‑104, AZ‑305, and AZ‑500.

# Day 3 — Azure AD Roles + RBAC Scopes (Control Plane vs Data Plane)

> This lab builds on Day 1 and Day 2.  
> All user accounts use the placeholder domain `@contoso.com` to avoid exposing my real Azure AD tenant domain.  
> Steps requiring IAM changes must be performed by an administrator with elevated privileges.

---

## 📚 Chapters to Read
- **Chapter 5 — Manage Azure AD Roles**  
- **Chapter 6 — Understand RBAC Scopes**  
- **Chapter 7 — Control Plane vs Data Plane Permissions**

---

## 🎯 Learning Objectives

By the end of this lab, you will:

- Understand the difference between **Azure AD roles** and **Azure RBAC roles**
- Understand **control‑plane** vs **data‑plane** authorization
- Assign Azure AD directory roles to a user
- Assign RBAC roles at different scopes
- Validate how permissions differ across scopes
- Observe real‑world least‑privilege behavior

This is one of the most important identity concepts in Azure.

---

# 🧪 Lab Steps

---

## 1. Identity Concepts Overview

Azure has **two separate permission systems**:

---

### 🔹 **Azure AD Roles (Directory Roles)**  
These control **identity management**:

- User management  
- Group management  
- App registrations  
- Enterprise apps  
- Conditional Access  
- MFA settings  

Examples:

- Global Administrator  
- User Administrator  
- Security Administrator  
- Application Administrator  

**Scope:** Tenant-wide (directory level)  
**Not inherited** into subscriptions or resources.

---

### 🔹 **Azure RBAC Roles (Resource Roles)**  
These control **Azure resource access**:

- VMs  
- Storage  
- Key Vault  
- Networking  
- Resource groups  
- Subscriptions  

Examples:

- Owner  
- Contributor  
- Reader  
- Storage Blob Data Reader  
- Key Vault Secrets User  

**Scope:** Subscription → Resource Group → Resource  
**Inherited downward**.

---

## 2. Create a Second Test User (Admin)

This user will be used to test Azure AD roles.

- **User principal name:** `emma.lee@contoso.com`  
- **Display name:** Emma Lee  
- **Role:** No admin roles  

---

## 3. Assign an Azure AD Role (Directory Role)

Assign Emma the **User Administrator** role.

Azure Portal →  
**Azure Active Directory → Roles and administrators → User Administrator**

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

## 4. Validate Azure AD Role Permissions (Login as Emma)

Sign in as: `emma.lee@contoso.com`

### Validate Allowed Actions

1. Go to **Azure Active Directory → Users**
2. Create a new user (e.g., `test.user@contoso.com`)
3. Reset a password
4. Add user to a group

### Validate Denied Actions

Try to:

- Open **Subscriptions**
- Open **Resource groups**
- Create a VM
- Access Key Vault

Expected:  
`Access denied` — Emma has **no RBAC roles**.

---

## 5. Assign RBAC Role to Emma (Admin)

Assign Emma **Reader** at the subscription scope.

Azure Portal →  
**Subscriptions → Access Control (IAM) → Add role assignment**

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

## 6. Compare Emma vs Alex (From Day 1)

| User | Azure AD Role | RBAC Role | What They Can Do |
|------|----------------|-----------|------------------|
| **Alex** | None | Contributor (RG) | Full control inside `rg-bootcamp` |
| **Emma** | User Administrator | Reader (Subscription) | Manage users, view resources only |

### Key Insight

- Azure AD roles do **not** grant resource access  
- RBAC roles do **not** grant directory access  

They are **completely separate permission systems**.

---

## 7. Control Plane vs Data Plane (Key Concept)

### 🔹 Control Plane  
Managing Azure resources:

- Create VM  
- Delete RG  
- Assign RBAC  
- Modify networking  

Controlled by **Azure RBAC**.

---

### 🔹 Data Plane  
Accessing the data inside a resource:

- Reading a blob  
- Retrieving a Key Vault secret  
- Querying a database  

Controlled by **resource‑specific roles**, such as:

- Storage Blob Data Reader  
- Key Vault Secrets User  
- Cosmos DB Reader  

### Example

Emma (Reader) can **see** the Key Vault but **cannot** read secrets.  
Alex (Contributor) can **manage** the Key Vault but **cannot** read secrets.  
VM identity (Key Vault Secrets User) **can** read secrets.

This is intentional and secure.

---

## 8. Troubleshooting Scenarios

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
**Cause:** Azure AD role only  
**Fix:** Assign RBAC role

---

## 9. Clean Up (Optional)

```bash
az role assignment delete --assignee emma.lee@contoso.com --role Reader
```

---

## 📌 Day 3 Summary

Today you learned:

- The difference between **Azure AD roles** and **Azure RBAC roles**
- How directory roles affect identity management
- How RBAC roles affect resource access
- How scope inheritance works
- How control‑plane and data‑plane permissions differ
- Why least‑privilege requires both systems to be configured correctly

This knowledge is essential for real‑world cloud architecture and all three certifications.

---

## ▶️ Next Lab

**Day 4 — Azure Locks + Resource Policies**  
`04-locks-resource-policies.md`
```