# 🏁 Final Project — The Secure Customer Portal (Enterprise Edition)  
### *A complete, end‑to‑end scenario combining AZ‑104, AZ‑500, AZ‑305, and Landing Zone engineering.*

This final project transforms a simple "App + SQL" deployment into a **secure, resilient, globally distributed, cost‑optimized, monitored, and governed** production architecture.

It mirrors the exact thinking expected from:

- Azure Administrators (AZ‑104)  
- Security Engineers (AZ‑500)  
- Solutions Architects (AZ‑305)  
- Cloud Platform Engineers (Landing Zones)  

You will progress through four maturity stages:

1. **Build it** (Administrator)  
2. **Protect it** (Security Engineer)  
3. **Design it right** (Solutions Architect)  
4. **Operate it** (Platform Engineer)  

---

## 🎯 Scenario Overview — "The Secure Customer Portal"

A client wants to deploy a **public‑facing web application** backed by an **Azure SQL Database**.  
The initial build works — but it is **not secure**, **not resilient**, and **not architected for global performance**.

Your mission is to transform it into a production‑ready platform.

---

## 🧩 Phase 1 — The Foundation (AZ‑104 Skills)  
### *"Can I build it?"*

### **Tasks**
Deploy the following:

- Azure App Service  
- Azure SQL Database  
- App Service connection string  
- Basic networking  

### **Expected Result**
The app runs and connects to SQL.

### **Intentional Weaknesses**
This environment is *not* production‑ready:

- SQL has a **public endpoint**  
- Secrets stored in App Service config  
- No identity integration  
- No network isolation  
- No monitoring  

These weaknesses become the foundation for the next phases.

---

## 🛡️ Phase 2 — The Security Challenge (AZ‑500 Skills)  
### *"Can I protect it?"*  
### *Zero Trust + Defense in Depth*

### 🔐 Challenge 1 — Remove Public Access
- Disable public network access on SQL  
- Create a **Private Endpoint**  
- Integrate App Service with VNet  
- Validate connectivity using logs or `tcpping`  

**Outcome:**  
Only the App Service can reach SQL.

---

### 🔑 Challenge 2 — Secret Management
- Create Azure Key Vault  
- Store SQL credentials or connection string  
- Remove secrets from App Service configuration  

**Outcome:**  
No plaintext secrets anywhere.

---

### 🆔 Challenge 3 — Identity Integration
- Enable **System‑Assigned Managed Identity** on App Service
- Grant **Key Vault Secrets User** role to the managed identity
- Update app to retrieve secrets at runtime using Azure SDK

**Outcome:**  
Passwordless, identity‑based access.

---

### 🛡️ Challenge 4 — Add a Web Application Firewall (WAF)
Choose one:

- **Azure Front Door Premium with WAF** (recommended for global reach)  
- **Application Gateway with WAF** (for regional deployments)

Configure:

- OWASP Core Rule Set  
- Bot protection  
- Geo‑filtering  
- Rate limiting  

**Outcome:**  
Layer‑7 protection for the public‑facing app.

---

### 🚨 Challenge 5 — Defender for Cloud Alert Simulation
Trigger a safe alert using:

- Defender's built‑in test alert feature  
- A temporary misconfiguration (e.g., open storage account)  
- EICAR test file upload

Then:

- Investigate in Microsoft Defender for Cloud  
- Review recommendations and Secure Score impact  
- Document remediation steps  

**Outcome:**  
Hands‑on **security operations**, not just configuration.

---

## 🧠 Phase 3 — The Design Challenge (AZ‑305 Skills)  
### *"Is it the right way to build it?"*  
### *Resiliency + Global Performance + Cost Optimization*

### 🌍 Challenge 1 — High Availability & Failover
Design for regional failure:

- Configure SQL **Auto‑Failover Groups** with secondary region
- Deploy secondary region App Service  
- Configure Front Door with failover routing policies
- Plan DNS and connection string strategies

**Outcome:**  
A multi‑region, resilient architecture with automated failover.

---

### 🌐 Challenge 2 — Global Traffic Optimization
Users are located in:

- London  
- New York  

Choose between:

- **Azure Front Door** → global routing, edge caching, integrated WAF  
- **Application Gateway** → regional load balancing

**Expected Answer:**  
Front Door for global performance optimization + automatic failover.

---

### 💰 Challenge 3 — Cost vs Performance
Evaluate trade-offs:

- DTU vs vCore pricing models  
- Compute tiers (Basic, Standard, Premium)  
- Storage redundancy (LRS, ZRS, GRS)  
- Failover region costs  
- Front Door caching to reduce backend load  
- Reserved Instances / Savings Plans for long-term commitments

**Outcome:**  
Architecture decisions backed by **business requirements and budget constraints**.

---

### ⚡ Challenge 4 — Add a Caching Layer (Redis)
Implement:

