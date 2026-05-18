# Reflection

## 1. Translation for Non-Technical Audience

The rollback explanation felt closest to overclaiming because describing the recovery as “automatic” can make the system sound infallible. In reality, the rollback only works correctly if monitoring, health checks, and deployment state tracking are configured properly. I would improve the explanation by clarifying that the automation reduces recovery time significantly but still depends on correct monitoring design.

---

## 2. Highest-Value Action Item

The highest-value action item was adding deployment target validation before deployment execution. I am reasonably confident this would prevent a recurrence because the incident originated from an incorrect environment target. To be fully certain, I would need to review how deployment variables are passed through the pipeline and whether any manual overrides bypass validation.

---

## 3. Transition to Kubernetes

The concepts that carry forward are health checks, automated rollback logic, traffic switching, and environment state awareness. The parts that become less important are manual state files and custom nginx switching scripts because Kubernetes manages traffic routing, health monitoring, and rollback orchestration automatically through deployments and services.
