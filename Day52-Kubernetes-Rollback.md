# 🔙 Day 52 – Kubernetes Deployment Rollback

## 📌 Scenario

The Nautilus DevOps team deployed a new release of an application earlier in the day.

After the release, a customer reported a bug related to the new version. To restore the previously working version, the team needed to **rollback the Kubernetes Deployment to its previous revision**.

The existing Deployment was:

```text
nginx-deployment
```

---

## 🎯 Objectives

- Inspect the Deployment rollout history
- Identify the available revisions
- Rollback `nginx-deployment` to the previous revision
- Monitor the rollback process
- Verify that all Pods are operational
- Confirm that the previous application version has been restored

---

## 🛠️ Tasks Performed

### ✅ 1. Check Deployment Rollout History

First, checked the revision history:

```bash
kubectl rollout history deployment/nginx-deployment
```

This displayed the available Deployment revisions.

Example:

```text
deployment.apps/nginx-deployment

REVISION  CHANGE-CAUSE
1         <none>
2         <none>
```

The latest revision represented the recently deployed release.

---

### ✅ 2. Rollback to Previous Revision

Rolled back the Deployment using:

```bash
kubectl rollout undo deployment/nginx-deployment
```

This instructed Kubernetes to revert the Deployment to its previous revision.

---

### ✅ 3. Monitor the Rollback

Checked the rollback status:

```bash
kubectl rollout status deployment/nginx-deployment
```

Expected:

```text
deployment "nginx-deployment" successfully rolled out
```

This confirmed that the rollback completed successfully.

---

### ✅ 4. Verify Pods

Checked the Pods managed by the Deployment:

```bash
kubectl get pods
```

Verified that the Pods were operational:

```text
STATUS
Running
```

---

### ✅ 5. Verify Deployment

Inspected the Deployment:

```bash
kubectl describe deployment nginx-deployment
```

This helped verify that the Deployment had returned to its previous configuration.

---

### ✅ 6. Check Rollout History Again

Verified the revision history:

```bash
kubectl rollout history deployment/nginx-deployment
```

This confirmed that Kubernetes had recorded the rollback as part of the Deployment's revision history.

---

## 🔄 Rollback Flow

```text
             Kubernetes Deployment
                     │
                     ▼
                Revision 1
                     │
                     ▼
                Revision 2
              New Release
                     │
                     ▼
               🐛 Bug Found
                     │
                     ▼
             kubectl rollout undo
                     │
                     ▼
                Revision 1
              Previous Version
                     │
                     ▼
               Pods Running
```

---

## 🧠 Key Learnings

- Kubernetes Deployments maintain revision history
- A Deployment can be rolled back without manually recreating it
- `kubectl rollout undo` is used to revert a Deployment
- `kubectl rollout status` helps monitor the rollback
- Rollbacks are useful when a new release introduces bugs or unexpected behavior
- Kubernetes makes application version management easier through Deployment revisions
- Always verify Pod status after performing a rollback

---

## 🎤 Interview Questions

### Q1. What is a Kubernetes rollback?

A rollback restores a Deployment to a previous revision when the current release has problems.

---

### Q2. Which command is used to rollback a Deployment?

```bash
kubectl rollout undo deployment/nginx-deployment
```

---

### Q3. How do you check Deployment history?

```bash
kubectl rollout history deployment/nginx-deployment
```

---

### Q4. How do you monitor a rollback?

```bash
kubectl rollout status deployment/nginx-deployment
```

---

### Q5. Why are rollbacks important in DevOps?

Rollbacks provide a quick way to restore a previously working application version when a new deployment causes failures or bugs.

---

### Q6. What is the difference between rolling update and rollback?

A **rolling update** gradually replaces the old application version with a new version.

A **rollback** reverses that change and restores a previous version.

```text
Rolling Update:
Old Version → New Version

Rollback:
New Version → Previous Version
```

---

## 📌 Useful Commands

### View Deployment

```bash
kubectl get deployment nginx-deployment
```

### View Rollout History

```bash
kubectl rollout history deployment/nginx-deployment
```

### Rollback Deployment

```bash
kubectl rollout undo deployment/nginx-deployment
```

### Monitor Rollback

```bash
kubectl rollout status deployment/nginx-deployment
```

### Check Pods

```bash
kubectl get pods
```

### Inspect Deployment

```bash
kubectl describe deployment nginx-deployment
```

---

## 📌 Final Configuration

```text
Kubernetes Cluster
        │
        ▼
nginx-deployment
        │
        ▼
Previous Revision
        │
        ▼
   Running Pods
```

---

## 🚀 Final Result

✅ Deployment `nginx-deployment` identified

✅ Rollout history inspected

✅ Deployment rolled back to the previous revision

✅ Rollback status verified

✅ Pods confirmed operational

✅ Previous application version restored

---

# 🎉 Day 52 Completed Successfully!
