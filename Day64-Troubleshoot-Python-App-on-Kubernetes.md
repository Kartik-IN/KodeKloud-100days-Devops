# ☸️ Day 64 – Troubleshoot Python App on Kubernetes

## 📌 Scenario

The Nautilus DevOps team had an existing Python Flask application deployed on a Kubernetes cluster. Due to a misconfiguration, the application was not coming up.

The task was to identify and fix the issues and make the application accessible through the specified NodePort.

---

## 🎯 Objectives

- Troubleshoot a Kubernetes Deployment
- Identify an incorrect container image
- Fix the Python Flask application deployment
- Verify the Flask application port
- Correct the Kubernetes Service target port
- Expose the application using NodePort `32345`

---

## 🛠️ Tasks Performed

### ✅ 1. Check the Python Pod

Initially checked the Pod:

```bash
kubectl describe pod -l app=python_app
```

The Pod was in:

```text
Status: Pending
```

The container showed:

```text
State: Waiting
Reason: ImagePullBackOff
```

---

### ✅ 2. Identify the Image Issue

The Deployment was using the incorrect image:

```yaml
image: poroko/flask-app-demo
```

The Kubernetes events showed:

```text
Failed to pull image "poroko/flask-app-demo"
```

The required image was:

```yaml
image: poroko/flask-demo-app
```

The Deployment image was corrected.

---

### ✅ 3. Verify the Pod

After fixing the image, checked the Pods:

```bash
kubectl get pods
```

The new Pod was running successfully:

```text
python-deployment-datacenter-57d654488b-rf9t5   1/1   Running   0   22s
```

---

### ✅ 4. Check the Existing Service

Checked the available Services:

```bash
kubectl get svc
```

The Python application Service was:

```text
python-service-datacenter
```

It was already configured with the required NodePort:

```text
8080:32345/TCP
```

---

### ✅ 5. Identify the TargetPort Issue

Inspected the Service:

```bash
kubectl describe svc python-service-datacenter
```

The Service was configured with:

```text
Port:       8080/TCP
TargetPort: 8080/TCP
NodePort:   32345/TCP
```

However, the Python Flask container was listening on:

```text
5000/TCP
```

Therefore, the Service `targetPort` needed to be changed from `8080` to `5000`.

---

### ✅ 6. Fix the Service

Edited the Service:

```bash
kubectl edit svc python-service-datacenter
```

Updated the port configuration:

```yaml
ports:
  - port: 8080
    targetPort: 5000
    nodePort: 32345
```

---

## 🔍 Verification

Checked the Service again:

```bash
kubectl describe svc python-service-datacenter
```

Expected configuration:

```text
TargetPort: 5000/TCP
NodePort:   32345/TCP
Endpoints:  <Pod-IP>:5000
```

Also verified the Pod:

```bash
kubectl get pods
```

Expected:

```text
1/1   Running
```

---

## ⚠️ Issues Found

### ❌ Issue 1 – Incorrect Docker Image

Incorrect:

```text
poroko/flask-app-demo
```

Correct:

```text
poroko/flask-demo-app
```

This caused:

```text
ImagePullBackOff
```

---

### ❌ Issue 2 – Incorrect Service TargetPort

Incorrect:

```yaml
targetPort: 8080
```

Correct:

```yaml
targetPort: 5000
```

The Flask application runs on port `5000`.

---

## 🧠 Key Learnings

- `ImagePullBackOff` can indicate an incorrect or unavailable container image.
- Kubernetes Pods must be running before the application can receive traffic.
- `targetPort` specifies the port on which the application container is listening.
- `nodePort` exposes a Service externally through a port on the Kubernetes node.
- The Service selector must correctly match the Pod labels.
- The `nodePort` can remain `32345` while the application's `targetPort` is `5000`.

---

## 📋 Final Configuration

| Component | Configuration |
|---|---|
| Deployment | `python-deployment-datacenter` |
| Container | `python-container-datacenter` |
| Image | `poroko/flask-demo-app` |
| Application Port | `5000` |
| Service | `python-service-datacenter` |
| Service Type | `NodePort` |
| Service Port | `8080` |
| TargetPort | `5000` |
| NodePort | `32345` |

---

## 🚀 Final Architecture

```text
                    Kubernetes Cluster
                           │
                           ▼
              python-deployment-datacenter
                           │
                           ▼
                  Python Flask Pod
                           │
                    Port 5000
                           ▲
                           │
                    targetPort: 5000
                           │
                           ▼
              python-service-datacenter
                    Service Port 8080
                           │
                    NodePort 32345
                           │
                           ▼
                      Application
```

---

## 🎉 Day 64 Completed Successfully!

✅ Fixed incorrect Docker image

✅ Python Pod running successfully

✅ Identified Flask application port `5000`

✅ Fixed Service `targetPort`

✅ NodePort `32345` configured

✅ Python application successfully exposed
