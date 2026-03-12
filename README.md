<h1 align="center">Manifests</h1>

This repository contains **Kubernetes manifests** for deploying the WordPress infrastructure via ArgoCD using a GitOps approach.

## Features

- **Orchestration:** Kubernetes with Kustomize
- **Deployment:** ArgoCD ApplicationSet for GitOps continuous delivery
- **Components:** WordPress web app + MariaDB database
- **Networking:** NGINX ingress with TLS via cert-manager
- **Storage:** 5Gi ReadWriteMany persistent volumes

## Components

1. **applications.yml** – ArgoCD ApplicationSet definition targeting this repository.
2. **web/base/** – WordPress deployment, service, ingress, PVC and Kustomize config.
3. **database/base/** – MariaDB deployment, service, PVC and Kustomize config.

## Structure

```
manifests/
├── applications.yml
├── web/base/
│   ├── deployment.yml
│   ├── service.yml
│   ├── ingress.yml
│   ├── pvc.yml
│   └── kustomization.yml
└── database/base/
    ├── deployment.yml
    ├── service.yml
    ├── pvc.yml
    └── kustomization.yml
```

## Deployment

Manifests are automatically applied by ArgoCD when changes are pushed to this repository. No manual `kubectl apply` is required.

To apply manually:

```bash
kubectl apply -k web/base/
kubectl apply -k database/base/
```

## Environment Variables

Sensitive values are injected via Kubernetes secrets:

- `WORDPRESS_DB_HOST` – Database service hostname
- `WORDPRESS_DB_USER` – Database user
- `WORDPRESS_DB_PASSWORD` – Database password
- `WORDPRESS_DB_NAME` – Database name

---
<p align="center">© 2026 - CEA Informatics</p>
