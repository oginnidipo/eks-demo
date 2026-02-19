# EKS Demo

Production-grade Amazon EKS cluster provisioned with Terraform, organized as modular infrastructure components.

## Architecture

```
├── vpc/          # VPC with public/private subnets, IAM roles
├── cluster/      # EKS cluster + managed node groups
├── autoscaler/   # Cluster Autoscaler IAM configuration
├── efs-csi/      # EFS CSI driver via Helm for persistent storage
└── users/        # IAM user management and RBAC
```

## Features

- **Modular Terraform** — each component is independently deployable with remote state references
- **Private node groups** — worker nodes run in private subnets for security
- **Cluster Autoscaler** — IAM policies for automatic node scaling
- **EFS CSI Driver** — persistent storage via Helm-managed EFS CSI driver
- **IAM & RBAC** — user management with proper role bindings

## Components

| Module | Purpose |
|--------|---------|
| `vpc` | VPC, subnets (public/private), IAM roles, networking |
| `cluster` | EKS cluster, managed node groups, provider config |
| `autoscaler` | Cluster Autoscaler IAM policies |
| `efs-csi` | EFS CSI driver deployment via Helm |
| `users` | IAM users, roles, and access management |

## Usage

Deploy in order:

```bash
# 1. Network layer
cd vpc && terraform init && terraform apply

# 2. EKS cluster
cd ../cluster && terraform init && terraform apply

# 3. Add-ons
cd ../autoscaler && terraform init && terraform apply
cd ../efs-csi && terraform init && terraform apply

# 4. Users (optional)
cd ../users && terraform init && terraform apply
```

## Related

- [k8s-observability-stack](https://github.com/oginnidipo/k8s-observability-stack) — Add production observability to this cluster
