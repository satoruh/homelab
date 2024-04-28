# homelab

Proxmox VE上にKubernetes Clusterを構築します。

## Requirements

### Proxmox VE server

SEE: https://www.proxmox.com/en/proxmox-virtual-environment/get-started

### Ansible

```
brew install ansible
```

### Argo CD

```
brew install argocd
```

### Helm

```
brew install helm
```

## Instructions

### Kubernetes Clusterを作成する

kubeadmを使ってKubernetes Clusterを構築します。

```
cd ansible
ansible-playbook -i inventory.yaml bootstrap.yaml
```

### cluster-admin なユーザを作成する

control-planeで下記を実行する

```
kubectl get cm kubeadm-config -n kube-system -o jsonpath='{.data.ClusterConfiguration}' > clusterconfiguration.yaml
sudo kubeadm kubeconfig user --client-name "${USER}" --org system:masters --config clusterconfiguration.yaml
```

### Argo CDをデプロイする

```
kubectl apply -k apps/argocd/
```

### その他のアプリケーションをデプロイする

```
kubectl apply -f apps/base/application.yaml
kubectl apply -f apps/monitoring/application.yaml
```

## Clean up

VMを削除する

```
cd ansible
ansbile-playbook -i inventory.yaml playbooks/cleanup.yaml
```
