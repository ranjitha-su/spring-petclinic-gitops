# spring-petclinic-gitops

> **Part of a 3-repo End-to-End DevSecOps Application release pipeline.**  
> | [spring-petclinic-app](https://gitlab.com/ranjitha-projects/spring-petclinic-app) | [spring-petclinic-gitops](https://gitlab.com/ranjitha-projects/spring-petclinic-gitops) | [eks-platform](https://gitlab.com/ranjitha-projects/terraform-eks-platform) |

---

## Architecture

![GitOpsEndToEnd](GitOpsEndToEndApplicationReleasePipeline.png)

## What This Repo Does

**spring-petclinic-gitops:** Contains Kubernetes manifests managed with Kustomize. The image tag in `kustomization.yaml` is automatically updated by the application pipeline. ArgoCD watches this repo and syncs changes to the EKS cluster.

---

## Prerequisites

The following CI/CD variables must be set in **GitLab → Settings → CI/CD → Variables** before the pipeline can run:

| Variable | Description |
|----------|-------------|
| `GITLAB_USERNAME` | GitLab username used by the CI bot to push back to this repo |
| `GITLAB_TOKEN` | GitLab personal or project (more secure) access token with `write_repository` scope |

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

Pipelines are implemented in **GitLab CI**.

---

## Related Repos

| Repo | Purpose |
|------|---------|
| [spring-petclinic-app](https://github.com/youruser/spring-petclinic-app) | Application source code + CI pipeline |
| [spring-petclinic-gitops](https://github.com/youruser/spring-petclinic-gitops) | K8s manifests + ArgoCD config |
| [eks-platform](https://github.com/youruser/eks-platform) | EKS cluster + ArgoCD bootstrap (Terraform) |