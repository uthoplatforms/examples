
# Using Kong on Utho Kubernetes Cluster with Utho Load Balancer

## Prerequisites

- Utho Kubernetes Cluster
- Access to Utho's UI, CLI, or API
- Kubernetes CLI (`kubectl`) installed and configured

## Step-by-Step Guide

### 1. Deploy Kong Ingress Controller

To deploy the Kong Ingress Controller, execute the following command:

```sh
kubectl create -f https://raw.githubusercontent.com/Kong/kubernetes-ingress-controller/v2.12.3/deploy/single/all-in-one-dbless.yaml
```

### 2. Verify the Deployment

Check the services created by Kong in the `kong` namespace:

```sh
kubectl get services -n kong
```

You should see an output similar to:

```
NAME                       TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                      AGE
kong-proxy                 NodePort    10.96.20.238     <none>        80:30576/TCP,443:31849/TCP   5m
```

### 3. Note the NodePort

From the above output, identify the NodePort above 30000. For example, if you see `80:30576/TCP,443:31849/TCP`, then `30576` is the NodePort for HTTP traffic.

### 4. Deploy Utho Load Balancer

You can deploy a Load Balancer from Utho using the UI.

#### Using Utho UI

1. Navigate to the Load Balancer section in Utho's UI.
2. Create a new Load Balancer.
3. Attach the worker node or node pool as the backend.
4. Set the target port to the identified NodePort (e.g., `30576`).

We are updating this document with CLI and API examples for faster deployment.

### 5. Access the Service

After deploying the load balancer and attaching the backend nodes, you can access your service using the Load Balancer's IP address:

```sh
http://<loadbalancer-ip-address>
```

This IP address will route the traffic to the Kong Ingress Controller, enabling you to manage your Kubernetes services effectively.

For any support, please reach us at support@utho.com.
