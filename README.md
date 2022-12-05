# ArgoCD configurations repo

This repository contains all the manifests for kubernetes cluster, bootstrap and application.

# Usage

Initializa apps with the following command - any further changes will be reconsiled by ArgoCD

```
# cd app-registry
# kustomize build | kubectl apply -f -
```

Get access to K8S cluster:

```
# aws eks update-kubeconfig --name sorlov-sandbox
# kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
# kubectl -n argocd port-forward service/argocd-server 8000:80
```

Navigate to ArgoCD UI to check rollout status.
