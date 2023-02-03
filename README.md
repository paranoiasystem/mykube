# How to fix ArgoCD infinite healtcheck on ingress

`kubectl -n argocd edit configmap argocd-cm`

add

```yaml
data:
  resource.customizations: |
    networking.k8s.io/Ingress:
        health.lua: |
          hs = {}
          hs.status = "Healthy"
          return hs
```