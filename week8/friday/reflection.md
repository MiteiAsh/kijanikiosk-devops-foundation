# Reflection

## 1. Hardest CI/CD Step

The hardest step to automate reliably would be the Kubernetes deployment verification stage. Build and push operations are deterministic, but orchestration environments introduce timing and networking variability. A deployment may appear successful while containers are still initializing or waiting for networking dependencies. The failure mode that concerns me most is a deployment entering a partially healthy state where some replicas are available but others continuously restart because of readiness or configuration problems.

## 2. Technical vs Plain Language

Plain language sentence:
"The orchestration platform automatically recreated the missing instance and restored service health in approximately 2 seconds."

Technical version for engineering teams:
"The Kubernetes Deployment controller detected replica divergence after Pod deletion and reconciled desired state by scheduling a replacement Pod that reached Running status within approximately 2 seconds."

The technical version is more precise because it identifies the exact control mechanism responsible for recovery behaviour. However, the plain language version is more accessible for non-technical stakeholders and communicates operational value more effectively.

## 3. Hardcoded Configuration

Several values currently remain hardcoded inside the deployment configuration and should move into centralized configuration management. These include the application port, image version references, service names, and environment-specific runtime values. Sensitive values such as database credentials, registry credentials, API tokens, and external service endpoints should be managed separately as secure configuration data rather than embedded directly into deployment definitions.

Keeping these values hardcoded creates operational risk because configuration changes require redeploying application manifests. It also increases the possibility of configuration drift between environments and raises security concerns if sensitive values are committed into version control systems.
