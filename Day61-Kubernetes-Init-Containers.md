# ☸️ Day 61 – Kubernetes Init Containers

## 📌 Scenario

The Nautilus DevOps team needed to deploy applications that require some configuration or preparation before the main application container starts.

To handle these prerequisites, an **Init Container** was used. The Init Container creates a file in a shared volume, and the main container continuously reads that file.

---

## 🎯 Objectives

- Create a Deployment named `ic-deploy-xfusion`
- Configure 1 replica
- Use the label `app: ic-xfusion`
- Create an Init Container named `ic-msg-xfusion`
- Use `debian:latest`
- Create a file using the Init Container
- Create a main container named `ic-main-xfusion`
- Use `debian:latest`
- Share data using an `emptyDir` volume
- Verify the main container can read the file created by the Init Container

---

## 🛠️ Tasks Performed

### ✅ 1. Create the YAML File

Created:

```bash
vi ic-deploy.yaml
```

Configuration:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ic-deploy-xfusion
  labels:
    app: ic-xfusion

spec:
  replicas: 1

  selector:
    matchLabels:
      app: ic-xfusion

  template:
    metadata:
      labels:
        app: ic-xfusion

    spec:
      initContainers:
        - name: ic-msg-xfusion
          image: debian:latest
          command:
            - /bin/bash
            - -c
            - 'echo Init Done - Welcome to xFusionCorp Industries > /ic/official'
          volumeMounts:
            - name: ic-volume-xfusion
              mountPath: /ic

      containers:
        - name: ic-main-xfusion
          image: debian:latest
          command:
            - /bin/bash
            - -c
            - 'while true; do cat /ic/official; sleep 5; done'
          volumeMounts:
            - name: ic-volume-xfusion
              mountPath: /ic

      volumes:
        - name: ic-volume-xfusion
          emptyDir: {}
```

---

## ⚠️ Mistake Faced

Initially, the volume field was incorrectly written as:

```yaml
volume:
```

Kubernetes returned:

```text
Deployment in version "v1" cannot be handled as a Deployment:
strict decoding error:
unknown field "spec.template.spec.volume"
```

### 🔧 Fix

Changed:

```yaml
volume:
```

to:

```yaml
volumes:
```

After correcting the field name, the Deployment configuration was accepted by Kubernetes.

---

## 🚀 2. Create the Deployment

Applied the YAML:

```bash
kubectl apply -f ic-deploy.yaml
```

The Deployment was successfully created.

---

## 🔍 3. Verify Deployment

```bash
kubectl get deployment ic-deploy-xfusion
```

Expected:

```text
NAME                READY   UP-TO-DATE   AVAILABLE
ic-deploy-xfusion   1/1     1            1
```

---

## 🔍 4. Verify Pod

```bash
kubectl get pods -l app=ic-xfusion
```

Expected:

```text
ic-deploy-xfusion-xxxxx   1/1   Running
```

---

## 📋 5. Verify Main Container Output

Used:

```bash
kubectl logs -l app=ic-xfusion -c ic-main-xfusion
```

Expected output:

```text
Init Done - Welcome to xFusionCorp Industries
```

The message is printed repeatedly because the main container executes:

```bash
while true; do cat /ic/official; sleep 5; done
```

---

## 🧠 How the Init Container Works

The Init Container runs first:

```text
ic-msg-xfusion
       │
       │ creates
       ▼
/ic/official
       │
       ▼
ic-volume-xfusion
       │
       ▼
    emptyDir
       │
       ▼
ic-main-xfusion
       │
       │ reads
       ▼
/ic/official
```

The Init Container creates:

```text
/ic/official
```

with the content:

```text
Init Done - Welcome to xFusionCorp Industries
```

The main container then reads the same file from the shared volume.

---

## 🧠 Key Learnings

- Init Containers run before the main application containers.
- Init Containers are useful for initialization and prerequisite tasks.
- An Init Container must successfully complete before the main container starts.
- Containers in the same Pod can share an `emptyDir` volume.
- `volumeMounts` defines where a volume is mounted inside a container.
- `volumes` defines the actual volume available to the Pod.
- YAML field names must be exact because Kubernetes performs strict validation.

---

## 🎤 Interview Questions

### Q1. What is an Init Container?

An Init Container is a container that runs before the main application containers in a Pod and performs initialization tasks.

### Q2. Why use an Init Container?

Init Containers can perform tasks such as:

- Preparing configuration
- Creating files
- Downloading dependencies
- Waiting for required services
- Performing initialization work

### Q3. Do Init Containers run continuously?

No. Normally, an Init Container completes its task and exits successfully before the main container starts.

### Q4. How did the Init Container share its file with the main container?

Both containers mounted the same:

```text
ic-volume-xfusion
```

volume using:

```yaml
emptyDir: {}
```

### Q5. What is the difference between `volumes` and `volumeMounts`?

`volumes` defines the storage at the Pod level.

`volumeMounts` defines where that storage is mounted inside a specific container.

Example:

```yaml
volumes:
  - name: ic-volume-xfusion
    emptyDir: {}
```

and:

```yaml
volumeMounts:
  - name: ic-volume-xfusion
    mountPath: /ic
```

---

## 📌 Final Configuration

| Component | Configuration |
|---|---|
| Deployment | `ic-deploy-xfusion` |
| Replicas | `1` |
| Label | `app: ic-xfusion` |
| Init Container | `ic-msg-xfusion` |
| Init Image | `debian:latest` |
| Main Container | `ic-main-xfusion` |
| Main Image | `debian:latest` |
| Volume | `ic-volume-xfusion` |
| Volume Type | `emptyDir` |
| Mount Path | `/ic` |

---

## 🔄 Execution Flow

```text
                 Deployment
                     │
                     ▼
              Pod ic-xfusion
                     │
                     ▼
          ┌─────────────────────┐
          │   Init Container    │
          │   ic-msg-xfusion    │
          │    debian:latest    │
          └──────────┬──────────┘
                     │
              Creates /ic/official
                     │
                     ▼
              ic-volume-xfusion
                   emptyDir
                     │
                     ▼
          ┌─────────────────────┐
          │   Main Container    │
          │   ic-main-xfusion   │
          │    debian:latest    │
          └──────────┬──────────┘
                     │
                     ▼
             Reads /ic/official
                     │
                     ▼
        Init Done - Welcome to
          xFusionCorp Industries
```

---

## 🚀 Final Result

✅ Deployment `ic-deploy-xfusion` created

✅ 1 replica configured

✅ `app: ic-xfusion` label configured

✅ Init Container `ic-msg-xfusion` created

✅ `debian:latest` used

✅ Main Container `ic-main-xfusion` created

✅ `debian:latest` used

✅ Shared `emptyDir` volume configured

✅ File created by Init Container

✅ Main container successfully reads the file

✅ YAML `volume` error identified and fixed

# 🎉 Day 61 Completed Successfully! 🚀
