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

## Commands

Check pods statuses:

```bash
kubectl get pods
```

Stop pods:

```bash
kubectl scale deployment espocrm --replicas=0
kubectl scale deployment espocrm-db --replicas=0
```

Start pods:

```bash
kubectl scale deployment espocrm --replicas=1
kubectl scale deployment espocrm-db --replicas=1
```

Remove pods (full uninstall):

```bash
kubectl delete -f espocrm-ingress.yaml
kubectl delete -f espocrm.yaml
kubectl delete -f espocrm-db.yaml
kubectl delete -f espocrm-storage.yaml
```

Execute pod container:

```bash
kubectl exec -it {POD_NAME} -c {CONTAINER_NAME} -- /bin/bash
```

Check container logs:

```bash
kubectl logs deployment/espocrm -c espocrm
```

Check all elements statuses:

```bash
kubectl get pods,svc,ingress,pvc
```
