# Utho Kubernetes Cluster (UKC) Storage Classes

## openebs (default)

This is the default storage class, providing read-write once access to applications on storage. If the application does not specify a storage class in the PersistentVolumeClaim (PVC), this storage class will be automatically assigned.

To use this storage class, apply the following YAML:

```
kubectl apply -f https://raw.githubusercontent.com/uthoplatforms/examples/main/pod-with-default-sc-pvc.yaml
```

## openebs-hostpath (Local PV)

This storage class is based on local hostpath storage, offering read-write once permission on storage. It is suitable when the worker node count is always one.

To use this storage class, apply the following YAML:

```
kubectl apply -f https://raw.githubusercontent.com/uthoplatforms/examples/main/pod-with-hostpath-sc-pvc.yaml
```

## openebs-nfs (NFS PV)

This storage class is NFS-based, providing read/write access to storage. It should be used when applications need to use shared storage.

To use this storage class, apply the following YAML:

```
kubectl apply -f https://raw.githubusercontent.com/uthoplatforms/examples/main/pod-with-nfs-sc-pvc.yaml
```

For dynamic provisioning of storage class, applications need to create Persistent Volume Claims (PVCs) to obtain persistent volume (storage) in the cluster. Based on application requirements, storage can be selected, and if the application does not define a storage class in the PVC, the default storage class (openebs(default)) will be assigned automatically.


# Utho Kubernetes Cluster (UKC) Load Balancer

## Step 1

Deploy Loadbalancer via API or via Utho Console https://console.utho.com
## [Loadbalancer Rest API Docs](https://utho.com/api-docs/#api-Load-Balancer-addloadbalancer)
## [Utho Console](https://console.utho.com)


## Step 2

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.10.0/deploy/static/provider/cloud/deploy.yaml
```

## Step 3 ( this step will nginx service to use given public ip and service will not be in pending mode)

```
apiVersion: v1
kind: Service
metadata:
  labels:
    app.kubernetes.io/component: controller
    app.kubernetes.io/instance: ingress-nginx
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
    app.kubernetes.io/version: 1.10.0
  name: ingress-nginx-controller
  namespace: ingress-nginx
spec:
  externalTrafficPolicy: Local
  ipFamilies:
  - IPv4
  ipFamilyPolicy: SingleStack
  ports:
  - appProtocol: http
    name: http
    port: 80
    protocol: TCP
    targetPort: http
  - appProtocol: https
    name: https
    port: 443
    protocol: TCP
    targetPort: https
  externalIPs:
  - Public IP  ### change here with your real public ip of loadbalancer 
  loadBalancerIP: Public IP ## change here with your real public ip loadbalancer 
  selector:
    app.kubernetes.io/component: controller
    app.kubernetes.io/instance: ingress-nginx
    app.kubernetes.io/name: ingress-nginx
  type: LoadBalancer
 ```

