# Installation with Kubernetes

## Install K3S (one-time)

```bash
curl -sfL https://get.k3s.io | sh -
mkdir -p ~/.kube
sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
sudo chown $USER:$USER ~/.kube/config
```

## Deploy EspoCRM

Note: before deploying you can change storage resources in the `espocrm-storage.yaml` file. 
The following resources is setted up by default:

- Database: 10Gi
- EspoCRM */data* directory: 10Gi
- EspoCRM */custom* directory: 5Gi
- EspoCRM */client/custom* directory: 5Gi

1. Create namespace for EspoCRM:

```bash
kubectl create namespace espocrm
```

2. Apply deployment:
   
```bash
kubectl apply -f espocrm-storage.yaml
kubectl apply -f espocrm-ingress.yaml
kubectl apply -f espocrm-db.yaml
kubectl apply -f espocrm.yaml
```

## Commands

Check pods statuses:

```bash
kubectl get pods -n espocrm
```

Stop pods:

```bash
kubectl scale statefulset espocrm --replicas=0 -n espocrm
kubectl scale statefulset espocrm-db --replicas=0 -n espocrm
```

Start pods:

```bash
kubectl scale statefulset espocrm --replicas=1 -n espocrm
kubectl scale statefulset espocrm-db --replicas=1 -n espocrm
```

Delete deployment (full uninstall):

```bash
kubectl delete namespace espocrm
```

Execute pod container:

```bash
kubectl -n espocrm exec -it espocrm-0 -c {CONTAINER_NAME} -- /bin/bash
kubectl -n espocrm exec -it espocrm-db-0 -- /bin/bash
```

Check logs:

```bash
kubectl logs statefulset/espocrm -c {CONTAINER_NAME} -n espocrm
kubectl logs statefulset/espocrm-db -n espocrm
```

Check all elements statuses:

```bash
kubectl get pods,svc,ingress,pvc -n espocrm
```
