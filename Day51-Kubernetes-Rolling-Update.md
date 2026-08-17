# 🔄 Day 51 – Kubernetes Rolling Update

## 📌 Scenario

The Nautilus application development team introduced updates to an application currently running on the Kubernetes cluster.

The application was using the **Nginx web server**, and a new updated image was prepared:

```text
nginx:1.19
```

The existing Kubernetes Deployment was:

```text
nginx-deployment
```

The requirement was to perform a **rolling update** so that the application could be updated without deleting the existing Deployment or causing unnecessary downtime.

---

## 🎯 Objectives

- Update the existing `nginx-deployment`
- Replace the current Nginx image with `nginx:1.19`
- Perform the update using Kubernetes rolling-update functionality
- Monitor the rollout
- Ensure all Pods are operational after the update

---

## 🛠️ Tasks Performed

### ✅ 1. Check Existing Deployment

First, verified the existing Deployment:

```bash
kubectl get deployment nginx-deployment
```

This confirmed that the Deployment was already running in the cluster.

---

### ✅ 2. Check Existing Pods

Verified the Pods managed by the Deployment:

```bash
kubectl get pods
```

This helped confirm the initial state before performing the update.

---

### ✅ 3. Identify Container Configuration

Inspected the Deployment configuration:

```bash
kubectl get deployment nginx-deployment -o yaml
```

Verified the existing container name and image before making changes.

---

### ✅ 4. Perform Rolling Update

Updated the Deployment to use the new image:

```bash
kubectl set image deployment/nginx-deployment <container-name>=nginx:1.19
```

The existing Deployment was updated without deleting it.

---

### ✅ 5. Monitor Rollout

Checked the rollout progress:

```bash
kubectl rollout status deployment/nginx-deployment
```

The rollout completed successfully.

Expected output:

```text
deployment "nginx-deployment" successfully rolled out
```

---

### ✅ 6. Verify Pods

Checked the Pods after the update:

```bash
kubectl get pods
```

Confirmed that the Pods were operational.

Expected status:

```text
STATUS
Running
```

---

### ✅ 7. Verify Updated Image

Checked the Deployment:

```bash
kubectl describe deployment nginx-deployment
```

Verified that the application was now using:

```text
nginx:1.19
```

---

## 🔍 Rolling Update Flow

```text
Existing Deployment
        │
        ▼
   Old Nginx Pods
        │
        │  Rolling Update
        ▼
   New nginx:1.19 Pods
        │
        ▼
 Old Pods gradually
 replaced
        │
        ▼
 All Pods Running
```

Kubernetes gradually replaces old Pods with new Pods rather than removing all Pods at once.

---

## 🧠 Key Learnings

- Kubernetes Deployments support rolling updates by default
- `kubectl set image` can update the image of an existing Deployment
- Rolling updates allow applications to be updated without completely stopping the Deployment
- `kubectl rollout status` helps monitor update progress
- Always verify Pod status after an update
- The Deployment should be updated rather than deleted and recreated
- Rolling updates reduce application downtime during deployments
- Rolling updates maintain application availability during upgrades

---

## 🎤 Interview Questions

### Q1. What is a rolling update?

A rolling update gradually replaces old Pods with new Pods so that the application remains available during deployment.

---

### Q2. How do you update an image in an existing Deployment?

Using:

```bash
kubectl set image deployment/<deployment-name> <container-name>=<new-image>
```

---

### Q3. How do you monitor a rolling update?

```bash
kubectl rollout status deployment/nginx-deployment
```

---

### Q4. Why shouldn't we delete and recreate the Deployment?

Deleting the Deployment can cause unnecessary downtime and removes the benefits of Kubernetes' controlled rollout mechanism.

---

### Q5. How can you check the rollout history?

```bash
kubectl rollout history deployment/nginx-deployment
```

---

### Q6. What happens to the old Pods during a rolling update?

Kubernetes gradually terminates old Pods while creating new Pods with the updated configuration.

---

### Q7. What is the difference between a rolling update and a recreate strategy?

| Aspect | Rolling Update | Recreate |
|--------|---|---|
| **Downtime** | Minimal/None | Full downtime |
| **Pod Replacement** | Gradual | All at once |
| **Availability** | Maintained | Lost during update |
| **Deployment Strategy** | Default | Alternative |

---

## 📌 Final Configuration

```text
Kubernetes Cluster
        │
        ▼
nginx-deployment
        │
        ▼
   nginx:1.19
        │
        ▼
  Running Pods
```

---

## 🚀 Final Result

✅ Existing `nginx-deployment` updated

✅ Image changed to `nginx:1.19`

✅ Rolling update performed successfully

✅ Rollout status verified

✅ All application Pods operational

✅ No Deployment deletion required

---

# 🎉 Day 51 Completed Successfully!

**Next:** Kubernetes Deployment Rollback 🚀
