# TrustOps Baseline SOC 2 Rules (v1)

Each rule: **Intent → Enforcement → Evidence**  
Mapped to SOC 2 Trust Services Criteria (TSC).

---

1. **MFA for privileged access** (CC6, CC7)  
- Intent: Protect against credential-only compromise.  
- Enforcement: CI requires SSO+MFA for maintainers; AWS IAM MFA enabled for admins.  
- Evidence: CI org settings export; screenshot/policy export of MFA enforcement.

2. **RBAC & least privilege** (CC6)  
- Intent: Ensure users/services have minimum rights.  
- Enforcement: Terraform denies `AdministratorAccess`; scoped IAM roles only.  
- Evidence: `terraform show` redacted + `aws iam list-attached-role-policies`.

3. **Secrets outside repo** (CC6, C1)  
- Intent: No hardcoded secrets.  
- Enforcement: Conftest denies plaintext in configs; require SSM Parameter Store refs.  
- Evidence: Scanner logs + Parameter Store keys.

4. **TLS enforced end-to-end** (CC6)  
- Intent: Protect data in transit.  
- Enforcement: Deny non-TLS listeners; app redirects to HTTPS.  
- Evidence: Terraform plan flags; `curl -I https://` check.

5. **Centralized logging** (CC7)  
- Intent: Enable visibility into system activity.  
- Enforcement: Terraform attaches CloudWatch Logs/metrics to workloads.  
- Evidence: Dashboard JSON + sample log stream.

6. **Encryption at rest** (CC6, C1)  
- Intent: Protect data at rest.  
- Enforcement: S3 SSE on; EBS encrypted; RDS `storage_encrypted=true`.  
- Evidence: AWS resource summaries.

7. **Automated backups** (A1)  
- Intent: Ensure recovery capability.  
- Enforcement: Backup plans for DB/storage; restore tested in sandbox.  
- Evidence: Last backup timestamp + restore test log.

8. **Change mgmt approvals** (CC8)  
- Intent: Require peer review for changes.  
- Enforcement: Protected branches, code owners, PR reviews.  
- Evidence: Branch protection export + sample PR history.

9. **Monitoring & alert thresholds** (A1)  
- Intent: Detect downtime or errors quickly.  
- Enforcement: CloudWatch alarms for 5xx/error budget burn.  
- Evidence: Alarm definitions + triggered sample.

10. **Policy violations alerting** (CC7)  
- Intent: Make compliance failures visible.  
- Enforcement: CI fails on OPA/Checkov violations; optional notifications.  
- Evidence: CI logs + notification proof.

---

> Note: Only AWS Free Tier + open-source tooling is used. Secrets Manager, EKS, and paid services are deferred until later versions.