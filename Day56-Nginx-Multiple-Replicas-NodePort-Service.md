# ☸️ Day 56 – Deploy Nginx with Multiple Replicas and NodePort Service

## 📌 Scenario

The Nautilus development team was developing a static website that needed to be deployed on a Kubernetes cluster.

To provide **high availability and scalability**, the application was deployed using a Kubernetes Deployment with multiple replicas and exposed using a NodePort Service.

---

## 🎯 Objectives

- Create a Kubernetes Deployment named `nginx-deployment`
- Use the `nginx:latest` image
- Configure 3 replicas
- Name the container `nginx-container`
- Create a NodePort Service named `nginx-service`
- Configure NodePort `30011`
- Verify the deployment and service

---

## 🛠️ Tasks Performed

### ✅ 1. Create the Deployment Manifest

Created:

```bash
vi nginx-deployment.yaml
```

Configuration:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment

spec:
  replicas: 3

  selector:
    matchLabels:
      app: nginx

  template:
    metadata:
      labels:
        app: nginx

    spec:
      containers:
      - name: nginx-container
        image: nginx:latest
```

---

### ✅ 2. Create the Deployment

```bash
kubectl apply -f nginx-deployment.yaml
```

Output:

```text
deployment.apps/nginx-deployment created
```

---

### ✅ 3. Verify Deployment

```bash
kubectl get deployment nginx-deployment
```

Verified that 3 replicas were running:

```text
NAME              READY   UP-TO-DATE   AVAILABLE
nginx-deployment  3/3     3            3
```

---

### ✅ 4. Verify Pods

```bash
kubectl get pods
```

Confirmed that three Nginx Pods were running:

```text
nginx-deployment-xxxxx   1/1   Running
nginx-deployment-xxxxx   1/1   Running
nginx-deployment-xxxxx   1/1   Running
```

---

### ✅ 5. Create NodePort Service

Created:

```bash
vi nginx-service.yaml
```

Configuration:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service

spec:
  type: NodePort

  selector:
    app: nginx

  ports:
  - port: 80
    targetPort: 80
    nodePort: 30011
```

---

### ✅ 6. Create the Service

```bash
kubectl apply -f nginx-service.yaml
```

Output:

```text
service/nginx-service created
```

---

### ✅ 7. Verify Service

```bash
kubectl get service nginx-service
```

Verified:

```text
nginx-service   NodePort   ...   80:30011/TCP
```

The application was exposed through NodePort:

```text
30011
```

---

## 🧠 Architecture

```text
                    nginx-service
                     NodePort
                      :30011
                         │
             ┌───────────┼───────────┐
             ↓           ↓           ↓
          Pod 1        Pod 2        Pod 3
             │           │           │
      nginx-container nginx-container nginx-container
             │           │           │
        nginx:latest nginx:latest nginx:latest
```

The Kubernetes Service distributes traffic to the available Nginx Pods.

---

## 🧠 Key Learnings

- Kubernetes Deployments manage application replicas.
- Multiple replicas improve application availability.
- Deployments can automatically maintain the desired number of Pods.
- Kubernetes Services provide stable network access to Pods.
- A `NodePort` Service exposes an application through a port on each Kubernetes node.
- Service selectors connect the Service to matching Pods using labels.
- `replicas: 3` ensures three instances of the application are maintained.

---

## 🎤 Interview Questions

### Q1. Why use a Deployment instead of creating individual Pods?

A Deployment manages the desired number of replicas and can automatically replace failed Pods.

### Q2. Why were 3 replicas configured?

Multiple replicas improve availability and allow the application to handle traffic across multiple Pods.

### Q3. What is a NodePort Service?

A NodePort Service exposes an application on a specific port on each Kubernetes node.

### Q4. What is the purpose of the selector?

The Service selector identifies the Pods that should receive traffic.

Example:

```yaml
selector:
  app: nginx
```

### Q5. What is the difference between `port` and `targetPort`?

- `port` is the port exposed by the Service.
- `targetPort` is the port on the application container.

In this task:

```text
Service port → 80
Container port → 80
NodePort → 30011
```

---

## 📌 Final Configuration

| Component | Configuration |
|---|---|
| Deployment | `nginx-deployment` |
| Image | `nginx:latest` |
| Container | `nginx-container` |
| Replicas | `3` |
| Service | `nginx-service` |
| Service Type | `NodePort` |
| Service Port | `80` |
| Target Port | `80` |
| NodePort | `30011` |

---

## 🚀 Final Result

✅ Deployment `nginx-deployment` created

✅ `nginx:latest` image deployed

✅ 3 replicas running

✅ Container named `nginx-container`

✅ NodePort Service `nginx-service` created

✅ NodePort `30011` configured

✅ Application exposed through Kubernetes Service

# 🎉 Day 56 Completed Successfully! 🚀
