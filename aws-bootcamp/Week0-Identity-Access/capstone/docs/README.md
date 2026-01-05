# 📚 Week 0 Documentation — Identity & Access Foundation

This directory contains detailed step-by-step guides for implementing Entra ID → AWS integration.

---

## 📖 Available Guides

### 🔐 Identity Integration Guides
- **01-root-account-security.md** - Securing the AWS root account and MFA setup
- **02-enable-identity-center.md** - IAM Identity Center configuration
- **03-entra-saml-setup.md** - Entra ID SAML integration
- **04-scim-provisioning.md** - Automatic user/group sync configuration
- **05-permission-sets.md** - Creating and managing permission sets
- **06-group-mapping.md** - Mapping Entra groups to AWS roles
- **07-sso-testing.md** - Testing and validating SSO login flow

### 🎯 Quick Start
1. Start with 01-root-account-security.md - Foundation security
2. Follow 02-enable-identity-center.md - Enable IAM Identity Center
3. Configure 03-entra-saml-setup.md - Set up SAML federation
4. Enable 04-scim-provisioning.md - Automatic provisioning
5. Create 05-permission-sets.md - Define access levels
6. Map 06-group-mapping.md - Connect Entra groups to AWS
7. Validate 07-sso-testing.md - Test the complete flow

---

## 🏗️ Week 0 Architecture

### Identity Flow

\`\`\`
User → Entra ID → SAML → IAM Identity Center → Permission Set → Temporary AWS Credentials
\`\`\`

### Components
1. **Entra ID** - Identity provider (IdP)
2. **SAML** - Authentication protocol
3. **SCIM** - Automated provisioning
4. **IAM Identity Center** - AWS access broker
5. **Permission Sets** - Role definitions
6. **Temporary Credentials** - Session tokens (no passwords)

---

## 🧪 Validation Checklist

### Identity Integration
- [ ] Root account secured with MFA
- [ ] Break-glass admin created
- [ ] IAM Identity Center enabled
- [ ] Entra ID SAML configured
- [ ] SCIM provisioning enabled
- [ ] Entra groups created (Admins, Dev, ReadOnly)
- [ ] Permission sets created
- [ ] Groups mapped to permission sets
- [ ] SSO login tested successfully

### Security Verification
- [ ] No IAM users exist (except break-glass)
- [ ] Root account not used for daily operations
- [ ] All access via Entra ID SSO
- [ ] MFA enforced for all users
- [ ] CloudTrail logging identity events

---

## 📋 Documentation Standards

Each guide in this directory follows this structure:

1. **Overview** - What you'll accomplish
2. **Prerequisites** - What's needed before starting
3. **Step-by-Step Instructions** - Detailed walkthrough with screenshots
4. **Validation** - How to verify success
5. **Troubleshooting** - Common issues and solutions
6. **Next Steps** - What comes after

---

## 🔗 Related Resources

- [← Back to Week 0 Overview](../../README.md)
- [Week 0 Capstone Details](../../week0-capstone.md)
- [Architecture Diagrams](../architecture/)
- [Terraform Code](../terraform/)
- [← Back to Main Bootcamp](../../../README.MD)

---

## 📝 Notes

- All screenshots should be stored in an \`images/\` subdirectory
- Configuration files should be stored in a \`configs/\` subdirectory
- Keep guides updated as AWS services evolve
- Document any deviations from standard procedures
