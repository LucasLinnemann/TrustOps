# TrustOps Architecture (v1)

**Goal:** Provide SOC 2 essentials as code: policy gates in CI/CD + AWS runtime checks + automated evidence collection — all running on AWS Free Tier.

---

## Components

- **CI/CD**: GitHub Actions (pull request checks + main deploys).
- **Policy-as-Code**: OPA/Conftest and Checkov to scan Terraform plans, configs, and app settings.
- **IaC**: Terraform for provisioning AWS Free Tier resources.
- **Cloud**: 
  - EC2 t2.micro / ECS (EC2 launch type)
  - S3 evidence bucket (versioned, lifecycle policy)
  - AWS Config (baseline managed rules)
  - CloudWatch (logs + dashboards)
  - SSM Parameter Store (secrets)
  - KMS (encryption free tier requests)

---

## Flow

1. **Developer PR** → GitHub Actions runs build/tests + OPA/Checkov scans.
2. **Policy Gate**:
   - ❌ Fail if controls violated.
   - ✅ Pass → Terraform plan/apply.
3. **Deploy** → AWS Free Tier resources created (app + logging + config).
4. **Runtime Governance**:
   - AWS Config evaluates drift and compliance.
   - CloudWatch collects logs and metrics.
5. **Evidence Export**:
   - CI artifacts (policy results, Terraform plans).
   - Cloud posture (Config snapshots, AWS CLI describes).
   - Stored in S3 with versioning + lifecycle retention.

---

## Repo Layout
TrustOps/
├─ app/                # demo API (.NET 8 later)
├─ infra/              # Terraform (AWS)
├─ soc2-rules/         # OPA/Checkov policies
├─ docs/               # architecture & SOC2 rules
└─ .github/workflows/  # CI/CD

---

## Trust Boundaries

- **CI/CD → AWS** via GitHub OIDC (no long-lived keys).
- **Secrets** in SSM Parameter Store, never in repo/CI logs.
- **Evidence bucket** write-once by CI, read-only by compliance role.

---

## Summary

TrustOps enforces compliance **before merge**, checks drift **after deploy**, and generates **immutable audit evidence** — showing engineers and compliance teams exactly where they stand.