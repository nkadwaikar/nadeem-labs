# 🧭 AWS Administrator Boot Camp  
### Identity‑First • Hands‑On • Entra‑Integrated • Admin‑Focused

This 5‑week AWS Boot Camp (including Week 0) is designed to build real AWS Administrator skills using an identity‑first architecture, Entra ID federation, and enterprise‑grade governance.

It mirrors how real companies onboard and train AWS Admins.

---

# �️ Folder Structure
```
aws-bootcamp/
│
├── Week0-Identity-Access/         # Identity Foundation (Entra → AWS)
│   ├── README.md
│   ├── week0-capstone.md
│   └── capstone/
│       ├── terraform/             # Infrastructure as Code
│       ├── docs/                  # Documentation and guides
│       └── architecture/          # Architecture diagrams
│
├── Week1-IAM-Security/            # IAM, Access Control & Account Security
│   ├── README.md
│   ├── week1-capstone.md
│   └── capstone/
│       ├── terraform/
│       ├── docs/
│       └── architecture/
│
├── Week2-Networking-EC2/          # Networking + EC2 (VM Admin)
│   ├── README.md
│   ├── week2-capstone.md
│   └── capstone/
│       ├── terraform/
│       ├── docs/
│       └── architecture/
│
├── Week3-Storage-Automation/      # S3, KMS, IAM Roles & Automation
│   ├── README.md
│   ├── week3-capstone.md
│   └── capstone/
│       ├── terraform/
│       ├── docs/
│       └── architecture/
│
└── Week4-Monitoring-Governance/   # Monitoring, Governance & Security
    ├── README.md
    ├── week4-capstone.md
    └── capstone/
        ├── terraform/
        ├── docs/
        └── architecture/
```

---

# �📘 AWS Admin Boot Camp Overview

| **Week** | **Theme** | **What You Learn** | **Hands‑On Deliverables** |
|---------|-----------|--------------------|---------------------------|
| **[Week 0](Week0-Identity-Access/)** | Identity Foundation (Entra → AWS) | SSO, SCIM, Permission Sets, Zero IAM users | Entra integration, group sync, SSO login, permission sets |
| **[Week 1](Week1-IAM-Security/)** | IAM & Account Security | IAM basics, policies, CloudTrail, billing protection | Custom IAM policies, CloudTrail, MFA enforcement, cost alarm |
| **[Week 2](Week2-Networking-EC2/)** | Networking + EC2 (VM Admin) | VPC, subnets, routing, EC2 lifecycle, SSM | VPC build, EC2 public/private, SGs, AMIs, SSM access |
| **[Week 3](Week3-Storage-Automation/)** | S3, KMS, IAM Roles & Automation | Storage, encryption, lifecycle, CLI, automation | S3 secure bucket, KMS, IAM role for EC2, lifecycle rules, CLI |
| **[Week 4](Week4-Monitoring-Governance/)** | Monitoring, Governance & Security | GuardDuty, Security Hub, Config, SCPs, patching | Config rules, SCPs, CloudWatch alarms, patch manager, cleanup |

---

# ⭐ WEEK 0 — Identity Foundation (Entra → AWS)

Your identity baseline before touching any AWS service.

### Skills
- SSO  
- SCIM provisioning  
- Permission Sets  
- Zero IAM users  
- Enterprise identity model  

### Hands‑On
- Secure root  
- Create break‑glass admin  
- Enable Identity Center  
- Add AWS app in Entra  
- Exchange metadata XML  
- Enable SCIM  
- Create Entra groups (Admins, Dev, ReadOnly)  
- Assign Permission Sets  
- Test SSO login  

---

# 🧱 WEEK 1 — IAM, Access Control & Account Security

Become the admin who controls access to AWS.

### Skills
- IAM policies  
- Custom JSON  
- Service roles  
- CloudTrail  
- MFA enforcement  
- Cost protection  

### Hands‑On
- Create custom IAM policies  
- Create service roles (EC2, Lambda)  
- Enable CloudTrail (all regions)  
- Create $5 billing alarm  
- Enforce MFA via Identity Center  
- Create tagging standards  

