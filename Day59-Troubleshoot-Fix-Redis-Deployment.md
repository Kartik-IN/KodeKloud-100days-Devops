# ☸️ Day 59 – Troubleshoot and Fix Redis Deployment

## 📌 Scenario

The Nautilus DevOps team had an existing Redis application deployed on a Kubernetes cluster.

The application was previously working correctly, but after changes were made to the deployment, the Redis Pod stopped running.

The task was to investigate the issue, identify the configuration mistakes, and restore the application.

---

## 🎯 Objectives

- Troubleshoot the `redis-deployment`
- Identify why the Redis Pod was not starting
- Fix the incorrect ConfigMap reference
- Fix the incorrect Redis image tag
- Verify that the Redis Pod returns to the `Running` state

---

## 🔍 1. Check the Deployment

The deployment was inspected using:

```bash
kubectl describe deployment redis-deployment
```

The output showed:

```text
Image: redis:alpin
```

and:

```text
ConfigMap:
  Name: redis-conig
```

Both contained spelling mistakes.

---

## 🔍 2. Inspect the Pod

Checked the Redis Pod:

```bash
kubectl describe pod -l app=redis
```

The Pod was in:

```text
Status: Pending
```

The container was stuck in:

```text
ContainerCreating
```

---

## ❌ Problem Identified

The most important error appeared in the Pod Events:

```text
FailedMount
```

Specifically:

```text
MountVolume.SetUp failed for volume "config" :
configmap "redis-conig" not found
```

### Root Cause

The Deployment was trying to mount a ConfigMap named:

```text
redis-conig
```

but that ConfigMap did not exist.

The correct ConfigMap name was:

```text
redis-config
```

There was also a typo in the Redis image:

```text
redis:alpin
```

The correct image was:

```text
redis:alpine
```

---

## 🛠️ 3. Fix the Deployment

Edited the Deployment:

```bash
kubectl edit deployment redis-deployment
```

Changed the Redis image from:

```yaml
image: redis:alpin
```

to:

```yaml
image: redis:alpine
```

Changed the ConfigMap from:

```yaml
configMap:
  name: redis-conig
```

to:

```yaml
configMap:
  name: redis-config
```

---

## 🔄 4. Verify the New Pod

Checked the Pods:

```bash
kubectl get pods -l app=redis
```

The new Redis Pod successfully started.

Expected:

```text
redis-deployment-xxxxx   1/1   Running
```

---

## 🔍 5. Verify Deployment

```bash
kubectl get deployment redis-deployment
```

Expected:

```text
NAME              READY   UP-TO-DATE   AVAILABLE
redis-deployment  1/1     1            1
```

---

## ⚠️ Mistakes Found

### ❌ Mistake 1 – Incorrect Redis Image Tag

Used:

```text
redis:alpin
```

Correct:

```text
redis:alpine
```

A small typo in an image tag can prevent Kubernetes from pulling the required image.

---

### ❌ Mistake 2 – Incorrect ConfigMap Name

Used:

```text
redis-conig
```

Correct:

```text
redis-config
```

This was the **confirmed reason** the Pod was stuck in `ContainerCreating`.

Kubernetes reported:

```text
configmap "redis-conig" not found
```

---

## 🧠 Key Learnings

- `kubectl describe pod` is extremely useful for troubleshooting Kubernetes issues.
- The **Events** section often contains the actual root cause.
- `FailedMount` usually indicates a problem mounting a volume.
- ConfigMap names must exactly match the referenced resource.
- Container image names and tags must also be exact.
- A Pod can remain in `Pending` or `ContainerCreating` because of volume or image-related problems.
- Always check logs and Events before changing Kubernetes configuration.

---

## 🎤 Interview Questions

### Q1. How do you troubleshoot a Pod that is not running?

Start with:

```bash
kubectl get pods
```

Then:

```bash
kubectl describe pod <pod-name>
```

Check the **Events** section for errors.

Depending on the state, also use:

```bash
kubectl logs <pod-name>
```

---

### Q2. What does `FailedMount` mean?

`FailedMount` means Kubernetes was unable to mount a required volume into the Pod.

In this case, the referenced ConfigMap did not exist.

---

### Q3. Why did the ConfigMap error prevent Redis from starting?

The Redis container depended on the ConfigMap volume. Since Kubernetes could not find the specified ConfigMap, it could not finish setting up the container.

---

### Q4. Why is exact naming important in Kubernetes?

Kubernetes resources are referenced by their names. A typo such as:

```text
redis-conig
```

instead of:

```text
redis-config
```

causes the reference to fail.

---

## 📌 Before vs After

| Configuration | Before ❌ | After ✅ |
|---|---|---|
| Redis Image | `redis:alpin` | `redis:alpine` |
| ConfigMap | `redis-conig` | `redis-config` |
| Pod Status | `Pending` | `Running` |
| Available Replicas | `0` | `1` |

---

## 🔧 Troubleshooting Flow

```text
Redis Pod not running
        │
        ▼
kubectl get pods
        │
        ▼
Pod stuck in ContainerCreating
        │
        ▼
kubectl describe pod
        │
        ▼
Check Events
        │
        ▼
FailedMount
        │
        ▼
ConfigMap "redis-conig" not found
        │
        ▼
Fix ConfigMap reference
        │
        ▼
Fix redis image typo
        │
        ▼
Pod recreated
        │
        ▼
Redis Pod Running ✅
```

---

## 🚀 Final Result

- ✅ `redis-deployment` successfully troubleshot
- ✅ Root cause identified using Pod Events
- ✅ Incorrect ConfigMap reference fixed
- ✅ Incorrect Redis image tag fixed
- ✅ Redis Pod returned to `Running`
- ✅ Deployment returned to `1/1` available

# 🎉 Day 59 Completed Successfully! 🚀
