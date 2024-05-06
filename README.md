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


