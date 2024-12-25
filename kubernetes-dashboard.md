# How to Deploy the Kubernetes Dashboard Quickly and Easily

## Prerequisites
Ensure you have a running Kubernetes cluster and `kubectl` configured to communicate with your cluster.

## Install Dashboard 
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml
```

## Create Admin Token 
```bash
kubectl -n kubernetes-dashboard create token admin-user
```

## Start Proxy 
```bash
kubectl proxy --port=8001 & 
```


## Open in browser 
```bash
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
```


