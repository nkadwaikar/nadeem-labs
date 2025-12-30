# Day 2 — Notes & Key Takeaways

## 1. Key Vault Access Models (RBAC vs Access Policies)
- Modern deployments should use **RBAC authorization**, not Access Policies.
- RBAC integrates cleanly with Managed Identities and Azure AD roles.
- Access Policies are legacy and harder to audit or govern.

**Takeaway:**  
RBAC-based Key Vault access is the recommended, future-proof model.

---

## 2. Managed Identity + Key Vault Integration
- VM’s system-assigned identity authenticates without secrets.
- Role required: **Key Vault Secrets User**.
- Identity must be assigned at the **Key Vault scope**.
- No need for Access Policies, SAS tokens, or client secrets.

**Takeaway:**  
Managed Identity + RBAC = secure, secretless authentication.

---

## 3. Least-Privilege Enforcement
- VM identity can **read** secrets but cannot write/delete.
- Contributor (Alex) can see the Key Vault resource but **cannot** read secrets.
- IAM actions require:
  - User Access Administrator  
  - Owner  
  - Global Administrator  

**Takeaway:**  
Key Vault enforces strict separation between **control-plane** and **data-plane** permissions.

---

## 4. RBAC Propagation Behavior
- Role assignments may take **up to 5 minutes** to apply.
- Secret retrieval may fail during propagation with:
  - `Forbidden`
  - `AuthorizationPermissionMismatch`

**Takeaway:**  
RBAC propagation delay is normal — always re-test after a few minutes.

---

## 5. Common Troubleshooting Patterns
- **Forbidden:** Missing RBAC role  
- **VaultNotFound:** Wrong vault name or region  
- **Identity mismatch:** Running `az login --identity` in Cloud Shell  
- **Firewall issues:** Key Vault network restrictions enabled  

**Takeaway:**  
Most Key Vault issues fall into identity, RBAC, or networking categories.

---

## 6. Governance Alignment
- Key Vault centralizes secrets and enforces least privilege.
- Managed Identity eliminates credential sprawl.
- RBAC provides auditable, role-based access control.

**Takeaway:**  
Day 2 reinforces secure-by-default design principles for cloud workloads.