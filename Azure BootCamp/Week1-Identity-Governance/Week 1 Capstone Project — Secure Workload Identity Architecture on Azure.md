# Week 1 Capstone Project — Secure Workload Identity Architecture on Azure
*Boot Camp: Identity, RBAC & Managed Identity — Week 1*

> This capstone consolidates all identity concepts from Week 1 into a single, real‑world architecture.  
> The goal is to build a secure, credential‑free identity flow where a VM‑based workload retrieves secrets and configuration files using Managed Identity, RBAC, Key Vault, and Storage.

---

# 1. Scenario Overview

A development team is deploying an application on a virtual machine.  
The application must:

- Retrieve a **database password** from Azure Key Vault  
- Read a **configuration file** from Azure Storage  
- Use **no secrets, no access keys, no connection strings**  
- Follow **least‑privilege RBAC**  
- Use **Managed Identity** for authentication  

Your task is to design and implement a **secure workload identity architecture** that meets these requirements.

This pattern is used across enterprise Azure environments and is a core AZ‑104 skill.

---

# 2. Architecture Diagram (Conceptual)

```
+-----------------------------+
| Azure AD                    |
|  - Admin Identity           |
|  - VM Managed Identity      |
+-----------------------------+
             |
             | Issues OAuth Tokens
             v
+-----------------------------+
| Virtual Machine (vm-bootcamp)
|  - System-assigned MI
+-----------------------------+
      |                     |
      | Auth via MI         | Auth via MI
      v                     v
+-------------+       +----------------+
| Key Vault   |       | Storage Account|
| Secrets     |       | Blob Container |
+-------------+       +----------------+
```

---

# 3. Capstone Objectives

By completing this capstone, you will:

### Identity & RBAC
- Configure Azure AD identities and RBAC roles  
- Apply least‑privilege access at resource and container scopes  

### Key Vault
- Deploy Key Vault in **RBAC mode**  
- Store and retrieve secrets using Managed Identity  

### Storage Account
- Deploy a Storage Account with a **private container**  
- Upload configuration files  
- Grant identity‑based blob access  

### Managed Identity
- Enable system‑assigned MI on a VM  
- Authenticate to Azure CLI using MI  
- Access Key Vault and Storage without credentials  

### Validation
- Validate access using:
  - Azure CLI (`--auth-mode login`)
  - REST API (OAuth token → Storage)  

### IaC (Day 7)
- Deploy the entire architecture using **Bicep**  

---

# 4. Deliverables (Portfolio-Ready)

Your final capstone submission includes:

### **A. Architecture Document**
- Overview  
- Identity flow  
- RBAC matrix  
- Security considerations  
- Diagram  

### **B. Hands-On Implementation**
- Key Vault (RBAC mode)  
- Storage Account (private container)  
- VM with system-assigned MI  
- Secret stored in Key Vault  
- Blob stored in Storage  
- RBAC assignments:
  - Key Vault Secrets Officer (admin)
  - Key Vault Secrets User (VM)
  - Storage Blob Data Reader (VM)

### **C. Validation Evidence**
- CLI output (secret retrieval)  
- CLI output (blob download)  
- REST API output (OAuth token → Storage)  

### **D. Day 7 Bicep Deployment**
A single Bicep deployment that creates:

- Key Vault  
- VM with MI  
- Storage Account  
- RBAC assignments  
- Container + sample blob (optional)

---

# 5. Step-by-Step Implementation

This capstone reuses validated steps from Days 1–3.

---

## Step 1 — Create Key Vault (Portal)

- RBAC mode  
- Soft delete + purge protection enabled  
- Add secret: `db-password`  

---

## Step 2 — Create Storage Account (Portal)

- Standard LRS  
- Private container: `app-data`  
- Upload blob: `config.json`  

---

## Step 3 — Enable VM Managed Identity

VM → Identity → System-assigned → **On**

---

## Step 4 — Assign RBAC Roles

| Resource | Role | Identity |
|----------|------|----------|
| Key Vault | Key Vault Secrets Officer | admin@contoso.com |
| Key Vault | Key Vault Secrets User | vm-bootcamp |
| Storage Account | Storage Blob Data Reader | vm-bootcamp |

---

## Step 5 — Validate Access from VM

### Login using MI
```bash
az login --identity --allow-no-subscriptions
```

### Retrieve secret
```bash
az keyvault secret show \
  --vault-name kv-bootcamp \
  --name db-password
```

### Download blob
```bash
az storage blob download \
  --account-name stidentitylab01 \
  --container-name app-data \
  --name config.json \
  --file downloaded.json \
  --auth-mode login
```

### REST API validation
```bash
TOKEN=$(curl -H "Metadata: true" \
  "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://storage.azure.com/" \
  | jq -r '.access_token')

curl -H "Authorization: Bearer $TOKEN" \
     -H "x-ms-version: 2021-08-06" \
     "https://stidentitylab01.blob.core.windows.net/app-data/config.json"
```

---

# 6. Validation Checklist

You have completed the Week 1 Capstone when:

✔ VM retrieves Key Vault secret using MI  
✔ VM downloads blob using MI  
✔ REST API call succeeds with OAuth token  
✔ No keys, SAS tokens, or connection strings used  
✔ RBAC assignments follow least privilege  
✔ Architecture diagram created  
✔ Bicep deployment completed  
✔ Documentation added to portfolio  

---

# 7. Security Considerations

- No secrets stored on VM  
- No access keys used  
- RBAC-only access  
- Managed Identity lifecycle managed by Azure  
- Key Vault protected by RBAC + soft delete  
- Storage Account protected by RBAC (no public access)  
- Identity-based access is fully auditable  

---

# 8. Final Deliverable Summary

Your Week 1 Capstone includes:

- **Architecture diagram**  
- **Identity flow explanation**  
- **RBAC matrix**  
- **Portal configuration steps**  
- **CLI validation**  
- **REST API validation**  
- **Bicep deployment (Day 7)**  