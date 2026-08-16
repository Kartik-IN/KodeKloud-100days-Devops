# ⚙️ Day 50 – Kubernetes Resource Requests and Limits

## 📌 Scenario

The Nautilus DevOps team noticed performance issues in some Kubernetes-hosted applications due to resource constraints.

To improve resource management, the team decided to configure **CPU and memory requests and limits** for application containers.

The task was to create a Pod running Apache HTTP Server with specific resource requirements.

---

## 🎯 Objectives

- Create a Kubernetes Pod named `httpd-pod`
- Create a container named `httpd-container`
- Use the `httpd:latest` image
- Configure CPU and memory requests
- Configure CPU and memory limits
- Verify the resource configuration

---

## 📋 Resource Requirements

| Resource | Request | Limit |
|----------|---------|-------|
| CPU | `100m` | `100m` |
| Memory | `15Mi` | `20Mi` |

---

## 🛠️ Tasks Performed

### ✅ 1. Create Kubernetes YAML Manifest

Created a Pod manifest:

```bash
vi pod-yaml.yml
```

Configuration:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: httpd-pod
spec:
  containers:
    - name: httpd-container
      image: httpd:latest
      resources:
        requests:
          memory: "15Mi"
          cpu: "100m"
        limits:
          memory: "20Mi"
          cpu: "100m"
```

---

### ✅ 2. Apply the Manifest

Applied the configuration to the Kubernetes cluster:

```bash
kubectl apply -f pod-yaml.yml
```

Expected output:

```bash
pod/httpd-pod created
```

---

## 🔍 Verification

### Check Pod Status

```bash
kubectl get pods
```

Expected:

```bash
NAME        READY   STATUS    RESTARTS   AGE
httpd-pod   1/1     Running   0          ...
```

---

### Check Resource Configuration

```bash
kubectl describe pod httpd-pod
```

Verified:

```text
Requests:
  cpu:     100m
  memory:  15Mi

Limits:
  cpu:     100m
  memory:  20Mi
```

---

### View Complete Pod Configuration

```bash
kubectl get pod httpd-pod -o yaml
```

Verified that the container contained:

```yaml
resources:
  requests:
    memory: "15Mi"
    cpu: "100m"
  limits:
    memory: "20Mi"
    cpu: "100m"
```

---

## 🧠 Key Learnings

### 🔹 Resource Requests

A **request** defines the amount of CPU or memory Kubernetes considers when scheduling a Pod.

For this task:

```text
CPU:    100m
Memory: 15Mi
```

---

### 🔹 Resource Limits

A **limit** defines the maximum amount of a resource that the container is allowed to consume.

For this task:

```text
CPU:    100m
Memory: 20Mi
```

---

### 🔹 CPU Units

Kubernetes CPU is commonly expressed in millicores.

```text
100m = 0.1 CPU core
```

---

### 🔹 Memory Units

`Mi` represents mebibytes.

```text
15Mi
20Mi
```

These are Kubernetes memory resource quantities.

---

## ⚠️ Common Mistakes to Avoid

- Using `15MB` instead of `15Mi`
- Using `100` instead of `100m`
- Putting `resources` outside the container definition
- Using `httpd` instead of explicitly specifying `httpd:latest`
- Incorrect container name
- Configuring Pod-level resources instead of container-level resources

---

## 🎤 Interview Questions

### Q1. What is a resource request in Kubernetes?

A resource request specifies the amount of CPU or memory required by a container and is used by the scheduler when deciding where to place the Pod.

---

### Q2. What is a resource limit?

A resource limit specifies the maximum amount of CPU or memory a container is allowed to consume.

---

### Q3. What happens when a container exceeds its memory limit?

The container can be terminated by Kubernetes due to an out-of-memory condition.

---

### Q4. What happens when a container reaches its CPU limit?

CPU usage is throttled rather than the container being immediately terminated.

---

### Q5. What does `100m` CPU mean?

`100m` means **100 millicores**, equivalent to:

```text
0.1 CPU core
```

---

### Q6. Why are resource requests important?

Requests help Kubernetes schedule Pods onto nodes with sufficient available resources.

---

## 📌 Final Configuration

```text
Kubernetes Cluster
       │
       ▼
    httpd-pod
       │
       ▼
httpd-container
       │
       ▼
httpd:latest

Resources
├── Requests
│   ├── CPU:    100m
│   └── Memory: 15Mi
│
└── Limits
    ├── CPU:    100m
    └── Memory: 20Mi
```

---

## 🚀 Final Result

✅ Pod `httpd-pod` created successfully

✅ Container `httpd-container` configured

✅ Image `httpd:latest` deployed

✅ CPU request: `100m`

✅ Memory request: `15Mi`

✅ CPU limit: `100m`

✅ Memory limit: `20Mi`

✅ Resource configuration verified using `kubectl`

---

# 🎉 Day 50 Completed Successfully!
