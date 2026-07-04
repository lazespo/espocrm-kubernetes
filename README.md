# Installation with Kubernetes

## Install K3S

```
curl -sfL https://get.k3s.io | sh -
mkdir -p ~/.kube
sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
sudo chown $USER:$USER ~/.kube/config
```

## Deploy EspoCRM

```
kubectl apply -f espocrm-storage.yaml
kubectl apply -f espocrm-ingress.yaml
kubectl apply -f espocrm-db.yaml
kubectl apply -f espocrm.yaml
```

Check statuses:

```
kubectl get pods
```
