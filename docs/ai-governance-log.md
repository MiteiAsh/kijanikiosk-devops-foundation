# AI Governance Log

## Entry 1

**Date:** 2026-05-23

**Task:** Create Terraform configuration for staging namespace

**AI Tool:** ChatGPT

**Prompt Summary:** Generate Terraform code to create a Kubernetes staging namespace.

**AI Output:** Terraform namespace resource.

**What it got wrong:** The resource used a deprecated namespace type. Terraform warned that kubernetes_namespace was deprecated.

**Manual Review:** Checked Terraform plan output and reviewed provider documentation.

**Change Made:** Replaced kubernetes_namespace with kubernetes_namespace_v1.

**Governance Control Referenced:** Human review before deployment.


## Entry 2

**Date:** 2026-05-23

**Task:** Create Ansible playbook for namespace configuration

**AI Tool:** ChatGPT

**Prompt Summary:** Generate Ansible playbook to configure the staging namespace.

**AI Output:** Playbook using kubernetes.core.k8s module.

**What it got wrong:** Did not account for missing Python Kubernetes dependency on Ubuntu.

**Manual Review:** Ran playbook, investigated failure message, installed required dependency.

**Change Made:** Installed Kubernetes Python package and reran validation.

**Governance Control Referenced:** Dependency verification and execution testing.
