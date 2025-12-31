# 🧭 **Azure Boot Camp — Full Multi‑Week Roadmap (Aligned to AZ‑104)**  
### *Identity → Networking → Compute → Storage → Monitoring → Backup → IaC (Bicep)*

---

# 📘 **Week 1 — Identity, RBAC, Managed Identity**  
### *Identity-first, portal-first, hands-on.*

**Hands‑on Labs:**
- Day 1 — Azure AD + RBAC Fundamentals  
- Day 2 — Key Vault + Admin Identity + VM Managed Identity  
- Day 3 — Managed Identity → Storage (Blob Read Access)  
- Day 4 — RBAC Scopes Deep Dive (Resource, RG, Subscription)  
- Day 5 — Azure AD Basics (Users, Groups, Roles)  
- Day 6 — Access Control Validation (CLI + Portal)  
- **Day 7 — Bicep: Key Vault + VM Managed Identity + RBAC Assignments**  
  - Deploy Key Vault (RBAC mode)  
  - Deploy VM with system-assigned MI  
  - Assign RBAC roles (Secrets Officer, Secrets User, Blob Data Reader)  

**Mapped AZ‑104 Chapters:**  
1, 2, 3, 10, 11

---

# 📗 **Week 2 — Networking & Security Foundations**  
### *VNets, NSGs, routing, private endpoints.*

**Hands‑on Labs:**
- Day 1 — VNets, Subnets, IP addressing  
- Day 2 — NSGs + Application Security Groups  
- Day 3 — Azure Firewall + Route Tables  
- Day 4 — Private Endpoints (Key Vault + Storage)  
- Day 5 — Service Endpoints vs Private Endpoints  
- Day 6 — DNS + Private DNS Zones  
- **Day 7 — Bicep: VNet + Subnets + NSGs + Private Endpoints + DNS Zones**  

**Mapped AZ‑104 Chapters:**  
4, 5, 6

---

# 📘 **Week 3 — Compute & Storage**  
### *VMs, VMSS, disks, snapshots, storage tiers, file shares.*

**Hands‑on Labs:**
- Day 1 — VM Provisioning (Portal + CLI)  
- Day 2 — VM Scale Sets + Load Balancer  
- Day 3 — Disks, Snapshots, Disk Encryption  
- Day 4 — Storage Tiers (Hot/Cool/Archive)  
- Day 5 — Azure Files (SMB + NFS)  
- Day 6 — Storage Security (Firewalls, Private Endpoints)  
- **Day 7 — Bicep: VMSS + Storage Account + Containers + Lifecycle Policies**  

**Mapped AZ‑104 Chapters:**  
9, 12

---

# 📙 **Week 4 — Monitoring, Backup, Automation**  
### *Operational excellence: logs, alerts, backup, automation.*

**Hands‑on Labs:**
- Day 1 — Azure Monitor + Metrics  
- Day 2 — Log Analytics Workspace + KQL  
- Day 3 — Alerts (Metric + Log)  
- Day 4 — Azure Backup (VM + File Share)  
- Day 5 — Recovery Services Vault + Restore  
- Day 6 — Automation Runbooks + Update Management  
- **Day 7 — Bicep: Log Analytics + Diagnostic Settings + Alerts + Backup Policies**  

**Mapped AZ‑104 Chapters:**  
7, 8

---

# 🎯 Why Adding Bicep to Day 7 Works Perfectly

- Keeps your **portal-first** learning intact  
- Reinforces everything you built during the week  
- Produces **portfolio artifacts** every week  
- Builds IaC skills without overwhelming you  
- Mirrors real enterprise workflows (Portal → IaC codification)  
- Aligns with AZ‑104 but also prepares you for AZ‑305  
