TrustOps — SOC 2 Baseline (Public / Demo) (v1)

Public demo only. Implementation details, production rule files, signing keys, and any operational secrets are kept in a private repository. This document describes the intent of each control and the types of evidence collected for audit purposes.

Each rule: Intent → Implementation (private) → Evidence
Mapped to SOC 2 Trust Services Criteria (TSC).

	1.	MFA for privileged access (CC6, CC7)

	•	Intent: Reduce risk of account compromise by requiring multi-factor authentication for privileged users.
	•	Implementation: Production enforcement is private.
	•	Evidence: Policy export or governance snapshot showing MFA requirement; sanitized configuration export.

	2.	RBAC & least privilege (CC6)

	•	Intent: Ensure users and services have only the permissions they need.
	•	Implementation: Production enforcement is private.
	•	Evidence: Role/policy inventory or role configuration summary (sanitized).

	3.	Secrets kept out of source (CC6, C1)

	•	Intent: Prevent hard-coded secrets, keys, or credentials in source code.
	•	Implementation: Production enforcement is private.
	•	Evidence: Secret-scan report (sanitized) and reference to secret management usage.

	4.	TLS enforced (data in transit) (CC6)

	•	Intent: Protect data in transit by enforcing TLS for external and internal endpoints.
	•	Implementation: Production enforcement is private.
	•	Evidence: Configuration snapshot showing enforced TLS (sanitized).

	5.	Centralized logging & auditability (CC7)

	•	Intent: Maintain telemetry and audit logs to support detection and investigation.
	•	Implementation: Production enforcement is private.
	•	Evidence: Example log-collection configuration and a sanitized sample log export.

	6.	Encryption at rest (CC6, C1)

	•	Intent: Protect stored data using at-rest encryption.
	•	Implementation: Production enforcement is private.
	•	Evidence: Resource configuration summary indicating encryption (sanitized).

	7.	Automated backups & tested restores (A1)

	•	Intent: Ensure recoverability of critical data through backups and restore tests.
	•	Implementation: Production enforcement is private.
	•	Evidence: Backup schedule summary and example restore-test result (sanitized).

	8.	Change management & code review (CC8)

	•	Intent: Require peer review and approvals for production changes.
	•	Implementation: Production enforcement is private.
	•	Evidence: Branch protection summary and an anonymized sample of approved change history.

	9.	Monitoring & alerting (A1)

	•	Intent: Detect operational issues and incidents via defined alarms and thresholds.
	•	Implementation: Production enforcement is private.
	•	Evidence: Alarm/metric definition summary and a sanitized sample alert event.

	10.	Policy violation detection & notification (CC7)

	•	Intent: Ensure compliance failures are detected pre-merge or in runtime and are actionable.
	•	Implementation: Production enforcement is private.
	•	Evidence: Policy-scan summary and an example notification (sanitized).

Notes
	•	This file is an illustrative summary of the intent and the types of evidence TrustOps collects for SOC 2 evaluations.
	•	The production enforcement mechanisms, concrete rule definitions, and signing/verification keys are not published here.
	•	For reproducible demo outputs and example reports, see test-vectors/ and examples/ in this repository (example artifacts are sanitized and watermarked).

Prepared for publishing in the public demo repository.