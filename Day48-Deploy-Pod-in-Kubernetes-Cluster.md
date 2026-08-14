# ☸️ Day 48 – Deploy Pod in Kubernetes Cluster

## 📌 Scenario

The Nautilus DevOps team started working with **Kubernetes for application management**.

The task was to create a Kubernetes Pod according to the following requirements:

- Create a Pod named `pod-httpd`
- Use the `httpd:latest` image
- Set the Pod label `app=httpd_app`
- Name the container `httpd-container`

The `kubectl` utility on the jump host was already configured to communicate with the Kubernetes cluster.

---

## 🎯 Objectives

- Create a Kubernetes Pod
- Understand Pod and container configuration
- Use the `httpd:latest` image
- Apply Kubernetes labels
- Configure a custom container name
- Verify the deployed Pod

---

## 🛠️ Tasks Performed

### ✅ 1. Check Existing Pods

Initially checked the Kubernetes cluster:

```bash
kubectl get pods
```

Output:

```
No resources found in default namespace.
```

---

### ✅ 2. Initial Pod Creation

Initially created the Pod using the imperative command:

```bash
kubectl run pod-httpd --image=httpd:latest
```

The Pod was successfully created.

However, this did not explicitly configure all the required fields such as the custom container name and label.

---

### ✅ 3. Create Kubernetes YAML Manifest

Created a YAML manifest using an editor:

```bash
vi pod-yaml.yml
```

**Configuration:**

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-httpd
  labels:
    app: httpd_app
spec:
  containers:
    - name: httpd-container
      image: httpd:latest
```

---

### ✅ 4. Apply the Manifest

Applied the configuration to the Kubernetes cluster:

```bash
kubectl apply -f pod-yaml.yml
```

Output:

```
pod/pod-httpd created
```

---

## 🔍 Verification

### Check Pod Status

```bash
kubectl get pods
```

Expected output:

```
NAME        READY   STATUS    RESTARTS   AGE
pod-httpd   1/1     Running   0          ...
```

---

### Verify Pod Label

```bash
kubectl get pod pod-httpd --show-labels
```

Confirmed output:

```
NAME        READY   STATUS    RESTARTS   AGE   LABELS
pod-httpd   1/1     Running   0          ...   app=httpd_app
```

---

### Inspect Pod Details

```bash
kubectl describe pod pod-httpd
```

Verified fields:

```
Name:         pod-httpd
Namespace:    default
...
Containers:
  httpd-container:
    Image:          httpd:latest
    State:          Running
...
Labels:           app=httpd_app
```

---

## ⚠️ Mistakes / Issues Faced

### ❌ Typo in kubectl Command

Initially entered:

```bash
kubectl gets pods
```

Kubernetes returned:

```
error: unknown command "gets" for "kubectl"
```

### 🔧 Fix

Used the correct command:

```bash
kubectl get pods
```

---

### 💡 Learning from the Mistake

`kubectl` follows a specific command structure:

```
kubectl <command> <resource> [options]
```

For example:

```bash
kubectl get pods
kubectl get services
kubectl get deployments
```

---

## 🧠 Key Learnings

- A **Kubernetes Pod** is the smallest deployable unit in Kubernetes
- Pods contain one or more containers
- **Kubernetes YAML** defines the desired state of resources
- `kubectl apply -f` creates or updates resources from a manifest
- **Labels** help identify and organize Kubernetes resources
- **Imperative commands** are useful for quick tasks
- **Declarative YAML** is more suitable for repeatable and version-controlled deployments
- Container names must be unique within a Pod
- The `default` namespace is used when no namespace is specified

---

## 🎤 Interview Questions

### Q1. What is a Pod?

**Answer:** A Pod is the smallest deployable unit in Kubernetes and can contain one or more containers. Containers within a Pod share network namespace, meaning they share IP addresses and ports.

---

### Q2. What is the purpose of labels?

**Answer:** Labels are key-value pairs used to identify, organize, and select Kubernetes resources. They enable resource organization and filtering.

**Example:**

```yaml
labels:
  app: httpd_app
  environment: production
  tier: frontend
```

---

### Q3. Difference between `kubectl run` and `kubectl apply`?

**Answer:**

| Aspect | kubectl run | kubectl apply |
|--------|-----------|--------------|
| **Type** | Imperative | Declarative |
| **Use Case** | Quick testing, prototyping | Production deployments |
| **Version Control** | Not ideal | Ideal (YAML files tracked) |
| **Flexibility** | Limited configuration | Full configuration control |
| **Reproducibility** | Lower | Higher |

---

### Q4. What does `apiVersion: v1` mean?

**Answer:** It specifies the **Kubernetes API version** used for the resource definition. `v1` is the stable, core API version used for basic resources like Pods, Services, and ConfigMaps.

---

### Q5. Why use YAML files in Kubernetes?

**Answer:**

- **Version Control:** Track infrastructure changes in git
- **Code Review:** Review changes before deployment
- **Reusability:** Reuse manifests across environments
- **Consistency:** Ensure consistent deployments
- **Documentation:** Self-documenting infrastructure
- **Automation:** Integrate with CI/CD pipelines

---

### Q6. What is a container name in a Pod specification?

**Answer:** The container name (`httpd-container` in this case) is a unique identifier for the container within the Pod. It's used to reference the container when viewing logs, executing commands, or managing the container lifecycle.

Example:

```bash
kubectl logs pod-httpd -c httpd-container
```

---

## 📌 Final Architecture

```
┌─────────────────────────────────────────┐
│   Kubernetes Cluster                    │
│                                         │
│   ┌─────────────────────────────────┐   │
│   │  Pod: pod-httpd                 │   │
│   │  Label: app=httpd_app           │   │
│   │                                 │   │
│   │  ┌─────────────────────────┐    │   │
│   │  │ Container: httpd-container │    │   │
│   │  │ Image: httpd:latest     │    │   │
│   │  │ Status: Running         │    │   │
│   │  └─────────────────────────┘    │   │
│   └─────────────────────────────────┘   │
└─────────────────────────────────────────┘
```

---

## 🚀 Final Result

✅ Pod `pod-httpd` created successfully

✅ `httpd:latest` image deployed

✅ Container named `httpd-container`

✅ Label `app=httpd_app` configured

✅ Pod verified using `kubectl` commands

---

## 📚 Additional Resources

- [Kubernetes Pods Documentation](https://kubernetes.io/docs/concepts/workloads/pods/)
- [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
- [Kubernetes API Versions](https://kubernetes.io/docs/reference/api-overview/)