- Azure Cache for Redis (Standard or Premium tier)  
- Cache‑aside pattern in application code  
- Reduced SQL database load  
- Improved response latency  
- Cache invalidation strategy

**Outcome:**  
Performance engineering with measurable improvements.

---

## 🧪 Phase 4 — Operational Excellence (Platform Engineering)  
### *"Can I operate it in production?"*

### 📊 Challenge 1 — Monitoring Baseline
Deploy comprehensive monitoring:

- Application Insights for application telemetry  
- Azure SQL Insights for database performance  
- Log Analytics workspace as central repository  
- Enable diagnostic settings for:
  - App Service (HTTP logs, metrics)  
  - SQL Database (query performance, blocks)  
  - Key Vault (access audit)  
  - Private Endpoints (connectivity)  
  - Front Door/WAF (security events)  

Create actionable alerts for:

- CPU > 80%  
- DTU > 90%  
- HTTP 500 errors  
- Failover events  
- Key Vault access denied  
- WAF block events

**Outcome:**  
A fully observable system with proactive alerting.

---

### 🏛️ Challenge 2 — Governance Enforcement
Use Azure Policy to enforce organizational standards:

- Require private endpoints for PaaS services  
- Enforce Key Vault firewall rules  
- Mandate HTTPS only for web apps  
- Require TLS 1.2+ for all services  
- Enforce diagnostic settings on all resources  
- Deny SQL public network access  
- Require specific resource tags

**Outcome:**  
Governance at scale through policy‑driven compliance.

---

### 🔄 Challenge 3 — Optional CI/CD (DevOps Excellence)
Implement infrastructure as code and automated deployments:

- Use GitHub Actions or Azure DevOps Pipelines  
- Deploy infrastructure using Bicep or Terraform  
- Automate deployment of:
  - App Service with configuration  
  - SQL Database with schemas  
  - Key Vault with secrets  
  - Private Endpoints  
  - Policy assignments  

**Outcome:**  
Repeatable, version-controlled infrastructure deployments.

---

## 📐 Final Architecture (Conceptual)

```
                    Internet Users
                          │
                          ▼
            ┌─────────────────────────┐
            │   Azure Front Door      │
            │   (WAF + Global CDN)    │
            └─────────────────────────┘
                          │
              ┌───────────┴───────────┐
              ▼                       ▼
      ┌───────────────┐       ┌───────────────┐
      │  App Service  │       │  App Service  │
      │  (Primary)    │       │  (Secondary)  │
      │  VNet Int.    │       │  VNet Int.    │
      └───────────────┘       └───────────────┘
              │                       │
              ▼                       ▼
      ┌───────────────┐       ┌───────────────┐
      │Private Endpt  │       │Private Endpt  │
      └───────────────┘       └───────────────┘
              │                       │
              ▼                       ▼
      ┌───────────────┐       ┌───────────────┐
      │  Azure SQL    │◄─────►│  Azure SQL    │
      │  (Primary)    │  Auto │  (Secondary)  │
      │               │Failover│               │
      └───────────────┘  Group └───────────────┘
              │
              ▼
      ┌───────────────┐
      │  Azure Cache  │
      │  for Redis    │
      └───────────────┘
```

**Supporting Services:**

- Azure Key Vault (secrets management)  
- Azure Monitor + Log Analytics (observability)  
- Microsoft Defender for Cloud (security posture)  
- Microsoft Sentinel (SIEM, optional)  
- Azure Policy (governance)  
- Management Groups (organizational hierarchy)  

This represents a **complete enterprise-grade architecture**.

---

## 📂 Folder Structure

```
Final-Project-Secure-Customer-Portal/
├── README.md
├── phase1-foundation/
│   ├── deploy.md
│   └── scripts/
├── phase2-security/
│   ├── private-endpoints.md
│   ├── key-vault.md
│   └── waf-config.md
├── phase3-architecture/
│   ├── ha-design.md
│   ├── redis-implementation.md
│   └── cost-analysis.xlsx
├── phase4-operations/
│   ├── monitoring-setup.md
│   ├── policy-definitions/
│   └── cicd-pipeline.yml
├── diagrams/
│   └── architecture.drawio
├── bicep/
│   ├── main.bicep
│   └── modules/
└── validation-checklist.md
```

---

## 📋 Success Criteria

**Phase 1:** Application is deployed and functional  
**Phase 2:** Zero Trust principles implemented, no public endpoints  
**Phase 3:** Multi-region resilience with optimized performance  
**Phase 4:** Full observability and governance enforcement  

---

## 🎓 Skills Demonstrated

Upon completion, you will have demonstrated:

- Infrastructure deployment (AZ-104)  
- Network security and identity management (AZ-500)  
- High availability and performance optimization (AZ-305)  
- Operational excellence and governance (Cloud Platform Engineering)  

This project serves as a comprehensive capstone for Azure certification preparation and real-world cloud architecture experience.