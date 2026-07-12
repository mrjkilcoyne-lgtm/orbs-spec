# Cloud IAM (Identity & Access Management)

## Scope
Authentication, authorization, and service-to-service access control: policies, roles, service accounts, and federation.

## Core principles
- Least privilege is hard to achieve but essential — start with deny-all and grant only what's needed; audit regularly (IAM Access Analyzer, Prowler).
- Long-lived static credentials (API keys, passwords) are a liability — rotate frequently or use short-lived credentials (OIDC, workload identity, assume roles).
- Service accounts (non-human identities for applications) require the same rigor as user accounts — don't share service accounts across services.
- Authentication (who are you?) and authorization (what can you do?) are separate — implement strong auth and explicit role-based access control (RBAC).
- Audit logs are your accountability trail — log all permission changes, data access, and suspicious activity; they're useless if you don't analyze them.

## Apex practices
- Use identity federation (OIDC, SAML) to avoid managing separate credentials — users authenticate with their corporate identity provider.
- Implement assume-role workflows (require MFA for privileged roles) to prevent casual access to prod — high-privilege roles require multi-factor approval.
- Use workload identity (Kubernetes service accounts mapped to cloud identities) instead of mounting service account keys on containers.
- Review and remove unused service accounts and roles regularly (quarterly); accumulation of unused permissions is a security risk.

## Pitfalls
- Sharing service accounts across services (hard to audit and revoke) — one service account per service.
- Permissive wildcard policies (asterisks in resources/actions) — enumerate the specific resources and actions required.
- Missing or weak audit logging (no accountability for who did what) — enable full logging from day one.

## Tools & references
AWS IAM, GCP IAM, Azure RBAC, Terraform for IAM policy as code, Prowler for auditing, checkov for IaC scanning, CIS Benchmarks.
