# argocd

## Setup

### Deploy argocd

```shell
kubectl apply -k apps/argocd
```

### Deploy cluster-base

```shell
kubectl apply -f apps/cluster-base/application.yaml
```
