# KijaniKiosk Capstone Project (Track A)

## Overview

This project extends the KijaniKiosk payments platform into a production-approaching Kubernetes environment with Infrastructure as Code, automated deployment, monitoring, and operational documentation.

## Architecture

- Terraform provisions the staging namespace
- Ansible configures the namespace
- Jenkins deploys to staging automatically
- Smoke tests validate deployments
- Approval gate controls production releases
- Kubernetes hosts the kk-payments application
- Prometheus monitors application health

## Prerequisites

- Docker
- Minikube
- kubectl
- Terraform
- Ansible
- Jenkins

## Setup

### Start Kubernetes

```bash
minikube start
```

### Provision staging namespace

```bash
cd terraform
terraform init
terraform apply -auto-approve
```

### Configure namespace

```bash
ansible-playbook ansible/staging-setup.yml
```

### Deploy application

```bash
kubectl apply -f k8s/staging/
```

## Monitoring

Prometheus alert rules are stored in:

```text
monitoring/kk-payments-alerts.yaml
```

## CI/CD Pipeline

1. Build
2. Deploy to staging
3. Smoke test
4. Manual approval gate
5. Deploy to production

## Repository Structure

docs/
ansible/
terraform/
monitoring/
k8s/
scripts/

## Known Limitations

- No TLS configured
- No Horizontal Pod Autoscaler
- Local Minikube deployment only
- Single-node cluster
