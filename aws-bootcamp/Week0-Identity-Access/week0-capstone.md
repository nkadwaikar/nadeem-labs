# 🏗️ Week 0 Capstone — Identity & Access Foundation
### Entra ID → AWS • Zero IAM Users • SCIM Provisioning • SSO

Week 0 establishes the **identity foundation** for your entire AWS environment.  
This capstone demonstrates how real enterprises integrate identity providers with AWS, eliminating IAM users and enabling enterprise-grade access control.

---

# 🎯 Capstone Goals

By the end of this capstone, you will have:

- Secured the AWS root account with MFA
- Created a break-glass admin user
- Enabled AWS IAM Identity Center
- Integrated Entra ID as the identity provider via SAML
- Enabled SCIM for automatic user/group provisioning
- Created Entra ID groups (Admins, Developers, ReadOnly)
- Configured permission sets for least-privilege access
- Mapped Entra groups to AWS permission sets
- Tested SSO login flow end-to-end
- Documented the complete identity architecture

This becomes your **identity baseline** for all future AWS work.

---

# 🏛️ Architecture Overview

### **Identity Flow**
```
User → Entra ID (IdP) → SAML Authentication → IAM Identity Center → Permission Set → Temporary AWS Credentials
```

### **Provisioning Flow**
```
Entra ID Groups → SCIM → IAM Identity Center → Automatic Sync → AWS Access
```

### **Components**
1. **Entra ID** - Single source of truth for identities
2. **SAML 2.0** - Federated authentication protocol
3. **SCIM** - Automated user/group provisioning
4. **IAM Identity Center** - AWS access broker (formerly AWS SSO)
5. **Permission Sets** - Reusable access policies
6. **Temporary Credentials** - Time-limited session tokens

---

# 📁 Capstone Folder Structure

```
Week0-Identity-Access/
│
├── capstone/
│   ├── architecture/
│   │   ├── identity-flow-diagram.png
│   │   ├── saml-integration.png
│   │   ├── scim-provisioning.png
│   │   └── permission-set-mapping.png
│   │
│   ├── docs/
│   │   ├── 01-root-account-security.md
│   │   ├── 02-enable-identity-center.md
│   │   ├── 03-entra-saml-setup.md
│   │   ├── 04-scim-provisioning.md
│   │   ├── 05-permission-sets.md
│   │   ├── 06-group-mapping.md
│   │   └── 07-sso-testing.md
│   │
│   └── terraform/
│       ├── identity-center.tf
│       ├── permission-sets.tf
│       └── variables.tf
│
├── README.md
└── week0-capstone.md   ← (this file)
```

---

# 🔐 Phase 1 — Secure the Root Account

### **Tasks**
- Enable MFA on root account
- Store root credentials in secure vault
- Create break-glass IAM admin user (emergency access only)
- Enable MFA for break-glass user
- Document root account access procedures

### **Validation**
- [ ] Root account has MFA enabled
- [ ] Root credentials securely stored
- [ ] Break-glass admin created with MFA
- [ ] Root access procedure documented
- [ ] No other IAM users exist

---

# 🏢 Phase 2 — Enable IAM Identity Center

### **Tasks**
- Navigate to IAM Identity Center
- Choose identity source (External IdP)
- Configure organization
- Select AWS region for Identity Center
- Note the Identity Center portal URL

### **Validation**
- [ ] IAM Identity Center enabled
- [ ] Organization configured
- [ ] Portal URL documented
- [ ] Ready for external IdP integration

---

# 🔗 Phase 3 — Configure Entra ID SAML Integration

### **Tasks**
- In Entra ID: Create enterprise application for AWS
- Download Identity Center SAML metadata
- Upload to Entra ID application
- Download Entra ID SAML metadata
- Upload to Identity Center
- Configure SAML attribute mappings
- Test SAML connection

### **Validation**
- [ ] Entra ID application created
- [ ] SAML metadata exchanged
- [ ] Attribute mappings configured
- [ ] SAML connection tested successfully
- [ ] No errors in connection test

---

# 🔄 Phase 4 — Enable SCIM Provisioning

### **Tasks**
- In Identity Center: Generate SCIM endpoint and token
- In Entra ID: Configure automatic provisioning
- Enter SCIM endpoint URL
- Enter SCIM bearer token
- Test provisioning connection
- Enable automatic sync
- Monitor initial sync

