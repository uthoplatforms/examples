# Integrate Utho's registry with Utho's UKS

To integrate Utho's registry with Utho's UKS using kubectl, you can create a Kubernetes secret to store the Docker credentials and configure the Kubernetes service account to use this secret for pulling images. Here's a step-by-step guide on how to achieve this:


## Step1: Create a Docker Registry Secret

Create a Kubernetes secret to store the Docker registry credentials.

```sh
kubectl create secret docker-registry utho-registry-secret \
  --docker-server=registry.utho.io \
  --docker-username=$REGISTRY_USERNAME \
  --docker-password=$REGISTRY_PASSWORD >
```

## Step 2: Patch the Default Service Account
Patch the default service account in the namespace where your workloads are running to use this secret.

```sh
kubectl patch serviceaccount default \
  -p "{\"imagePullSecrets\": [{\"name\": \"utho-registry-secret\"}]}"

```
## Step 3: Verify the Configuration
Deploy a sample pod to verify that the secret is correctly configured and your pod can pull images from the Utho registry.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-pod
spec:
  containers:
  - name: test-container
    image: registry.utho.io/<your_image>:<your_tag>
  imagePullSecrets:
  - name: utho-registry-secret
```

Apply the configuration:

```sh
kubectl apply -f test-pod.yaml
```

## Summary
Create a Kubernetes secret using kubectl create secret docker-registry.
Patch the default service account to use the created secret.
Deploy a test pod to verify the setup.

