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

# Install Keycloak Operator

[https://www.keycloak.org/operator/installation](https://www.keycloak.org/operator/installation)

## Basic Deploy

info: [https://www.keycloak.org/operator/basic-deployment](https://www.keycloak.org/operator/basic-deployment)

### Database

for prod [https://access.crunchydata.com/documentation/postgres-operator/latest/](https://access.crunchydata.com/documentation/postgres-operator/latest/)

for test `keycloak_operator_example/example-postgres.yaml`

### Secret DB credential for Keycloak

test credential: postgres:testpassword

```sh
kubectl create secret generic keycloak-db-secret \
  --from-literal=username=[your_database_username] \
  --from-literal=password=[your_database_password]
```

### Keycloak Example 

for test `keycloak_operator_example/example-kc.yaml`