# Day 62 – Kubernetes Secrets 🔐

## 📌 Task

The Nautilus DevOps team needed to securely store license/password information inside the Kubernetes cluster. The requirement was to use a **Kubernetes Secret**, consume it inside a Pod, and mount the Secret as a file.

---

## 🎯 Objectives

- Create a generic Kubernetes Secret named `blog`.
- Store the existing `/opt/blog.txt` file inside the Secret.
- Create a Pod named `secret-xfusion`.
- Use `ubuntu:latest` as the container image.
- Keep the container running using a `sleep` command.
- Mount the Secret at `/opt/games`.
- Verify the Secret file from inside the container.

---

## 🛠️ Step 1: Check the Secret File

The existing file was:

```bash
cat /opt/blog.txt
```

This file contained the password/license information that needed to be stored securely.

---

## 🔐 Step 2: Create the Kubernetes Secret

Created a generic Secret named `blog` using the file:

```bash
kubectl create secret generic blog --from-file=/opt/blog.txt
```

Verify:

```bash
kubectl get secret blog
```

The Secret uses the filename as its key:

```text
blog.txt
```

---

## 📄 Step 3: Create the Pod Manifest

Created `secret-xfusion.yaml`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-xfusion

spec:
  containers:
    - name: secret-container-xfusion
      image: ubuntu:latest
      command:
        - /bin/bash
        - -c
        - "sleep 3600"
      volumeMounts:
        - name: secret-volume
          mountPath: /opt/games

  volumes:
    - name: secret-volume
      secret:
        secretName: blog
```

---

## 🚀 Step 4: Create the Pod

```bash
kubectl apply -f secret-xfusion.yaml
```

Verify:

```bash
kubectl get pod secret-xfusion
```

Expected status:

```text
NAME             READY   STATUS    RESTARTS   AGE
secret-xfusion   1/1     Running   0          ...
```

---

## 🔍 Step 5: Access the Container

Once the Pod was in the `Running` state:

```bash
kubectl exec -it secret-xfusion -c secret-container-xfusion -- bash
```

---

## 📂 Step 6: Verify the Mounted Secret

Inside the container:

```bash
ls -l /opt/games
```

The Secret file was available:

```text
blog.txt
```

Read the file:

```bash
cat /opt/games/blog.txt
```

The output matched the original `/opt/blog.txt` content.

Exit the container:

```bash
exit
```

---

## 🏗️ Architecture

```text
                  Kubernetes Cluster
                         │
                         ▼
                ┌─────────────────┐
                │ Secret: blog    │
                │                 │
                │ blog.txt        │
                │ (license data)  │
                └────────┬────────┘
                         │
                         │ Secret Volume
                         ▼
              ┌──────────────────────┐
              │ Pod: secret-xfusion  │
              │                      │
              │ ubuntu:latest        │
              │                      │
              │ /opt/games/          │
              │    └── blog.txt      │
              └──────────────────────┘
```

---

## 🧠 Key Learnings

### 1. Kubernetes Secrets

Secrets are Kubernetes objects designed to store sensitive information such as:

- Passwords
- API keys
- Tokens
- Certificates
- License information

### 2. Creating a Secret from a File

```bash
kubectl create secret generic blog --from-file=/opt/blog.txt
```

Kubernetes creates a Secret containing the file's contents.

### 3. Mounting Secrets as Files

A Secret can be mounted into a container using:

```yaml
volumes:
  - name: secret-volume
    secret:
      secretName: blog
```

and:

```yaml
volumeMounts:
  - name: secret-volume
    mountPath: /opt/games
```

The resulting file becomes:

```text
/opt/games/blog.txt
```

### 4. Secret vs ConfigMap

| Feature | Secret | ConfigMap |
|---|---|---|
| Intended for | Sensitive data | Non-sensitive configuration |
| Passwords | ✅ | ❌ |
| API tokens | ✅ | ❌ |
| Application configuration | Sometimes | ✅ |
| Can be mounted as files | ✅ | ✅ |
| Base64 encoded in manifest representation | ✅ | ❌ |

> **Important:** Base64 encoding is not encryption. Kubernetes Secret data should be protected with appropriate cluster security controls.

---

## 💡 Useful Commands

### List Secrets

```bash
kubectl get secrets
```

### View Secret Details

```bash
kubectl describe secret blog
```

### View Secret YAML

```bash
kubectl get secret blog -o yaml
```

### Check Pod

```bash
kubectl get pod secret-xfusion
```

### Execute into Container

```bash
kubectl exec -it secret-xfusion -c secret-container-xfusion -- bash
```

### Check Mounted Secret

```bash
ls -l /opt/games
```

### Read Secret File

```bash
cat /opt/games/blog.txt
```

---

## 🎤 Interview Questions

### Q1. What is a Kubernetes Secret?

A Kubernetes Secret is an object used to store sensitive information such as passwords, tokens, keys, and certificates.

### Q2. How can you create a Secret from a file?

```bash
kubectl create secret generic blog --from-file=/opt/blog.txt
```

### Q3. How can a Secret be consumed by a Pod?

A Secret can be consumed as:

- Environment variables
- Mounted files through a volume

### Q4. What happens when a Secret is mounted as a volume?

Each Secret key becomes a file inside the specified mount directory.

For this task:

```text
Secret key: blog.txt
        ↓
Mount path: /opt/games
        ↓
Container file: /opt/games/blog.txt
```

### Q5. Are Kubernetes Secrets encrypted by Base64?

**No.** Base64 is an encoding mechanism, not encryption. Additional Kubernetes security mechanisms, including encryption at rest, should be configured to protect Secret data.

---

## ✅ Final Result

| Requirement | Status |
|---|---|
| Secret `blog` created | ✅ |
| `/opt/blog.txt` stored in Secret | ✅ |
| Pod `secret-xfusion` created | ✅ |
| Container `secret-container-xfusion` | ✅ |
| Image `ubuntu:latest` | ✅ |
| Pod Running | ✅ |
| Secret mounted at `/opt/games` | ✅ |
| `blog.txt` verified inside container | ✅ |

---

# 🎉 Day 62 Completed Successfully!

**Topic:** Kubernetes Secrets  
**Skills:** Secret Creation, Secret Volumes, Pod Configuration, Secure Configuration Management, `kubectl exec` Verification
