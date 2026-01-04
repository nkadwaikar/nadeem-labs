# 🏗️ Week 1 Capstone — Identity-First, Governance-Ready Landing Zone  
*Zero secrets. Zero trust. Fully governed. Fully observable. Fully IaC.*

> **📌 Status: Complete (Validation Evidence Deferred)**  
> Week 1 establishes a secure, identity-driven foundation using modern Azure governance and IaC patterns.  
> All deployments were executed **entirely from VS Code**, without Azure CLI or Portal.

---

## 🎯 Project Overview

This capstone delivers a **minimal, enterprise-aligned landing zone** built entirely with Bicep and deployed through Visual Studio Code.  
The design follows an **identity-first** approach where all access flows through Managed Identity and RBAC — no secrets, no connection strings, no manual steps.

### Core capabilities implemented:

- **User Assigned Managed Identity (UAMI)**  
- **Azure Key Vault (RBAC-mode)**  
- **Role-Based Access Control (RBAC)**  
- **Resource Locks (CanNotDelete)**  
- **Azure Policy (baseline governance)**  
- **Azure Monitor + Activity Logs**  
- **Log Analytics + KQL queries (optional)**  
- **Modular Bicep (IaC)**  
- **VS Code-only deployment workflow**

This reflects real-world cloud security patterns used across NZ/AU enterprise environments and aligns with hiring expectations for senior cloud architects.

---

## 🧭 Architecture Diagram (Week 1)

Below is the conceptual architecture for the Week 1 identity-first landing zone.

```plaintext
                   ┌──────────────────────────────┐
                   │      Subscription Scope       │
                   │  (create-rg.bicep deployed)   │
                   └───────────────┬──────────────┘
                                   │
                                   ▼
                     ┌────────────────────────┐
                     │   Resource Group        │
                     │   rg-identity-lab       │
                     └───────────┬────────────┘
                                 │
     ┌───────────────────────────┼───────────────────────────┐
     ▼                           ▼                           ▼
┌──────────────┐        ┌────────────────┐          ┌────────────────┐
│  Managed      │        │   Key Vault    │          │ Resource Lock  │
│  Identity     │        │   wk1-kv       │          │  wk1-lock      │
│  wk1-uami     │        │ (RBAC Mode)    │          │ CanNotDelete   │
└──────┬────────┘        └───────┬────────┘          └────────────────┘
       │                          │
       │  principalId             │  kvId
       │                          │
       └──────────────┬───────────┘
                      ▼
            ┌──────────────────────┐
            │        RBAC          │
            │ Key Vault Secrets    │
            │ User Assignment       │
            └──────────────────────┘
```

---

## 🔗 Supporting Documentation & Diagrams

These files live in `capstone/docs/`:

- 📘 [VS Code Deployment Workflow](docs/vscode-deployment-workflow.md)  
- 🔐 [Identity-First Access Flow](docs/identity-first-access-flow.md)  
- 🛡️ [Governance Flow Diagram](docs/governance-flow.md)  
- 📝 [Lessons Learned](docs/week1-lessons-learned.md)

---

## 📂 Repository Structure (Week 1)

```plaintext
capstone/
├── bicep/                      # Subscription + RG-level deployments
│   ├── main.bicep
│   ├── create-rg.bicep
│   └── modules/
│       ├── identity.bicep
│       ├── keyvault.bicep
│       ├── rbac.bicep
│       └── locks.bicep
│
├── docs/                       # Architecture notes, workflows, lessons
│   ├── governance-flow.md
│   ├── identity-first-access-flow.md
│   ├── vscode-deployment-workflow.md
│   └── week1-lessons-learned.md
│
└── week1-capstone.md           # This file
```

---

## 🧩 What This Capstone Demonstrates

**✔ Identity-first access**  
All workloads authenticate using Managed Identity — no secrets, no keys.

**✔ Governance from Day 1**  
Policies, RBAC, and locks ensure safe, compliant deployments.

**✔ Observability baked in**  
Activity logs and optional diagnostics provide visibility.

**✔ Modular, production-ready IaC**  
Bicep modules reflect real enterprise patterns and reusable architecture.

**✔ VS Code-only workflow**  
No CLI. No Portal. Everything deployed through the Azure extension ecosystem.

---

## 🧪 Validation Status (Week 1)

Formal validation evidence (screenshots, KQL output, etc.) is **deferred** for Week 1.  
The environment has been validated manually through VS Code Azure Explorer.

A full validation folder will be added in Week 2+.

---

## 📝 Lessons Learned

A full reflection on Week 1 is available here:

📄 [Week 1 Lessons Learned](docs/week1-lessons-learned.md)

---

## ▶️ Next Capstone (Week 2)

**Week 2 — Secure Hub-Spoke Network Architecture**  
Includes:

- Virtual Networks  
- Subnets  
- NSGs  
- Private Endpoints  
- Private DNS Zones  
- Identity-first access to PaaS services  
- Modular Bicep + VS Code deployment

---

## 🎉 Summary

Week 1 establishes the foundation for all future capstones with:

- Secure identity-first architecture
- Enterprise-grade governance controls
- Modular, reusable IaC patterns
- Professional documentation and diagrams
- VS Code-centric deployment workflow