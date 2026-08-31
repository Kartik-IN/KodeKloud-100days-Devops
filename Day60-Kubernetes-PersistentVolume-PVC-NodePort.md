# ☸️ Day 60 – Kubernetes PersistentVolume, PVC and NodePort

## 📌 Scenario

The Nautilus DevOps team needed to create a Kubernetes template for a web application that requires persistent storage for application code.

The setup required a **PersistentVolume (PV)**, a **PersistentVolumeClaim (PVC)**, an Nginx Pod using the PVC, and a NodePort Service to expose the web server.

---

## 🎯 Objectives

- Create a PersistentVolume named `pv-devops`
- Create a PersistentVolumeClaim named `pvc-devops`
- Use `hostPath` storage
- Configure `ReadWriteOnce` access
- Deploy an Nginx Pod using the PVC
- Mount persistent storage at the Nginx document root
- Expose the application using a NodePort Service

---

## 🛠️ Tasks Performed

### ✅ 1. Create PersistentVolume

Created a PersistentVolume named:

```text
pv-devops
```

Configuration:

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-devops
spec:
  storageClassName: manual
  capacity:
    storage: 4Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /mnt/data
```

The PV provides:

```text
Storage     → 4Gi
StorageClass → manual
Access Mode → ReadWriteOnce
Volume Type → hostPath
Path        → /mnt/data
```

---

### ✅ 2. Create PersistentVolumeClaim

Created:

```text
pvc-devops
```

Configuration:

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-devops
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 2Gi
```

The PVC requests:

```text
2Gi
```

from the available `4Gi` PersistentVolume.

---

### ✅ 3. Create Nginx Pod

Created Pod:

```text
pod-devops
```

Container:

```text
container-devops
```

Image:

```text
nginx:latest
```

The PVC was mounted at the Nginx document root:

```text
/usr/share/nginx/html
```

Configuration:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-devops
  labels:
    app: web-devops
spec:
  containers:
    - name: container-devops
      image: nginx:latest
      ports:
        - containerPort: 80
      volumeMounts:
        - name: devops-storage
          mountPath: /usr/share/nginx/html
  volumes:
    - name: devops-storage
      persistentVolumeClaim:
        claimName: pvc-devops
```

---

### ✅ 4. Create NodePort Service

Created:

```text
web-devops
```

Service type:

```text
NodePort
```

NodePort:

```text
30008
```

Configuration:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-devops
spec:
  type: NodePort
  selector:
    app: web-devops
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30008
```

---

## 🚀 Deployment

All resources were created using:

```bash
kubectl apply -f pv-pvc-pod-service.yaml
```

Resources created:

```text
persistentvolume/pv-devops created
persistentvolumeclaim/pvc-devops created
pod/pod-devops created
service/web-devops created
```

---

## 🔍 Verification

### Check PersistentVolume

```bash
kubectl get pv pv-devops
```

Expected:

```text
pv-devops   4Gi   RWO   ...   Bound
```

---

### Check PersistentVolumeClaim

```bash
kubectl get pvc pvc-devops
```

Expected:

```text
pvc-devops   Bound   pv-devops   4Gi
```

The PVC successfully bound to:

```text
pv-devops
```

---

### Check Pod

```bash
kubectl get pod pod-devops
```

Expected:

```text
pod-devops   1/1   Running
```

---

### Check Service

```bash
kubectl get svc web-devops
```

Expected port mapping:

```text
80:30008/TCP
```

---

## 🧠 Storage Architecture

```text
                     Kubernetes Cluster
                            │
                            ▼
                    web-devops Service
                      NodePort :30008
                            │
                            ▼
                       pod-devops
                            │
                            ▼
                   container-devops
                      nginx:latest
                            │
                            ▼
                  /usr/share/nginx/html
                            │
                            ▼
                       pvc-devops
                            │
                            ▼
                        pv-devops
                            │
                            ▼
                        hostPath
                        /mnt/data
```

---

## 🧠 Key Learnings

- A **PersistentVolume (PV)** provides storage resources in Kubernetes.
- A **PersistentVolumeClaim (PVC)** requests storage from available PVs.
- A PVC can bind to a suitable PersistentVolume.
- `ReadWriteOnce` allows the volume to be mounted as read-write by a single node.
- `hostPath` uses a directory on the Kubernetes node as storage.
- Pods can mount a PVC using `persistentVolumeClaim`.
- Persistent storage can be mounted directly into an application's document root.
- A NodePort Service can expose the application outside the Kubernetes cluster.

---

## 🎤 Interview Questions

### Q1. What is a PersistentVolume?

A PersistentVolume is a storage resource provisioned for use by applications running in Kubernetes.

### Q2. What is a PersistentVolumeClaim?

A PersistentVolumeClaim is a request for storage made by a Kubernetes workload.

### Q3. What is the relationship between PV and PVC?

```text
Application
     ↓
   PVC
     ↓
    PV
     ↓
 Storage
```

The PVC requests storage and Kubernetes binds it to a suitable PV.

### Q4. What does `ReadWriteOnce` mean?

`ReadWriteOnce` allows a volume to be mounted as read-write by workloads on a single node.

### Q5. What is `hostPath`?

`hostPath` mounts a directory from the Kubernetes node's filesystem into a Pod.

### Q6. Why use a PVC instead of directly mounting the PV?

Pods normally consume storage through PVCs. This separates the application's storage request from the underlying storage implementation.

---

## 📌 Final Configuration

| Component | Configuration |
|---|---|
| PersistentVolume | `pv-devops` |
| PV Storage | `4Gi` |
| Storage Class | `manual` |
| Access Mode | `ReadWriteOnce` |
| Volume Type | `hostPath` |
| Host Path | `/mnt/data` |
| PersistentVolumeClaim | `pvc-devops` |
| PVC Request | `2Gi` |
| Pod | `pod-devops` |
| Container | `container-devops` |
| Image | `nginx:latest` |
| Mount Path | `/usr/share/nginx/html` |
| Service | `web-devops` |
| Service Type | `NodePort` |
| NodePort | `30008` |

---

## 🔄 Request Flow

```text
Client
  │
  │ :30008
  ▼
web-devops Service
  │
  │ :80
  ▼
pod-devops
  │
  ▼
container-devops
  │
  ▼
Nginx :80
  │
  ▼
/usr/share/nginx/html
  │
  ▼
pvc-devops
  │
  ▼
pv-devops
  │
  ▼
/mnt/data
```

---

## ✅ Final Result

- ✅ PersistentVolume `pv-devops` created
- ✅ `4Gi` storage configured
- ✅ `manual` storage class configured
- ✅ `ReadWriteOnce` access mode configured
- ✅ `hostPath /mnt/data` configured
- ✅ PVC `pvc-devops` created
- ✅ PVC successfully bound to the PV
- ✅ Pod `pod-devops` created
- ✅ `container-devops` running `nginx:latest`
- ✅ PVC mounted at Nginx document root
- ✅ NodePort Service `web-devops` created
- ✅ NodePort `30008` configured

# 🎉 Day 60 Completed Successfully! 🚀
