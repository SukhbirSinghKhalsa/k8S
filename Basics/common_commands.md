# 📦 Kubernetes (kubectl) Quick Reference Guide

A handy cheat sheet for commonly used `kubectl` commands to manage and troubleshoot your Kubernetes cluster.

---

## 1. 🔍 Basic Information & Context

Commands to understand your current cluster and environment:

```bash
kubectl cluster-info
```
Displays addresses of the control plane and services.

```bash
kubectl get nodes
```
Lists all nodes and their status.

```bash
kubectl config get-contexts
```
Shows all available cluster contexts (Dev, QA, Prod, etc.).

```bash
kubectl config use-context <name>
```
Switches to a specific cluster context.

```bash
kubectl version
```
Displays client and server Kubernetes versions.

---

## 2. 📄 Viewing Resources ("Get" Commands)

Use these to inspect what’s running in your cluster.

> 💡 Tip: Add `-n <namespace>` to target a specific namespace.

```bash
kubectl get pods
```
Lists all pods.

```bash
kubectl get svc
```
Lists all services.

```bash
kubectl get deployments
```
Shows deployments and their state.

```bash
kubectl get all
```
Displays pods, services, deployments, and replicasets.

```bash
kubectl get pods -o wide
```
Shows detailed pod info (node, IP, etc.).

---

## 3. ⚙️ Creating & Modifying Resources

Manage resources using YAML files or CLI commands.

```bash
kubectl apply -f <file.yaml>
```
Create or update resources from a file.

```bash
kubectl create deployment <name> --image=<image>
```
Quickly create a deployment.

```bash
kubectl edit <resource> <name>
```
Edit a live resource configuration.

```bash
kubectl delete -f <file.yaml>
```
Delete resources defined in a file.

```bash
kubectl delete pod <pod-name>
```
Delete a specific pod (it may restart if managed).

---

## 4. 🛠️ Troubleshooting & Debugging

Essential commands when something goes wrong.

```bash
kubectl describe pod <name>
```
Detailed pod info, events, and errors.

```bash
kubectl logs <name>
```
View container logs.

```bash
kubectl logs -f <name>
```
Stream logs in real time.

```bash
kubectl exec -it <name> -- /bin/bash
```
Access a container shell.

```bash
kubectl top pod
```
View CPU and memory usage (requires Metrics Server).

---

## 5. 🚀 Scaling & Rollouts

Manage deployments and application lifecycle.

```bash
kubectl scale deployment <name> --replicas=5
```
Scale number of replicas.

```bash
kubectl rollout status deployment <name>
```
Check rollout progress.

```bash
kubectl rollout undo deployment <name>
```
Rollback to previous version.

```bash
kubectl port-forward <pod-name> 8080:80
```
Forward pod port to local machine.

---

## 📌 Notes

- Always verify your current context before making changes:
  ```bash
  kubectl config current-context
  ```
- Use namespaces to organize workloads effectively.
- Prefer `kubectl apply` over `create` for declarative management.

---

## 🧠 Pro Tip

Create aliases for faster usage:

```bash
alias k=kubectl
```
