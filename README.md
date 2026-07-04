# Installation with Kubernetes

## Install K3S

```bash
curl -sfL https://get.k3s.io | sh -
mkdir -p ~/.kube
sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
sudo chown $USER:$USER ~/.kube/config
```

## Deploy EspoCRM

```bash
kubectl apply -f espocrm-storage.yaml
kubectl apply -f espocrm-ingress.yaml
kubectl apply -f espocrm-db.yaml
kubectl apply -f espocrm.yaml
```

Check pods statuses:

```bash
kubectl get pods
```

Execute pod container:

```bash
kubectl exec -it {POD_NAME} -c {CONTAINER_NAME} -- /bin/bash
```

Check container logs:

```bash
kubectl logs deployment/espocrm -c espocrm
```

Check storage (volumes):

```bash
kubectl get pvc
```
