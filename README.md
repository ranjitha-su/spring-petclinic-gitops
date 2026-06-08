# microservices-gitops

> **Part of a 3-repo end-to-end DevSecOps project.**  
> | [microservices-app](https://gitlab.com/ranjitha-projects/microservices-demo-app) | [microservices-gitops](https://gitlab.com/ranjitha-projects/microservices-gitops) | [eks-platform](https://gitlab.com/ranjitha-projects/terraform-eks-platform) |

---

## What This Repo Does

**microservices-gitops:** Contains Kubernetes manifests managed with Kustomize. The image tag in `kustomization.yaml` is automatically updated by the application pipeline. ArgoCD watches this repo and syncs changes to the EKS cluster.

---

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     Developer Pushes Code                   │
└─────────────────────┬───────────────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────┐
│   microservices-app             │
│   GitLab CI Pipeline            │
│   - Lint & test                 │
│   - Build Docker image          │
│   - Push to Docker Hub          │
│   - Trigger GitOps pipeline ────┼──────────────┐
└─────────────────────────────────┘              │
                                                 ▼
                                  ┌──────────────────────────┐
                                  │   microservices-gitops   │
                                  │   GitLab CI Pipeline     │
                                  │   - Update image tag in  │
                                  │     kustomization.yaml   │
                                  │   - Commit & push        │
                                  └──────────┬───────────────┘
                                             │
                                             │ ArgoCD watches
                                             ▼
                                  ┌──────────────────────────┐
                                  │   eks-platform           │
                                  │   EKS Cluster (AWS)      │
                                  │   - ArgoCD syncs         │
                                  │     manifests            │
                                  │   - App deployed to k8s  │
                                  └──────────────────────────┘
```

---

## Tech Stack

| Layer | Tool |
|-------|------|
| CI/CD | GitLab CI |
| Container Registry | Docker Hub |
| GitOps | ArgoCD |
| K8s Manifests | Kustomize |
| Cluster | AWS EKS |
| Infra as Code | Terraform |

---

## CI/CD Note

Pipelines are implemented in **GitLab CI** (private). The `.gitlab-ci.yml` is available on request. This GitHub repo is the portfolio mirror.

---

## Related Repos

| Repo | Purpose |
|------|---------|
| [microservices-app](https://github.com/youruser/microservices-app) | Application source code + CI pipeline |
| [microservices-gitops](https://github.com/youruser/microservices-gitops) | K8s manifests + ArgoCD config |
| [eks-platform](https://github.com/youruser/eks-platform) | EKS cluster + ArgoCD bootstrap (Terraform) |