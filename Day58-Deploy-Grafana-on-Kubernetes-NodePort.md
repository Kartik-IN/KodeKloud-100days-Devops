# ☸️ Day 58 – Deploy Grafana on Kubernetes with NodePort

## 📌 Scenario

The Nautilus DevOps team needed to deploy **Grafana** on a Kubernetes cluster to collect and analyze application analytics.

The requirement was to deploy Grafana and expose it externally using a Kubernetes `NodePort` Service.

No additional configuration inside Grafana was required. The main goal was to make sure the **Grafana login page was accessible**.

---

## 🎯 Objectives

- Create a Deployment named `grafana-deployment-xfusion`
- Deploy a Grafana image
- Configure Grafana to listen on port `3000`
- Create a `NodePort` Service
- Configure NodePort `32000`
- Verify that the Grafana login page is accessible

---

## 🛠️ Tasks Performed

### ✅ 1. Create Grafana Deployment and Service

Created:

```bash
vi grafana.yaml
```

Configuration:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana-deployment-xfusion

spec:
  replicas: 1

  selector:
    matchLabels:
      app: grafana

  template:
    metadata:
      labels:
        app: grafana

    spec:
      containers:
        - name: grafana
          image: grafana/grafana:latest
          ports:
            - containerPort: 3000

---
apiVersion: v1
kind: Service
metadata:
  name: grafana-service-xfusion

spec:
  type: NodePort

  selector:
    app: grafana

  ports:
    - port: 3000
      targetPort: 3000
      nodePort: 32000
```

---

## 🚀 2. Deploy Grafana

Applied the configuration:

```bash
kubectl apply -f grafana.yaml
```

Expected output:

```text
deployment.apps/grafana-deployment-xfusion created
service/grafana-service-xfusion created
```

---

## 🔍 3. Verify Deployment

```bash
kubectl get deployment grafana-deployment-xfusion
```

Expected:

```text
NAME                        READY   UP-TO-DATE   AVAILABLE
 grafana-deployment-xfusion 1/1     1            1
```

---

## 🔍 4. Verify Pod

```bash
kubectl get pods
```

Expected:

```text
grafana-deployment-xfusion-xxxxx   1/1   Running
```

---

## 🔍 5. Verify Service

```bash
kubectl get svc grafana-service-xfusion
```

Expected port mapping:

```text
3000:32000/TCP
```

The traffic flow is:

```text
NodePort 32000
      ↓
Service Port 3000
      ↓
Grafana Container Port 3000
```

---

## 🌐 6. Test Grafana

Tested the application using:

```bash
curl http://localhost:32000
```

The Grafana application was successfully accessible.

The **Grafana login page** was available through the Kubernetes NodePort.

---

## 🧠 Key Learnings

- Kubernetes Deployments are used to manage application Pods.
- Grafana runs on port `3000` by default.
- A Kubernetes `NodePort` Service exposes an application outside the cluster.
- `targetPort` determines which container port receives the traffic.
- `nodePort` determines the port exposed on the Kubernetes node.
- Services use selectors to route traffic to matching Pods.

---

## 🎤 Interview Questions

### Q1. What is Grafana?

Grafana is an open-source visualization and analytics platform commonly used to visualize metrics and monitoring data.

### Q2. Why use a Deployment for Grafana?

A Deployment manages the Grafana Pod and ensures the desired number of replicas are maintained.

### Q3. What is a NodePort?

A NodePort exposes a Kubernetes Service on a static port on each Kubernetes node.

### Q4. What is the difference between `port`, `targetPort`, and `nodePort`?

```text
port       → Service port
targetPort → Container/application port
nodePort   → Port exposed on the Kubernetes node
```

For this task:

```text
port       → 3000
targetPort → 3000
nodePort   → 32000
```

### Q5. How does the Service find the Grafana Pod?

The Service uses the label selector:

```yaml
selector:
  app: grafana
```

The Grafana Pod has the matching label:

```yaml
labels:
  app: grafana
```

---

## 📌 Final Configuration

| Component | Configuration |
|---|---|
| Deployment | `grafana-deployment-xfusion` |
| Image | `grafana/grafana:latest` |
| Replicas | `1` |
| Container | `grafana` |
| Container Port | `3000` |
| Service | `grafana-service-xfusion` |
| Service Type | `NodePort` |
| Service Port | `3000` |
| Target Port | `3000` |
| NodePort | `32000` |

---

## 🚀 Architecture

```text
                  Kubernetes Cluster
                         │
                         │
                  NodePort :32000
                         │
                         ▼
              ┌─────────────────────┐
              │   Grafana Service   │
              │      Port 3000      │
              └──────────┬──────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │ Grafana Deployment  │
              │ grafana-deployment- │
              │      xfusion        │
              └──────────┬──────────┘
                         │
                         ▼
                  Grafana Pod
                         │
                         ▼
                 grafana container
                  grafana:latest
                    Port 3000
```

---

## ✅ Final Result

- ✅ Deployment `grafana-deployment-xfusion` created
- ✅ Grafana image deployed
- ✅ Grafana container running on port `3000`
- ✅ NodePort Service created
- ✅ NodePort `32000` configured
- ✅ Grafana accessible
- ✅ Grafana login page verified

# 🎉 Day 58 Completed Successfully! 🚀
