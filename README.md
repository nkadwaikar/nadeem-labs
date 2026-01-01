# 🚀 Cloud Engineering – Built With Precision (and the Occasional Coffee Spill ☕)

A growing collection of Azure labs, architectures, and Boot Camp notes – written to stay clean, practical, and easy to revisit.  
Built for the days when the cloud behaves, and the days when it needs a little extra coffee (or encouragement).

This repository is designed for cloud engineers, architects, and certification candidates who want **hands-on, production-style Azure labs** – not just theory or exam notes.

## 🎓 Azure Boot Camp – Identity-First, Architect-Ready, Security-Focused

This repository tracks my full **Azure Boot Camp**, built around real-world cloud engineering and aligned with:

- **AZ-104** (Administrator)  
- **AZ-305** (Architect)  
- **AZ-500** (Security Engineer)  

Each week focuses on a major Azure domain and ends with a **capstone project** that demonstrates architect-level thinking and hands-on capability.

Every lab is designed to be:

- Clear  
- Repeatable  
- Production-aligned  
- Identity-first  
- Backed by Bicep deployments  

All written with the same care I put into my coffee – precise, consistent, and energizing enough to keep learning fun.

## **Week 1 – Identity & Governance**  
[Identity, RBAC, Managed Identity](./azure-bootcamp/Week1-Identity-Governance/README.md)

- Entra ID fundamentals  
- RBAC scopes & inheritance  
- Managed Identity patterns  
- Key Vault identity access  
- Identity-first architecture (Capstone 1)

## **Week 2 – Networking & Security**  
- Virtual networks & subnets  
- NSGs & ASGs  
- Private endpoints  
- Azure Firewall  
- Hub-spoke architecture (Capstone 2)

## **Week 3 – Compute, App Services & Storage**  
- Virtual machines  
- App Services  
- Storage accounts  
- Load balancers  
- 3-tier application deployment (Capstone 3)

### **Azure Front Door – Routing & Global Delivery**

A two-part guide covering routing and global content delivery for static websites:

**• Static Website Routing**  
Connecting Azure Front Door to a static website and validating routing end-to-end.

**• Modern CDN Delivery (Front Door Standard)**  
Azure CDN is retired for new deployments – Front Door Standard now provides the modern CDN experience.

This lab covers:

- Global edge delivery  
- Caching behavior  
- Routing validation  
- The small quirks you only notice after going global  

📖 **[View Full Lab →](./labs/Azure%20Front%20Door-Static%20Website%20Hosting%20Lab.md)**  

// ...existing code...

### **Azure Front Door Rules Engine – Practical Scenarios**
- Redirects & rewrites  
- Header manipulation  
- Cache overrides  
- Troubleshooting rule evaluation  

### **Azure Front Door Premium – Private Link End-to-End**
- Private origins  
- Locked-down storage accounts  
- Global delivery without exposing backend services