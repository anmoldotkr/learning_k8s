# ☸️ Kubernetes Commands Cheatsheet

A quick reference guide for commonly used `kubectl` and `minikube` commands.

---

## 📦 Namespace Commands

| Command | Description |
|--------|-------------|
| `kubectl get ns` | List all namespaces |
| `kubectl create namespace <namespace_name>` | Create a new namespace |

---

## 🚀 Pod Commands

| Command | Description |
|--------|-------------|
| `kubectl get pods` | List pods in the default namespace |
| `kubectl get pods -n <namespace_name>` | List pods in a specific namespace |
| `kubectl get pods -A` | List all pods across all namespaces |
| `kubectl get pods -w -n <namespace_name>` | Watch pods live in a namespace |
| `kubectl logs <pod_name> -n <namespace_name>` | View logs of a specific pod |

**Example:**
```bash
kubectl get pods -w -n nginx-dp
kubectl logs nginx-dp-7d4bfbcb6d-dzvgk -n nginx-dp
```

---

## 🛠️ Deployment Commands

| Command | Description |
|--------|-------------|
| `kubectl get deployments -A` | List all deployments across all namespaces |
| `kubectl get deployment -n <namespace_name>` | List deployments in a specific namespace |
| `kubectl describe deployment -n <namespace_name>` | Describe a deployment in detail |
| `kubectl create deployment <name> --image=<image> -n <namespace>` | Create a new deployment |
| `kubectl scale deployment <name> --replicas=<count> -n <namespace>` | Scale a deployment |

**Examples:**
```bash
# Create a deployment
kubectl create deployment nginx-dp --image=nginx -n nginx-dp

# Scale a deployment to 2 replicas
kubectl scale deployment nginx-dp --replicas=2 -n nginx-dp
```

---

## 🔁 ReplicaSet Commands

| Command | Description |
|--------|-------------|
| `kubectl get rs -n <namespace_name>` | List ReplicaSets in a namespace |
| `kubectl describe rs <replicaset_name> -n <namespace_name>` | Describe a specific ReplicaSet |

**Example:**
```bash
kubectl describe rs nginx-dp-7d4bfbcb6d -n nginx-dp
```

---

## 🌐 Service & Networking Commands

| Command | Description |
|--------|-------------|
| `kubectl get svc` | List services in the default namespace |
| `kubectl get svc -n <namespace_name>` | List services in a specific namespace |
| `kubectl expose deployment <name> --port=<port> --target-port=<target> --type=NodePort -n <namespace>` | Expose a deployment as a service |
| `kubectl get endpoints <service_name> -n <namespace_name>` | Get endpoints for a service |
| `minikube service list` | List all services in Minikube |

**Example:**
```bash
# Expose nginx-dp on port 81, targeting container port 80
kubectl expose deployment nginx-dp --port=81 --target-port=80 --type=NodePort -n nginx-dp

# Get endpoints
kubectl get endpoints nginx-dp -n nginx-dp
```

---

## 📋 General / Utility Commands

| Command | Description |
|--------|-------------|
| `kubectl get all -A` | List all resources across all namespaces |

---

## 🧩 Full Workflow Example: Deploy nginx

```bash
# 1. Create a namespace
kubectl create namespace nginx-dp

# 2. Create a deployment
kubectl create deployment nginx-dp --image=nginx -n nginx-dp

# 3. Scale the deployment
kubectl scale deployment nginx-dp --replicas=2 -n nginx-dp

# 4. Watch pods come up
kubectl get pods -w -n nginx-dp

# 5. Expose the deployment
kubectl expose deployment nginx-dp --port=81 --target-port=80 --type=NodePort -n nginx-dp

# 6. Verify the service
kubectl get svc -n nginx-dp

# 7. Check endpoints
kubectl get endpoints nginx-dp -n nginx-dp

# 8. View logs
kubectl logs <pod_name> -n nginx-dp
```

---