# Post-Incident Review: Week 5 Monday Incident

# 1. Incident Summary

During an investor demonstration, the deployment pipeline targeted the wrong environment and interrupted staging availability for approximately 48 seconds. The issue was identified during the live walkthrough and service was restored after the deployment target was corrected.

---

# 2. Timeline

- 09:14 UTC — Nia began investor demonstration
- 09:15 UTC — Deployment pipeline triggered
- 09:16 UTC (estimated ±1 minute) — Incorrect environment received deployment
- 09:16 UTC (estimated ±1 minute) — Users began receiving service errors
- 09:17 UTC — Engineering team identified incorrect deployment target
- 09:17 UTC — Rollback and environment correction initiated
- 09:18 UTC — Normal service restored and demonstration resumed

---

# 3. Root Cause

The deployment pipeline allowed deployments to proceed without validating the intended target environment.

Why?
1. The deployment script accepted environment values without verification.
2. No pre-deployment validation step checked whether the selected environment matched the intended target.
3. Environment state tracking relied on manual operator awareness.
4. The deployment process lacked enforced safeguards preventing production-impacting environment mistakes.

Structural finding:
The pipeline depended on human correctness instead of system-enforced environment validation.

---

# 4. Contributing Factors

- No automated rollback mechanism existed at the time of the incident.
- Environment naming conventions were inconsistent between scripts.
- The demonstration environment shared deployment tooling with operational environments.
- Monitoring visibility during the demonstration was limited.

---

# 5. Prevention Mechanisms

- Add mandatory deployment target validation before execution.
- Require environment confirmation checks inside deployment scripts.
- Separate demonstration environments from operational staging systems.
- Add automated rollback monitoring for failed deployments.

---

# 6. What Went Well

The engineering team identified the incorrect deployment target quickly and restored service within one minute. Communication during the incident remained clear and the demonstration resumed without requiring infrastructure rebuilds.

---

# 7. Action Items

| Owner | Action Item | Target Completion |
|---|---|---|
| DevOps Engineer | Add deployment environment validation checks to all deployment scripts | 1 week |
| Platform Team | Implement automated rollback monitoring for failed deployments | 2 weeks |
| Engineering Manager | Standardize environment naming conventions across all infrastructure scripts | 2 weeks |
| SRE Team | Create isolated demonstration environments separate from operational staging | 3 weeks |
