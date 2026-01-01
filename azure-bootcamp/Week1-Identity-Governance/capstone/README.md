# 🏗️ Capstone — Identity‑First Secure Workload Architecture  
### *Zero secrets. Zero trust. Enterprise‑grade identity design.*

> **📌 Portfolio Status:** Work in Progress | Last Updated: December 2025

This capstone demonstrates how to build a **secure, identity‑driven workload** in Azure using:

- Managed Identity  
- Azure Key Vault  
- Azure Storage  
- RBAC (Role‑Based Access Control)  
- Bicep (Infrastructure as Code)  
- Identity governance best practices  

This architecture reflects modern cloud security patterns used across enterprise environments.

---

## 🎯 Objectives

By completing this capstone, you will:

- Deploy a VM with a **system‑assigned Managed Identity**
- Securely access **Key Vault** and **Storage** without secrets
- Implement **least‑privilege RBAC** at correct scopes
- Enforce **zero‑trust identity patterns**
- Deploy the entire environment using **modular Bicep**
- Validate identity flows using **CLI + REST API**
- Document design decisions like an Azure Architect

This capstone directly supports **AZ‑104, AZ‑305, and AZ‑500** certification skills.

---

## 🧱 Architecture Overview

The workload uses identity‑based authentication end‑to‑end:

```
VM (Managed Identity)
        │
        ▼
Azure AD → Issues OAuth token
        │
        ├── Key Vault (Secrets)
        └── Storage Account (Blob)
```

No secrets. No connection strings. No SAS tokens.

---

## 📂 Repository Structure

```
capstone/
├── README.md
├── architecture/                          🚧 Work in Progress
│   ├── identity-architecture.drawio
│   └── identity-architecture.png
├── bicep/                                 🚧 Work in Progress
│   ├── main.bicep
│   └── modules/
│       ├── vm.bicep
│       ├── keyvault.bicep
│       ├── storage.bicep
│       └── identity.bicep
├── validation/                            🚧 Work in Progress
│   ├── cli-validation.md
│   ├── portal-validation.md
│   └── troubleshooting.md
└── docs/                                  🚧 Work in Progress
    └── security-controls.md
```

Each folder is designed for clarity, auditability, and professional presentation.

---

## 🚀 Deployment Workflow

### **1. Deploy Core Resources (Bicep)** 🚧 Work in Progress
- Resource group  
- Virtual machine  
- Managed identity  
- Key Vault (RBAC mode)  
- Storage account  

### **2. Assign RBAC Roles**  
- VM → Key Vault Secrets User  
- VM → Storage Blob Data Reader  

### **3. Upload Test Data**  
- `app-secret` → Key Vault  
- `settings.json` → Storage  

### **4. Validate Identity Flows** 🚧 Work in Progress
- `az login --identity`  
- Retrieve Key Vault secret  
- Download blob using OAuth token  

---

## 🔍 Validation Steps

> **🚧 Work in Progress** - Validation scripts coming soon

Validation scripts will be located in:

```
validation/cli-validation.md
validation/portal-validation.md
validation/troubleshooting.md
```

Will include:

- Token inspection  
- RBAC verification  
- Access tests  
- Error simulation  
- Troubleshooting patterns  

---

## 🔐 Security Controls

> **🚧 Work in Progress** - Security documentation coming soon

Will be documented in:

```
docs/security-controls.md
```

Will include:

- Zero Trust alignment  
- RBAC least privilege  
- Key Vault hardening  
- Storage network restrictions  
- Identity lifecycle considerations  

---

## 🧠 Why This Capstone Matters

This project demonstrates the **core identity patterns** used in modern cloud environments:

- Identity‑based authentication  
- Secretless workloads  
- RBAC governance  
- Modular IaC  
- Secure workload design  

It proves you understand:

- Identity  
- Security  
- Governance  
- IaC  
- Architecture  

This is a foundational project for a strong Azure portfolio.

---

## 📌 Completion Checklist

Progress tracking:

- 🚧 VM identity is enabled  
- 🚧 Key Vault is deployed in RBAC mode  
- 🚧 Storage account is deployed  
- 🚧 RBAC roles are assigned correctly  
- 🚧 VM retrieves Key Vault secret  
- 🚧 VM reads blob data using OAuth  
- 🚧 No secrets or keys were used  
- 🚧 Bicep deployment is modular and reusable  
- 🚧 Architecture diagram is included  

**Legend:** ✅ Complete | 🚧 In Progress | ⏳ Planned

---

## 🎯 Project Roadmap

### Phase 1: Foundation (Current)
- 🚧 Define architecture
- 🚧 Create Bicep modules
- ⏳ Deploy core resources

### Phase 2: Security & Validation
- ⏳ Implement RBAC
- ⏳ Create validation scripts
- ⏳ Document security controls

### Phase 3: Documentation
- ⏳ Architecture diagrams
- ⏳ Troubleshooting guides
- ⏳ Final polish

---

## ▶️ Next Capstone

**Capstone 2 — Secure Hub‑Spoke Network Architecture** ⏳ Planned  
(Week 2 Networking & Security)
