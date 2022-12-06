# ArgoCD configurations repo

![ArgoCD](static/argocd.png?raw=true "ArgoCD")
![Prometheus](static/prometheus.png?raw=true "Prometheus")

This repository contains ArgiCD configuration scripts to boostrap kubernetes cluster with:
* self-managing ArgoCD
* AWS Load Balancer controller
* External Secrets
* ArgoCD image uploader
* Kube-prometheus stack
* Cluster autoscaler
* Metrics server
* [Weather-app](/https://github.com/s0rl0v/weather-app) deployment also happens there.

`apps-bootstrap` directory contains ArgoCD apps, `apps-live` directory is dedicated for workloads.

Kustomization manifests are used to compose the desired configuration.

Helm chart for `weather-backend` application is [here](/weather-backend/charts/weather-backend/Chart.yaml)

# Usage

Initialize apps with the following command - any further changes will be reconsiled by ArgoCD

```
# cd app-bootstrap/
# kustomize build | kubectl apply -f -
# cd app-live/
# kustomize build | kubectl apply -f -
```

Get access to K8S cluster:

```
# aws eks update-kubeconfig --name sorlov-sandbox
# kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
# kubectl -n argocd port-forward service/argocd-server 8000:80
```

Navigate to ArgoCD UI to check rollout status.
