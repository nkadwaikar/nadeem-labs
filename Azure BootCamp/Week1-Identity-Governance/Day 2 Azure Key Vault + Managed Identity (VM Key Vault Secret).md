# Day 2 — Azure Key Vault + Managed Identity (VM → Key Vault Secret)

> This lab continues from **Day 1**, using the same VM (`vm-identity-lab`) and Resource Group (`rg-identity-lab`).  
> All user accounts use the placeholder domain `@contoso.com` to avoid exposing my real Azure AD tenant domain.  
> Steps requiring IAM changes must be performed by a Global Administrator or User Access Administrator.

---

## Chapters to Read
- **Chapter 10 — Secure Azure Resources with Azure Key Vault**  
- **Chapter 11 — Implement Managed Identities**

---

## Learning Objectives
- Deploy Azure Key Vault using RBAC authorization  
- Create and manage secrets  
- Assign Key Vault RBAC roles to a Managed Identity  
- Authenticate to Key Vault from a VM **without secrets**  
- Validate least‑privilege behavior  
- Troubleshoot Key Vault access issues  

---

# Lab Steps

---

## 1. Create Key Vault (Admin)

### Configuration
- **Name:** `kv-identity-lab`  
- **Resource Group:** `rg-identity-lab`  
- **Region:** Same as VM  
- **SKU:** Standard  
- **Soft Delete:** Enabled  
- **Purge Protection:** Optional  
- **Access Model:** **RBAC** (not Access Policies)

### Portal Steps
1. Go to **Azure Portal**
2. Search for **Key Vaults**
3. Select **Create**
4. Fill in:
   - Resource Group: `rg-identity-lab`
   - Key Vault Name: `kv-identity-lab`
   - Region: Same as VM
   - Pricing Tier: Standard
5. Under **Access Configuration**, select:
   - **Permission Model:** Azure RBAC
6. Click **Review + Create → Create**

---

## 🔍 Key Vault Access Models — RBAC vs Access Policies

| Feature | RBAC | Access Policies |
|--------|------|-----------------|
| Authorization Layer | Azure AD | Key Vault internal |
| Granularity | High (role‑based) | Medium (permission‑based) |
| Recommended | ✔ Yes | ✘ Legacy |
| IAM Integration | Full | None |
| Supports PIM | Yes | No |
| Supports Deny Assignments | Yes | No |
| Applies To | Management + Data plane | Data plane only |

---

## 2. Add a Secret to Key Vault

1. Open **kv-identity-lab**
2. Left menu → **Secrets**
3. Click **Generate/Import**
4. Configure:
   - **Name:** `db-password`
   - **Value:** `P@ssw0rd123!`
5. Click **Create**

---

## 3. Assign Key Vault RBAC Role to the VM’s Managed Identity

### Portal Steps
1. Open **kv-identity-lab**
2. Left menu → **Access Control (IAM)**
3. Click **Add → Add role assignment**
4. Select:
   - **Role:** Key Vault Secrets User
   - **Scope:** Key Vault
   - **Assign access to:** Managed Identity
5. Select:
   - **Identity type:** Virtual Machine
   - **Name:** `vm-identity-lab`
6. Click **Save**

### Expected Behavior
- VM can **read** secrets  
- VM cannot **write**, **delete**, or **list** all secrets  
- Alex (Contributor) cannot read secrets  
- Only admins can modify IAM  

---

## 4. Connect to the VM

```bash
ssh -i <path-to-private-key> azureuser@<public-ip>