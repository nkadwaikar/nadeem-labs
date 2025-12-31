<!-- filepath: vscode-vfs://github/nkadwaikar/nadeem-labs/README.md -->
# 🚀 Cloud Engineering — Built With Precision (and the Occasional Coffee Spill)

A growing collection of Azure labs, architectures, and Boot Camp notes — written to stay clean, practical, and easy to revisit. Perfect for the days when the cloud behaves, and the days when the coffee kicks in late.

---

## 👋 About Me

I work with Azure services and enjoy turning complex cloud tasks into clear, repeatable steps.  
My goal is simple: build documentation that's lightweight, organized, and friendly enough that *future me* won't wonder, "How did I do this last time?"

---

## 🎓 Azure Administrator Boot Camp (AZ‑104 Track)

This repo tracks my full Azure Administrator Boot Camp — a structured, identity‑first journey through Azure's core services.  
Each week focuses on a major domain (Identity, Networking, Compute, Monitoring), and every week ends with a real‑world capstone project deployed with Bicep.

Every lab is written to be clear, repeatable, and production‑ready — the kind of documentation I wish existed when I first started.

---

## 🧭 Full Multi‑Week Roadmap (AZ‑104 Aligned)

A high‑level view of the Boot Camp structure:

- **Week 1:** [Identity, RBAC, Managed Identity](./Week1-Identity-Governance/) 
- **Week 2:** Networking & Security  
- **Week 3:** Compute, App Services & Storage  
- **Week 4:** Monitoring, Backup & Governance  

Each week includes:
- 7 hands‑on labs  
- A real‑world capstone project  
- Architecture diagrams  
- Validation steps  
- A full Bicep deployment

---

## ✅ Completed Days

- **Day 1:** [RBAC, Managed Identity, Storage Access](./Week1-Identity-Governance/01-rbac-basics.md) (Completed)
- **Day 2:** [Key Vault + Managed Identity](./Week1-Identity-Governance/02-keyvault-managed-identity.md) (Completed)
- **Day 3:** Managed Identity → Storage Account (Blob Read Access)

This list grows as I progress through the Boot Camp.

---

## 📅 What This Boot Camp Includes

- Daily hands‑on labs  
- Architecture diagrams  
- Validation and troubleshooting steps  
- Notes & takeaways for long‑term retention  
- A full AZ‑104‑aligned learning path  

---

## 📘 Featured Labs

### **Azure Front Door — Routing & Global Delivery**

A two‑part guide covering both routing and global content delivery for static websites:

**• Static Website Routing**  
How to connect Azure Front Door to a static website and validate routing end‑to‑end.

**• Modern CDN Delivery (Front Door Standard)**  
Azure CDN is retired for new deployments, and Front Door Standard now provides the modern CDN experience.  
This section covers global delivery, caching behavior, edge nodes, and the small quirks that make global distribution both powerful and occasionally humbling.

📖 **[View Full Lab →](./labs/Azure%20Front%20Door-Static%20Website%20Hosting%20Lab.md)**

---

## 🛠️ Upcoming Labs

### **Azure Front Door Rules Engine — Practical Scenarios**

Real‑world rule patterns: redirects, rewrites, header manipulation, cache overrides, and the classic "why is this rule not firing yet?" troubleshooting flow.

---

### **Azure Front Door Premium — Private Link End‑to‑End Lab**

A deeper dive into secure architectures using Front Door Premium with Private Link — private origins, locked‑down storage, and global delivery without exposing your backend.