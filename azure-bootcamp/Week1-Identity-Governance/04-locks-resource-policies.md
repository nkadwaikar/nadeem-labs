<!-- filepath: vscode-vfs://github/nkadwaikar/nadeem-labs/azure-bootcamp/Week1-Identity-Governance/04-locks-resource-policies.md -->
# **Day 4 — Azure Locks + Resource Policies (Hands-On Lab)**  
### *Protect resources from accidental deletion and enforce governance at scale.*

> This lab builds on Days 1–3 and introduces two major governance controls:  
> **Resource Locks** (Delete/Read-only) and **Azure Policy** (compliance enforcement).  
> These are essential for real-world cloud governance and AZ-104/AZ-500/AZ-305.

---

## 📚 Chapters to Read
- **Chapter 8 — Azure Resource Locks**  
- **Chapter 9 — Azure Policy & Compliance**  

---

## 🎯 Learning Objectives

By the end of this lab, you will:

- Apply **Delete** and **Read-only** locks at different scopes  
- Understand lock inheritance  
- Test how locks affect RBAC permissions  
- Deploy and assign Azure Policies  
- Validate compliance and remediation  
- Understand how governance interacts with identity and RBAC  

---

# 🧪 Lab Steps

---

## **1. Create a Test Resource Group**

If you already have `rg-bootcamp`, you can reuse it.  
Otherwise:

**Azure Portal → Resource groups → Create**

- **Name:** `rg-locks-demo`  
- **Region:** your preferred region  

---

## **2. Apply a Delete Lock at Resource Group Scope**

**Azure Portal → Resource groups → rg-locks-demo → Settings → Locks → Add**

- **Lock name:** `rg-delete-lock`  
- **Lock type:** Delete  
- **Notes:** Prevent accidental deletion  

Click **OK** to apply.

### ✔ Expected Behavior

- You **cannot delete** the resource group  
- You **cannot delete** any resource inside it  
- You **can still modify** resources  

This is the most common lock used in production.

---

## **3. Test the Delete Lock**

Try to delete the resource group:

**Resource group → Overview → Delete resource group**

Expected:

> "Cannot delete resource group because a lock is in place."

Try to delete a resource inside the RG (e.g., a VM or storage account).

Expected:

> "Cannot delete resource because a lock is in place."

---

## **4. Apply a Read-Only Lock at Resource Scope**

Pick any resource inside the RG (e.g., a storage account).

**Storage account → Settings → Locks → Add**

- **Lock name:** `sa-readonly-lock`  
- **Lock type:** Read-only  

Click **OK** to apply.

### ✔ Expected Behavior

- You **cannot modify** the resource  
- You **cannot delete** the resource  
- You **can view** all settings  
- You **can read** data (if RBAC allows it)  

---

## **5. Test the Read-Only Lock**

Try to:

- Change configuration  
- Add tags  
- Modify networking  
- Update access keys  
- Change SKU  

Expected:

> "The resource is locked and cannot be modified."

---

## **6. Remove the Read-Only Lock**

**Storage account → Settings → Locks → Select the lock → Delete**

Confirm deletion.

This restores normal behavior.

---

# **Azure Policy Section**

Now let's enforce governance at scale.

---

## **7. Assign a Built-In Azure Policy**

We'll use a simple, common policy:

**"Require tags on resource groups"**

**Azure Portal → Policy → Definitions → Search: "Require tag"**

Choose:

- **Policy:** *Require a tag on resource groups*  

**Click Assign:**

- **Scope:** Select your subscription  
- **Basics:**
  - **Assignment name:** `require-environment-tag`
  - **Description:** Enforce environment tag on all RGs
- **Parameters:**
  - **Tag name:** `environment`  
- **Remediation:** Leave as default
- **Review + create** → **Create**

---

## **8. Test the Policy**

Try to create a new resource group **without** the `environment` tag.

**Resource groups → Create:**
- **Name:** `rg-test-noncompliant`
- **Region:** your region
- **Tags:** (leave empty)
- Click **Review + create**

Expected:

> "Resource group creation failed due to policy violation."

Now try again **with** the tag:

**Resource groups → Create:**
- **Name:** `rg-test-compliant`
- **Region:** your region
- **Tags:** `environment = dev`
- Click **Review + create** → **Create**

Expected:

✔ Resource group creation succeeds.

---

## **9. View Compliance**

**Azure Portal → Policy → Compliance**

Find your assignment: `require-environment-tag`

- It should show **non-compliant** for any RG missing the tag  
- It should show **compliant** for RGs with the tag  

Note: Compliance scan may take 5-10 minutes to update.

---

## **10. Optional: Deploy a Deny Policy for SKUs**

Assign:

**"Allowed virtual machine SKUs"**

**Azure Portal → Policy → Definitions → Search: "Allowed virtual machine SKUs"**

**Click Assign:**

- **Scope:** Select your subscription or resource group
- **Parameters:**
  - **Allowed SKUs:** Select:
    - `Standard_B2s`  
    - `Standard_D2s_v3`
- **Review + create** → **Create**

Try to deploy a VM with a different SKU (e.g., `Standard_D4s_v3`).

Expected:

> "The resource is disallowed by policy."

This is how enterprises enforce cost control and standardization.

---

# 🧩 Governance + Identity Interaction (Important)

### ✔ Locks override RBAC  
Even **Owner** cannot delete a locked resource.

### ✔ Policies override RBAC  
Even **Contributor** cannot deploy non-compliant resources.

### ✔ Directory roles do not affect locks or policies  
Emma (User Administrator) cannot bypass:

- Locks  
- Policies  
- RBAC  

### ✔ RBAC controls *who* can act  
Policies and locks control *what* is allowed.

This is the foundation of Azure governance.

---

# 🧹 **Cleanup (Optional)**

To remove resources created in this lab:

1. **Remove locks first:**
   - Navigate to each locked resource
   - Delete all locks

2. **Remove policy assignments:**
   - **Policy → Assignments → Select assignment → Delete**

3. **Delete test resources:**
   - Delete `rg-test-compliant` (if created)
   - Delete `rg-locks-demo` (if not needed)

---

# 📌 **Day 4 Summary**

Today you learned:

- How to apply **Delete** and **Read-only** locks  
- How lock inheritance works  
- How locks interact with RBAC  
- How to assign Azure Policies  
- How to enforce tagging, SKU restrictions, and compliance  
- How governance controls override RBAC permissions  
- How identity, RBAC, locks, and policy form a complete governance model  

This is essential knowledge for real-world Azure environments and all three certifications.

---

## ▶️ Next Lab

**Day 5 — Access Validation & Identity Troubleshooting**  
`05-access-validation.md`

---