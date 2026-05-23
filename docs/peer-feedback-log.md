# Peer Feedback Log

## Feedback Item 1

**Issue:** Terraform configuration used a deprecated Kubernetes namespace resource.

**Severity:** Medium

**Resolution:** Replaced `kubernetes_namespace` with `kubernetes_namespace_v1`.

**Evidence:** Terraform plan completed without deprecation warnings after update.


## Feedback Item 2

**Issue:** Terraform state files were accidentally present in the project directory.

**Severity:** Low

**Resolution:** Confirmed `.gitignore` excluded Terraform state files and verified they were not tracked by Git.

**Evidence:** `git ls-files | grep tfstate` returned no tracked state files.


## Feedback Item 3

**Issue:** Ansible deployment failed because the Kubernetes Python dependency was missing.

**Severity:** Medium

**Resolution:** Installed the required Kubernetes Python package and reran the playbook successfully.

**Evidence:** Successful execution of `ansible-playbook ansible/staging-setup.yml`.