---

# 🌐 WEEK 2 — Networking + EC2 (VM Admin)

Build the network and deploy/manage servers.

### Skills
- VPC  
- Subnets  
- Route tables  
- Internet/NAT gateways  
- EC2 lifecycle  
- SSM Session Manager  
- Security Groups  

### Hands‑On
- Build VPC (2 public + 2 private subnets)  
- Deploy public EC2  
- Deploy private EC2  
- Connect using SSM (no SSH keys)  
- Create AMIs  
- Create SGs for web/app/admin  
- Test connectivity  

---

# 🔐 WEEK 3 — S3, KMS, IAM Roles & Automation

Manage storage, encryption, and identity‑based access.

### Skills
- S3  
- KMS encryption  
- IAM roles for EC2  
- Lifecycle rules  
- AWS CLI  
- CloudWatch Events  

### Hands‑On
- Create S3 bucket (block public access)  
- Enable versioning + KMS  
- Upload files  
- Create IAM role for EC2  
- Attach S3 read‑only policy  
- Test access from EC2  
- Create lifecycle rules (Glacier)  
- Install AWS CLI + SSO login  
- Automate a task with CloudWatch  

---

# 🛡️ WEEK 4 — Monitoring, Governance & Security

Become the admin who keeps AWS secure, compliant, and healthy.

### Skills
- GuardDuty  
- Security Hub  
- AWS Config  
- SCPs  
- CloudWatch  
- Patch Manager  
- Resource cleanup  

### Hands‑On
- Enable GuardDuty + simulate threat  
- Enable Security Hub  
- Enable AWS Config  
- Create Config rules (S3 encrypted, no public EC2)  
- Create SCP (deny S3 deletion)  
- Create CloudWatch alarms (CPU, billing, root login)  
- Patch EC2 using SSM Patch Manager  
- Clean up unused resources  

---

# 🎓 By the End of This Boot Camp, You Will Be Able To…

- Use Entra ID as the identity source for AWS  
- Manage AWS access with Permission Sets  
- Build secure VPCs  
- Deploy and maintain EC2 servers  
- Use IAM roles instead of passwords  
- Manage S3, encryption, lifecycle  
- Monitor and secure AWS with GuardDuty, Config, Security Hub  
- Enforce governance with SCPs  
- Automate admin tasks  
- Keep AWS clean, patched, and cost‑efficient

---

# 🚀 Current Progress

| Week | Status |
|------|--------|
| Week 0 — Identity Foundation | ⏳ In Progress |
| Week 1 — IAM & Security | 📋 Planned |
| Week 2 — Networking + EC2 | 📋 Planned |
| Week 3 — Storage & Automation | 📋 Planned |
| Week 4 — Monitoring & Governance | 📋 Planned |

---

# 🧩 Skills Demonstrated
- **Identity & Access**: Entra ID federation, IAM Identity Center, permission sets, zero standing privileges
- **IAM Management**: Custom policies, service roles, least privilege, MFA enforcement
- **Infrastructure as Code**: Terraform modules, state management, reusable components
- **Networking**: VPC design, subnet segmentation, security groups, routing, NAT gateways
- **Compute**: EC2 provisioning, AMI management, SSM Session Manager, instance hardening
- **Storage & Encryption**: S3, KMS, lifecycle policies, bucket security
- **Security**: CloudTrail, GuardDuty, Security Hub, AWS Config, SCPs
- **Monitoring**: CloudWatch alarms, metrics, logs, cost management
- **Automation**: AWS CLI, CloudWatch Events, patch management
- **Documentation**: Architecture diagrams, runbooks, troubleshooting guides
- **Git Workflows**: Feature branches, pull requests, version control

---

# 🎯 Goal
Build an **audit-friendly**, **enterprise-grade**, and **hands-on** AWS Administrator portfolio that mirrors real-world cloud operations and demonstrates production-ready skills for AWS Administrator roles.
