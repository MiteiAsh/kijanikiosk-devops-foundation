# Capstone Reflection

## What did I get wrong?

At the start of this project I assumed that deploying Kubernetes workloads and automating CI/CD would be mostly about writing manifests and pipeline scripts. During implementation I discovered that integration between tools (Terraform, Ansible, Kubernetes, and Jenkins) is often more difficult than the individual tools themselves.

A specific issue I ran into was assuming that installing kubectl inside Jenkins would automatically allow cluster access. In reality, Jenkins required proper kubeconfig setup and network connectivity to the Minikube cluster, which was more complex than expected.

If I repeated this project I would set up CI/CD-to-cluster connectivity earlier in the process to avoid delays during pipeline testing.

---

## Most important thing I learned

The most important concept I learned was Infrastructure as Code and environment separation. Using Terraform to create the staging namespace and Ansible to configure it showed how infrastructure can be made repeatable and version-controlled.

I also learned how Kubernetes deployments can be structured so that staging and production environments share the same base manifests but differ through configuration (ConfigMaps and namespaces).

---

## What would I do differently on a second pass?

On a second pass I would:
- Fully resolve Jenkins-to-Kubernetes connectivity earlier
- Add more automated testing in the pipeline (beyond rollout status)
- Deploy a complete monitoring stack (Prometheus/Grafana instead of only alert rules)
- Improve security by avoiding local kubeconfig dependencies and using service accounts for Jenkins
