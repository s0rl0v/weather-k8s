# ArgoCD configurations repo

This repository contains manifests to boostrap kubernetes cluster with self-managing ArgoCD as well as with AWS Load Balancer controller, External Secrets, ArgoCD image uploader. Weather-app deployment also happens there.

`apps-registry` directory contains ArgoCD apps, other respective folders contain configurations for the apps deployment.

Kustomization manifests are used to compose the desired configuration.


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