### **Validation**
- [ ] SCIM endpoint configured
- [ ] Token securely stored
- [ ] Provisioning connection successful
- [ ] Automatic sync enabled
- [ ] Initial sync completed without errors

---

# 👥 Phase 5 — Create Entra ID Groups

### **Tasks**
- Create `AWS-Admins` group
- Create `AWS-Developers` group
- Create `AWS-ReadOnly` group
- Add test users to groups
- Verify groups sync to Identity Center

### **Validation**
- [ ] All three groups created
- [ ] Groups synced to Identity Center
- [ ] Test users assigned to groups
- [ ] Groups visible in Identity Center console

---

# 🎫 Phase 6 — Create Permission Sets

### **Tasks**
- Create `AdministratorAccess` permission set
- Create `PowerUserAccess` permission set
- Create `ReadOnlyAccess` permission set
- Configure session duration (4-12 hours)
- Add tags to permission sets
- Document permission set policies

### **Validation**
- [ ] All three permission sets created
- [ ] Session duration configured
- [ ] Tags applied
- [ ] Policies documented
- [ ] No inline wildcard permissions (unless justified)

---

# 🗺️ Phase 7 — Map Groups to Permission Sets

### **Tasks**
- Assign `AWS-Admins` → `AdministratorAccess`
- Assign `AWS-Developers` → `PowerUserAccess`
- Assign `AWS-ReadOnly` → `ReadOnlyAccess`
- Specify target AWS accounts
- Review assignment summary
- Document group-to-role mappings

### **Validation**
- [ ] All groups mapped correctly
- [ ] Target accounts specified
- [ ] Assignments show as "Provisioned"
- [ ] Mapping documentation complete

---

# ✅ Phase 8 — Test SSO Login Flow

### **Tasks**
- Access Identity Center portal URL
- Sign in with Entra ID credentials
- Verify MFA challenge
- View available AWS accounts and roles
- Select a role and access AWS console
- Verify temporary credentials
- Test CLI access with SSO
- Log out and verify session termination

### **Validation**
- [ ] SSO login successful
- [ ] MFA enforced
- [ ] Correct roles displayed
- [ ] AWS console access works
- [ ] Temporary credentials verified
- [ ] AWS CLI SSO configured
- [ ] Session termination works

---

# 📋 Final Validation Checklist

### **Identity Foundation**
- [ ] Root account secured with MFA
- [ ] Break-glass admin created
- [ ] IAM Identity Center enabled
- [ ] Entra ID SAML configured
- [ ] SCIM provisioning enabled

### **Groups & Permissions**
- [ ] Entra groups created and synced
- [ ] Permission sets configured
- [ ] Groups mapped to permission sets
- [ ] All assignments provisioned

### **SSO & Access**
- [ ] SSO login tested successfully
- [ ] MFA enforced for all users
- [ ] Temporary credentials working
- [ ] AWS CLI SSO configured
- [ ] Zero IAM users (except break-glass)

### **Documentation**
- [ ] Architecture diagrams created
- [ ] Step-by-step guides documented
- [ ] Troubleshooting notes captured
- [ ] Emergency access procedures documented

---

# 🎓 Capstone Outcome

You now have an **enterprise-grade identity foundation**:

✅ **Zero standing privileges** - No IAM users, only federated access  
✅ **Automatic provisioning** - Users/groups sync automatically  
✅ **Least privilege** - Permission sets enforce minimal access  
✅ **Audit-ready** - All access via Entra ID with MFA  
✅ **Enterprise pattern** - Mirrors how real companies operate  

This identity foundation supports:
- Multi-account AWS organizations
- Role-based access control (RBAC)
- Compliance requirements (SOC2, ISO 27001)
- Zero-trust security model
- Scalable user management

---

# 🔗 Related Resources

- [← Back to Week 0 Overview](README.md)
- [Detailed Documentation](capstone/docs/)
- [Architecture Diagrams](capstone/architecture/)
- [Terraform Code](capstone/terraform/)
- [← Back to Main Bootcamp](../README.MD)

---

# 📝 Next Steps

After completing Week 0, proceed to:
- **Week 1** - IAM, Access Control & Account Security
- **Week 2** - Networking + EC2 (VM Admin)
- **Week 3** - S3, KMS, IAM Roles & Automation
- **Week 4** - Monitoring, Governance & Security
