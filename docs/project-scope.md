# KijaniKiosk Capstone Scope

## Problem Statement

The current KijaniKiosk deployment can run in Kubernetes, but staging environments, deployment automation, monitoring, and operational documentation are incomplete. This makes releases harder to validate and increases operational risk.

## Track

Track A – Infrastructure First

## In Scope

1. Provision a staging namespace using Terraform.
2. Configure the staging environment using Ansible.
3. Deploy kk-payments using Kubernetes manifests and environment-specific configuration.
4. Add Jenkins deployment automation with a staging smoke test and approval gate.
5. Add Prometheus alert rules for application health monitoring.

## Out of Scope

1. Multi-region deployment (not required for project scope).
2. Production-grade managed Kubernetes infrastructure (using Minikube for demonstration).

## Success Criteria

1. Terraform creates the staging namespace successfully.
2. Ansible configures the namespace automatically.
3. Jenkins deploys to staging and runs a successful smoke test.
4. Prometheus alert rules are committed and validated.
5. kk-payments is reachable and healthy in staging.
