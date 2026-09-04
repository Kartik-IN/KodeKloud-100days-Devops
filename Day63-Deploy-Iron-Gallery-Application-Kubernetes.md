# ☸️ Day 63 – Deploy Iron Gallery Application on Kubernetes

## 📌 Scenario

The Nautilus DevOps team was preparing the **Iron Gallery** application for deployment on a Kubernetes cluster.

The task required deploying both the Iron Gallery frontend and Iron DB backend in a dedicated namespace, along with the required volumes, environment variables, and Kubernetes Services.

---

## 🎯 Objectives

- Create a dedicated Kubernetes namespace.
- Deploy the Iron Gallery application.
- Deploy the Iron DB database.
- Configure container resource limits.
- Configure `emptyDir` volumes.
- Configure database environment variables.
- Create a ClusterIP service for the database.
- Create a NodePort service for the gallery application.
- Verify that the application is running successfully.

---

## 🛠️ Step 1: Create Namespace

Created the namespace:

```bash
kubectl create namespace iron-namespace-xfusion
```

Namespace:

```text
iron-namespace-xfusion
```

---

## 🖼️ Step 2: Create Iron Gallery Deployment

Created deployment:

```text
iron-gallery-deployment-xfusion
```

Configuration:

| Parameter | Value |
|---|---|
| Namespace | `iron-namespace-xfusion` |
| Replicas | `1` |
| Label | `run=iron-gallery` |
| Container | `iron-gallery-container-xfusion` |
| Image | `kodekloud/irongallery:2.0` |
| Memory Limit | `100Mi` |
| CPU Limit | `50m` |

### Volumes

Two `emptyDir` volumes were configured:

```text
config  → /usr/share/nginx/html/data
images  → /usr/share/nginx/html/uploads
```

---

## 🗄️ Step 3: Create Iron DB Deployment

Created deployment:

```text
iron-db-deployment-xfusion
```

Configuration:

| Parameter | Value |
|---|---|
| Namespace | `iron-namespace-xfusion` |
| Replicas | `1` |
| Label | `db=mariadb` |
| Container | `iron-db-container-xfusion` |
| Image | `kodekloud/irondb:2.0` |

### Environment Variables

```text
MYSQL_DATABASE=database_blog
MYSQL_ROOT_PASSWORD=<configured password>
MYSQL_PASSWORD=<configured password>
MYSQL_USER=ironuser
```

Passwords are represented as placeholders here and should be supplied securely in the deployment environment.

### Database Volume

Configured an `emptyDir` volume:

```text
db → /var/lib/mysql
```

---

## 🌐 Step 4: Create Iron DB Service

Created a ClusterIP service:

```text
iron-db-service-xfusion
```

Configuration:

```text
Selector:    db=mariadb
Protocol:    TCP
Port:        3306
TargetPort:  3306
Type:        ClusterIP
```

The service provides internal Kubernetes networking for the database.

---

## 🌍 Step 5: Create Iron Gallery Service

Created a NodePort service:

```text
iron-gallery-service-xfusion
```

Configuration:

```text
Selector:    run=iron-gallery
Protocol:    TCP
Port:        80
TargetPort:  80
NodePort:    32678
Type:        NodePort
```

The NodePort exposes the Iron Gallery application externally.

---

## 🔍 Verification

### Check Deployments

```bash
kubectl get deployments -n iron-namespace-xfusion
```

Expected:

```text
iron-gallery-deployment-xfusion   1/1
iron-db-deployment-xfusion        1/1
```

---

### Check Pods

```bash
kubectl get pods -n iron-namespace-xfusion
```

Both Pods should be:

```text
1/1   Running
```

---

### Check Services

```bash
kubectl get svc -n iron-namespace-xfusion
```

Expected services:

```text
iron-db-service-xfusion
iron-gallery-service-xfusion
```

The gallery service should expose:

```text
80:32678/TCP
```

---

### Check All Resources

```bash
kubectl get all -n iron-namespace-xfusion
```

