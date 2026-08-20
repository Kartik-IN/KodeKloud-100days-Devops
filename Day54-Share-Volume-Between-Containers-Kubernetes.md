# ☸️ Day 54 – Share Volume Between Containers in Kubernetes

## 📌 Scenario

The Nautilus DevOps team needed to deploy an application using multiple containers inside a Kubernetes Pod.

The requirement was to create a shared volume so that both containers could access the same temporary data.

---

## 🎯 Objectives

- Create a Kubernetes Pod with multiple containers
- Use `fedora:latest` images
- Create and configure an `emptyDir` shared volume
- Mount the same volume at different paths
- Create a file in the first container
- Verify that the file is accessible from the second container

---

## 🛠️ Tasks Performed

### ✅ 1. Create Kubernetes YAML

Created the manifest:

```bash
vi volume-share.yaml
```

Configuration:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: volume-share-nautilus

spec:
  containers:

  - name: volume-container-nautilus-1
    image: fedora:latest
    command: ["/bin/bash", "-c", "sleep 3600"]
    volumeMounts:
    - name: volume-share
      mountPath: /tmp/media

  - name: volume-container-nautilus-2
    image: fedora:latest
    command: ["/bin/bash", "-c", "sleep 3600"]
    volumeMounts:
    - name: volume-share
      mountPath: /tmp/demo

  volumes:
  - name: volume-share
    emptyDir: {}
```

---

### ✅ 2. Create the Pod

```bash
kubectl apply -f volume-share.yaml
```

Output:

```text
pod/volume-share-nautilus created
```

---

### ✅ 3. Verify Pod Status

```bash
kubectl get pod volume-share-nautilus
```

Verified that both containers were running:

```text
volume-share-nautilus   2/2   Running
```

---

### ✅ 4. Create File in First Container

Created `media.txt` inside the first container:

```bash
kubectl exec volume-share-nautilus -c volume-container-nautilus-1 -- sh -c 'echo "Welcome to xFusionCorp Industries" > /tmp/media/media.txt'
```

---

### ✅ 5. Verify File in First Container

```bash
kubectl exec volume-share-nautilus -c volume-container-nautilus-1 -- cat /tmp/media/media.txt
```

Output:

```text
Welcome to xFusionCorp Industries
```

---

### ✅ 6. Verify Shared File in Second Container

Checked the mounted directory:

```bash
kubectl exec volume-share-nautilus -c volume-container-nautilus-2 -- ls -l /tmp/demo/
```

Confirmed:

```text
media.txt
```

Then verified the contents:

```bash
kubectl exec volume-share-nautilus -c volume-container-nautilus-2 -- cat /tmp/demo/media.txt
```

Output:

```text
Welcome to xFusionCorp Industries
```

---

## 🧠 How the Shared Volume Works

Both containers use the same Kubernetes volume:

```text
                 volume-share
                  emptyDir
                     │
          ┌──────────┴──────────┐
          │                     │
     Container 1           Container 2
          │                     │
     /tmp/media            /tmp/demo
          │                     │
      media.txt  ───────────► media.txt
```

The mount paths are different, but both paths point to the same `emptyDir` volume.

---

## 🧠 Key Learnings

- A Kubernetes Pod can contain multiple containers.
- Containers inside the same Pod can share storage.
- `emptyDir` creates temporary storage for containers in a Pod.
- The same volume can be mounted at different paths in different containers.
- `kubectl exec` allows commands to be executed inside a specific container.
- Shared volumes are useful when containers need to exchange temporary files or data.
- Data stored in an `emptyDir` volume exists as long as the Pod exists.

---

## 🎤 Interview Questions

### Q1. What is `emptyDir`?

`emptyDir` is a temporary Kubernetes volume created when a Pod is assigned to a node. It can be shared between containers within the same Pod.

### Q2. Can multiple containers mount the same volume?

Yes. Multiple containers in the same Pod can mount and share the same volume.

### Q3. Why were different mount paths used?

Each container can mount the same volume at a different location. In this task:

```text
Container 1 → /tmp/media
Container 2 → /tmp/demo
```

### Q4. What happens to `emptyDir` when the Pod is deleted?

The `emptyDir` data is deleted along with the Pod.

### Q5. Why was `sleep 3600` used?

The Fedora container would otherwise exit after starting. The sleep command keeps the containers running so they can be accessed using `kubectl exec`.

---

## 📌 Final Configuration

```text
Kubernetes Pod
│
├── volume-container-nautilus-1
│   ├── Image: fedora:latest
│   └── Mount: /tmp/media
│
├── volume-container-nautilus-2
│   ├── Image: fedora:latest
│   └── Mount: /tmp/demo
│
└── volume-share
    └── Type: emptyDir
```

File created:

```text
/tmp/media/media.txt
```

Accessible from:

```text
/tmp/demo/media.txt
```

---

## 🚀 Final Result

✅ Pod `volume-share-nautilus` created

✅ Two Fedora containers running

✅ `volume-share` configured as `emptyDir`

✅ Shared volume mounted in both containers

✅ `media.txt` created in Container 1

✅ File successfully accessed from Container 2

✅ Shared storage verified successfully

# 🎉 Day 54 Completed Successfully!
