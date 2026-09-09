# TravelBooking GitOps Repository

This repository contains the deployment manifests for the TravelBooking application,
managed by ArgoCD using GitOps principles.

## Structure

```
apps/                    # ArgoCD Application CRDs
charts/                  # Helm charts per service
network-policies/        # Cilium L7 network policies
```

## How It Works

1. CI pipeline (GitHub Actions) builds images and updates `image.tag` in `charts/<service>/values.yaml`
2. ArgoCD detects the commit and syncs the Helm charts to GKE
3. Cilium network policies enforce zero-trust service communication

## Bootstrap

```bash
kubectl apply -f apps/app-of-apps.yaml
```

## Important

- **Never manually edit resources in the cluster** — ArgoCD will revert them
- **All changes go through Git** — commit to this repo to deploy
- **Rollback** = `git revert` the commit
