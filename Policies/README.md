**Service Control Policies (SCPs) — Enforce Monitoring Compliance**

SCPs are attached to the production OU. They prevent spoke accounts from disabling or removing monitoring infrastructure. This ensures compliance is enforced at the governance layer — even if an account administrator attempts to remove monitoring components.

**IAM Trust Policy — Using aws:PrincipalOrgID (Organizations)**

The cross-account role uses aws:PrincipalOrgID instead of explicit account IDs. Any account within the Organization can assume this role — no per-account trust policy updates needed when adding new accounts.



