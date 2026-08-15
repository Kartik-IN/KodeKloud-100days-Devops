# 🚀 Day 49 – Deploy Applications with Kubernetes Deployments

## 📌 Scenario

The Nautilus DevOps team continued moving applications to **Kubernetes** for better application management.

The task was to create a Kubernetes **Deployment** for the `httpd` application using the specified Docker image.

The deployment requirements were:

- Deployment name: `httpd`
- Application/container name: `httpd`
- Image: `httpd:latest`

---

## 🎯 Objectives

- Create a Kubernetes Deployment
- Use the `httpd:latest` image
- Understand the relationship between Deployments and Pods
- Verify the Deployment
- Verify the Pod created by the Deployment

---

## 🛠️ Tasks Performed

### ✅ 1. Create the Deployment

Created the Deployment using:

```bash
kubectl create deployment httpd --image=httpd:latest
```

Output:

```bash
deployment.apps/httpd created
```

---

### ✅ 2. Verify the Deployment

Checked the available Deployments:

```bash
kubectl get deployments
```

Expected output:

```bash
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
httpd   1/1     1            1           ...
```

The `httpd` Deployment was successfully created.

---

### ✅ 3. Check the Pod

A Deployment automatically creates and manages a Pod.

Checked the Pods:

```bash
kubectl get pods
```

Expected output:

```bash
NAME                     READY   STATUS    RESTARTS   AGE
httpd-xxxxxxxxxx-xxxxx   1/1     Running   0          ...
```

---

### ✅ 4. Inspect the Deployment

Used:

```bash
kubectl describe deployment httpd
```

Verified:

- Deployment name: `httpd`
- Container image: `httpd:latest`
- Pod template
- Replica information
- Deployment status

---

## 🔍 Verification

The Kubernetes resource hierarchy was:

```text
Kubernetes Cluster
       │
       ▼
   Deployment
      httpd
       │
       ▼
      Pod
       │
       ▼
   Container
       │
       ▼
  httpd:latest
```

The Deployment successfully created and managed the application Pod.

---

## 🧠 Key Learnings

- A Deployment manages application Pods in Kubernetes.
- Deployments provide a declarative way to manage applications.
- A Deployment automatically creates a ReplicaSet.
- The ReplicaSet creates and maintains Pods.
- If a managed Pod fails, the Deployment can recreate it.
- Using `httpd:latest` explicitly specifies the required image tag.
- Deployments are preferred over manually creating individual Pods for continuously running applications.

---

## 🎤 Interview Questions

### Q1. What is a Kubernetes Deployment?

A Deployment is a Kubernetes resource used to manage and maintain a desired number of application Pods.

---

### Q2. What happens when you create a Deployment?

The Deployment creates a ReplicaSet, which then creates and manages the required Pods.

```text
Deployment
    ↓
ReplicaSet
    ↓
Pod
    ↓
Container
```

---

### Q3. Difference between a Pod and a Deployment?

A **Pod** runs containers directly.

A **Deployment** manages Pods and provides features such as:

- Replica management
- Rolling updates
- Self-healing
- Version updates

---

### Q4. How can you check Deployments?

```bash
kubectl get deployments
```

---

### Q5. How can you inspect a Deployment?

```bash
kubectl describe deployment httpd
```

---

### Q6. Why specify `httpd:latest` instead of just `httpd`?

Specifying the tag makes the requested image version explicit.

```text
httpd:latest
```

consists of:

```text
Repository → httpd
Tag        → latest
```

---

## 📌 Useful Commands

### List Deployments

```bash
kubectl get deployments
```

### List Pods

```bash
kubectl get pods
```

### Describe Deployment

```bash
kubectl describe deployment httpd
```

### View Deployment YAML

```bash
kubectl get deployment httpd -o yaml
```

---

## 🚀 Final Result

✅ Deployment `httpd` created successfully

✅ Image `httpd:latest` configured

✅ Deployment created a Pod

✅ Pod reached `Running` state

✅ Deployment verified using `kubectl`

---

# 🎉 Day 49 Completed Successfully!

**Next:** Kubernetes Pod Resource Limits 🚀
