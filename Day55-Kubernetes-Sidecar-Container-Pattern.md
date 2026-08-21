# ☸️ Day 55 – Kubernetes Sidecar Container Pattern

## 📌 Scenario

The Nautilus DevOps team needed to ship Nginx access and error logs to a log aggregation service without using persistent storage.

To follow the **Separation of Concerns** principle, a second container was deployed alongside Nginx to read and process the logs.

A shared `emptyDir` volume was used so both containers could access the same log files.

---

## 🎯 Objectives

- Create a Pod named `webserver`
- Deploy `nginx:latest`
- Create a sidecar container using `ubuntu:latest`
- Share Nginx logs between containers
- Use an `emptyDir` volume
- Configure a native Kubernetes sidecar container
- Mount `/var/log/nginx` in both containers

---

## 🛠️ Task Requirements

| Component | Configuration |
|---|---|
| Pod | `webserver` |
| Volume | `shared-logs` |
| Volume Type | `emptyDir` |
| Main Container | `nginx-container` |
| Main Image | `nginx:latest` |
| Sidecar | `sidecar-container` |
| Sidecar Image | `ubuntu:latest` |
| Mount Path | `/var/log/nginx` |

---

## 📝 Kubernetes YAML

Created `webserver.yaml`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webserver

spec:
  volumes:
    - name: shared-logs
      emptyDir: {}

  containers:
    - name: nginx-container
      image: nginx:latest
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx

  initContainers:
    - name: sidecar-container
      image: ubuntu:latest
      restartPolicy: Always
      command:
        - sh
        - -c
        - "while true; do cat /var/log/nginx/access.log /var/log/nginx/error.log; sleep 30; done"
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx
```

---

## 🚀 Deployment

Delete the previous Pod if required:

```bash
kubectl delete pod webserver
```

Create the Pod:

```bash
kubectl apply -f webserver.yaml
```

---

## 🔍 Verification

### Check Pod Status

```bash
kubectl get pod webserver
```

Expected:

```text
NAME        READY   STATUS    RESTARTS   AGE
webserver   2/2     Running   0          ...
```

### Check Pod Configuration

```bash
kubectl describe pod webserver
```

Verify:

```text
nginx-container
Image: nginx:latest
```

and:

```text
sidecar-container
Image: ubuntu:latest
```

Both containers should have:

```text
/var/log/nginx from shared-logs
```

### Verify the Volume

```bash
kubectl get pod webserver -o yaml
```

Expected:

```yaml
volumes:
  - name: shared-logs
    emptyDir: {}
```

---

## ⚠️ Problem Faced

Initially, the sidecar container was configured under the normal `containers` section.

The lab checker reported:

```text
'sidecar-container' doesn't exist
```

and:

```text
Image used is not 'ubuntu:latest' for 'sidecar-container'
```

### 🔧 Root Cause

The task specifically expected `sidecar-container` to be configured as a **Kubernetes native sidecar**.

The corrected configuration was:

```yaml
initContainers:
  - name: sidecar-container
    image: ubuntu:latest
    restartPolicy: Always
```

The `restartPolicy: Always` allows the init container to behave as a long-running sidecar.

---

## 🧠 Key Learnings

### 1. What is a Sidecar Container?

A sidecar is a container that runs alongside the main application container and provides supporting functionality.

In this task:

```text
Nginx
  ↓
Serves web application
```

```text
Sidecar
  ↓
Reads Nginx logs
```

### 2. What is `emptyDir`?

`emptyDir` creates temporary storage shared between containers in the same Pod.

```yaml
volumes:
  - name: shared-logs
    emptyDir: {}
```

The volume exists for the lifetime of the Pod.

### 3. Why Share `/var/log/nginx`?

Nginx writes:

```text
/var/log/nginx/access.log
/var/log/nginx/error.log
```

The sidecar mounts the same directory and can read those logs.

```text
             webserver Pod
                  │
        ┌─────────┴─────────┐
        │                   │
   nginx-container    sidecar-container
        │                   │
        └───────┬───────────┘
                │
          shared-logs
           emptyDir
                │
        /var/log/nginx
```

### 4. Native Kubernetes Sidecar

A long-running sidecar can be defined under `initContainers` with:

```yaml
restartPolicy: Always
```

This allows the container to start as a sidecar and continue running alongside the application container.

---

## 🎤 Interview Questions

### Q1. What is the Sidecar pattern?

The Sidecar pattern runs an additional container alongside the main application container to provide supporting functionality such as logging, monitoring, proxying, or security.

### Q2. Why use `emptyDir`?

`emptyDir` provides temporary storage that can be shared between containers within the same Pod.

### Q3. Can two containers in the same Pod share a volume?

Yes. Containers in the same Pod can mount the same Kubernetes volume.

### Q4. What is the purpose of `restartPolicy: Always` for a native sidecar?

It allows the sidecar defined in `initContainers` to continue running instead of completing before the main container starts.

### Q5. What happens to `emptyDir` when the Pod is deleted?

The `emptyDir` data is deleted along with the Pod.

---

## 📌 Final Result

```text
                    Kubernetes Pod
                       webserver
                           │
             ┌─────────────┴─────────────┐
             │                           │
      nginx-container              sidecar-container
        nginx:latest                  ubuntu:latest
             │                           │
             │                           │
             └──────────┬────────────────┘
                        │
                  shared-logs
                    emptyDir
                        │
                 /var/log/nginx
                        │
             ┌──────────┴──────────┐
             │                     │
        access.log             error.log
```

---

## ✅ Completion

- ✅ Pod `webserver` created
- ✅ `nginx:latest` deployed
- ✅ `sidecar-container` configured
- ✅ `ubuntu:latest` used
- ✅ `shared-logs` created with `emptyDir`
- ✅ Volume mounted at `/var/log/nginx`
- ✅ Native Kubernetes sidecar configured
- ✅ Pod running successfully

# 🎉 Day 55 Completed Successfully! 🚀
