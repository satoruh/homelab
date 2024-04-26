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

## Instructions

### Kubernetes Clusterを作成する

kubeadmを使ってKubernetes Clusterを構築します。

```
cd ansible
ansible-playbook -i inventory.yaml site.yaml
```

### Argo CDをデプロイする

```
cd argocd
kubectl apply -k apps/argocd/
```

## Clean up

VMを削除する

```
cd ansible
ansbile-playbook -i inventory.yaml playbooks/cleanup.yaml
```