This verifies the Deployments, Pods, ReplicaSets, and Services together.

---

## 🏗️ Architecture

```text
                    Kubernetes Cluster
                           │
                           ▼
              iron-namespace-xfusion
                           │
             ┌─────────────┴─────────────┐
             │                           │
             ▼                           ▼
    Iron Gallery                     Iron DB
    Deployment                       Deployment
             │                           │
             ▼                           ▼
   iron-gallery-container      iron-db-container
   kodekloud/irongallery:2.0   kodekloud/irondb:2.0
             │                           │
       ┌─────┴─────┐                     │
       ▼           ▼                     ▼
     config       images                db
    emptyDir     emptyDir             emptyDir
       │           │                     │
       ▼           ▼                     ▼
 /html/data   /html/uploads        /var/lib/mysql
       │
       ▼
iron-gallery-service-xfusion
       │
       ▼
NodePort :32678
```

---

## 🧠 Key Learnings

### 1. Kubernetes Namespace

Namespaces provide logical isolation and organization for Kubernetes resources.

```bash
kubectl get pods -n iron-namespace-xfusion
```

### 2. Deployment

A Deployment manages application Pods and ensures the desired number of replicas are running.

```yaml
replicas: 1
```

### 3. Labels and Selectors

Labels identify resources, while selectors allow Deployments and Services to find the appropriate Pods.

Gallery:

```text
run=iron-gallery
```

Database:

```text
db=mariadb
```

### 4. `emptyDir`

`emptyDir` creates temporary storage associated with the Pod.

It was used for:

```text
config
images
db
```

### 5. Resource Limits

The Iron Gallery container was configured with:

```yaml
limits:
  memory: 100Mi
  cpu: 50m
```

Resource limits prevent a container from consuming more resources than intended.

### 6. ClusterIP vs NodePort

| Service | Type | Purpose |
|---|---|---|
| `iron-db-service-xfusion` | ClusterIP | Internal database access |
| `iron-gallery-service-xfusion` | NodePort | External gallery access |

---

## 🎤 Interview Questions

### Q1. Why use a Namespace?

Namespaces provide logical separation and organization of Kubernetes resources.

### Q2. What is an `emptyDir` volume?

An `emptyDir` is temporary storage created when a Pod is assigned to a node. It exists for the lifetime of the Pod.

### Q3. What is the difference between ClusterIP and NodePort?

**ClusterIP** exposes a service internally within the Kubernetes cluster.

**NodePort** exposes the service through a port on each Kubernetes node.

### Q4. Why are labels and selectors important?

They allow Kubernetes resources such as Deployments and Services to identify and associate with the correct Pods.

### Q5. What is the purpose of resource limits?

Resource limits restrict the maximum CPU and memory that a container can consume.

---

## 📋 Final Configuration

### Iron Gallery

```text
Deployment:  iron-gallery-deployment-xfusion
Container:   iron-gallery-container-xfusion
Image:       kodekloud/irongallery:2.0
Replicas:    1
Label:       run=iron-gallery
Memory:      100Mi
CPU:         50m
```

### Iron DB

```text
Deployment:  iron-db-deployment-xfusion
Container:   iron-db-container-xfusion
Image:       kodekloud/irondb:2.0
Replicas:    1
Label:       db=mariadb
Database:    database_blog
User:        ironuser
```

### Services

```text
iron-db-service-xfusion
    Type: ClusterIP
    Port: 3306

iron-gallery-service-xfusion
    Type: NodePort
    Port: 80
    NodePort: 32678
```

---

## 🚀 Final Result

✅ Namespace `iron-namespace-xfusion` created

✅ Iron Gallery deployment created

✅ Iron DB deployment created

✅ Required labels and selectors configured

✅ Gallery resource limits configured

✅ Required `emptyDir` volumes configured

✅ Database environment variables configured

✅ Database ClusterIP service created

✅ Gallery NodePort service created

✅ Gallery exposed on NodePort `32678`

✅ Application verified successfully

# 🎉 Day 63 Completed Successfully!
