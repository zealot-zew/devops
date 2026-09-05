# Exercise 1: Deploying and Exposing an Nginx Web Server on Minikube

## Objective
To set up a local single-node Kubernetes cluster using **Minikube**, deploy a containerized **Nginx** web server pod, expose it to external traffic using a **NodePort Service**, and access the web application in a browser.

---

## Prerequisites
Ensure the following tools are installed and configured:
- [Minikube](https://minikube.sigs.k8s.io/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- A virtualization/container driver (e.g., Docker, vfkit, Hyperkit, or Podman)

---

## Steps of Execution

### Step 1: Start the Local Kubernetes Cluster
Initialize and start the local single-node Minikube cluster:
```bash
minikube start
```
> **Explanation**: This downloads the necessary VM/base image, starts the control plane, and configures `kubectl` to communicate with the local cluster.

---

### Step 2: Deploy the Nginx Pod
Create and run a new Kubernetes pod named `hello-k8s` using the official `nginx` container image:
```bash
kubectl run hello-k8s --image=nginx --port=80
```
> **Explanation**: The `kubectl run` command instructs the cluster to pull the `nginx` image (if not present) and run a container listening on port `80`.

---

### Step 3: Verify the Pod Status
Check the status of the newly created pod until it is in the `Running` state:
```bash
kubectl get pods
```
> **Explanation**: You may see the status transition from `ContainerCreating` to `Running` with `1/1` containers ready.

---

### Step 4: Expose the Pod via a NodePort Service
Expose the pod to external traffic by creating a Kubernetes `NodePort` Service:
```bash
kubectl expose pod hello-k8s --type=NodePort --port=80
```
> **Explanation**: This creates a Service resource of type `NodePort` targeting port 80 of the `hello-k8s` pod, allocating a cluster port for external access.

---

### Step 5: Access the Service in the Web Browser
Launch the service tunnel and open the web page in your default browser:
```bash
minikube service hello-k8s
```
> **Explanation**: Minikube generates an accessible tunnel URL (e.g., `http://127.0.0.1:<port>`) and automatically opens it in the browser.

---

## Output

