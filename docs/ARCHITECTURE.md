TrustOps Architecture (Public / Demo) (v1)

Goal: Provide SOC 2 essentials as code: policy gates in CI/CD + cloud runtime checks + automated evidence collection — designed to run within free-tier/small-scale cloud resources for demos.

Components
	•	CI/CD: GitHub Actions (pull request checks + main deploys).
	•	Policy-as-Code: OPA/Conftest and Checkov (policy checks and IaC scans).
	•	IaC: Terraform for provisioning cloud resources.
	•	Cloud (demo):
	•	Small compute instances / container hosts (free-tier or equivalent).
	•	Versioned object store for evidence export.
	•	Configuration & posture service for baseline checks.
	•	Centralized logging and dashboards.
	•	Secure parameter store for secrets (production secrets are not stored in repo).

Flow
	1.	Developer PR → GitHub Actions runs build/tests + policy-as-code scans.
	2.	Policy Gate:
	•	❌ Fail if controls are violated.
	•	✅ Pass → Terraform plan (and optional apply in authorized environments).
	3.	Deploy → Demo cloud resources created for app, logging, and config snapshots.
	4.	Runtime Governance:
	•	Baseline config evaluates drift and compliance.
	•	Centralized logging collects telemetry and metrics.
	5.	Evidence Export:
	•	CI artifacts (policy results, sanitized plan summaries).
	•	Cloud posture snapshots (sanitized configuration exports).
	•	Stored in a versioned evidence bucket with retention policies.

Repo Layout

TrustOps/
├─ app/                # demo API and integration examples
├─ infra/              # Terraform (demo infrastructure)
├─ soc2-rules/         # policy-as-code examples (public/demo rules only)
├─ docs/               # architecture & SOC2 rules (sanitized)
└─ .github/workflows/  # CI/CD demo workflows

Trust Boundaries
	•	CI/CD → Cloud via short-lived credentials or OIDC (no long-lived credentials checked into repository).
	•	Secrets are stored in a secure parameter store in production; demo artifacts do not contain secrets.
	•	Evidence bucket is write-controlled by CI and read-accessible to authorized compliance roles only.

Summary

This architecture shows the demo-level flow for enforcing policy gates before merge, running posture checks at runtime, and collecting sanitized evidence for audit. Production enforcement configurations and signing/verification mechanisms are maintained in the private repository.

Prepared for publishing in the public demo repository.