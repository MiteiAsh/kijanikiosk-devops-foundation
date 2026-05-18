# KijaniKiosk Week 7 vs Week 8 Delivery Comparison

KijaniKiosk completed a major transition this week from server-based deployments to container-based orchestration. The previous delivery model depended heavily on manually prepared servers and direct process management. This week's approach introduces a reproducible deployment pipeline built around immutable container images and automated workload recovery.

The most important operational improvement is consistency. In the previous deployment process, production behaviour depended on the exact state of the server at the time of deployment. Differences in installed packages, missing dependencies, or process state could produce inconsistent results between environments. The new delivery process packages the entire application runtime into a single production image that behaves identically wherever it runs.

This change also improved portability. The service can now move between environments without rebuilding the application separately for each machine. The same image used during testing is the image deployed into the cluster. This reduces deployment drift and improves rollback confidence because every release is versioned and traceable.

Operational resilience also improved significantly. During validation testing, a running service instance was intentionally deleted to simulate unexpected failure. The orchestration platform automatically recreated the missing instance and restored service health in approximately 2 seconds without operator intervention. Under the previous deployment model, recovery required manual service investigation and process restart activity.

Another measurable improvement came from the production image optimisation work completed earlier in the week. The original single-stage image baseline was substantially larger because it included unnecessary build tooling and development dependencies. The final production image was reduced to approximately 48.4MB, improving startup speed, reducing transfer overhead, and lowering registry storage consumption.

The new architecture also separates build concerns from runtime concerns more effectively. Development tooling exists only during the build stage and is excluded from the final runtime environment. This reduces attack surface area and improves operational safety by limiting what exists inside production containers.

| Concern | Week 7 Approach | Week 8 Approach |
|---|---|---|
| Deployment mechanism | Application deployed directly onto virtual machines using manually managed processes and server configuration. | Application packaged into immutable production containers and deployed through orchestration manifests. |
| Rollback mechanism | Rollback required switching traffic between manually maintained environments and restarting processes. | Rollback achieved by redeploying a previous versioned container image through the orchestration platform. |
| Failure recovery | Service recovery depended on manual operator intervention after process or server failure. | Failed workloads are automatically recreated by the orchestration platform without human involvement. |
| Scaling | Scaling required provisioning additional servers or manually duplicating processes. | Scaling controlled declaratively by adjusting replica count within the orchestration configuration. |

From a business perspective, the operational model is now more predictable and auditable. Every deployment artifact is versioned, reproducible, and independently verifiable. This creates a stronger foundation for compliance, incident response, and controlled release management. It also reduces the dependency on individual engineers remembering undocumented server configuration steps during deployments.

The deployment process now follows a complete delivery lifecycle: production image creation, versioned image distribution, orchestration deployment, service exposure, and automated recovery validation. This provides significantly stronger operational guarantees than the previous server-centric model and reduces the likelihood of environment-specific deployment failures.

However, the current platform is not yet production-complete. Environment-specific configuration values are still embedded directly into deployment definitions rather than managed centrally. Sensitive configuration management, readiness validation before traffic acceptance, and advanced rollout protections are also not yet implemented. Next week's work introduces centralized configuration management and secret handling, which will improve operational flexibility, security, and deployment safety across multiple environments.
