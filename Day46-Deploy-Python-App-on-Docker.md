# 🐳 Day 46 – Deploy Python App on Docker Containers

## 📌 Scenario

The Nautilus DevOps team needed to containerize a Python application and deploy it on **App Server 1**.

The application dependencies were already provided in:

```bash
/python_app/src/requirements.txt
```

The task was to create a Docker image, deploy the application inside a container, map the required port, and verify that the application was accessible.

---

## 🎯 Objectives

* Create a Dockerfile for the Python application
* Use a Python base image
* Install application dependencies
* Expose port `5002`
* Run `server.py` using Docker `CMD`
* Build an image named `nautilus/python-app`
* Create a container named `pythonapp_nautilus`
* Map host port `8097` to container port `5002`
* Verify the application using `curl`

---

## 🛠️ Tasks Performed

### ✅ 1. Navigate to Application Directory

```bash
cd /python_app
```

The application structure contained:

```text
python_app/
└── src/
    ├── requirements.txt
    └── server.py
```

---

### ✅ 2. Create Dockerfile

Created:

```bash
vi Dockerfile
```

Dockerfile:

```dockerfile
FROM python:3.13-slim

WORKDIR /python_app

COPY src/requirements.txt ./src/

RUN pip install --no-cache-dir -r src/requirements.txt

COPY src/ ./src/

EXPOSE 5002

CMD ["python", "src/server.py"]
```

---

### ✅ 3. Build Docker Image

Built the image using the required name:

```bash
docker build -t nautilus/python-app .
```

Build completed successfully.

---

### ✅ 4. Verify Docker Image

```bash
docker images
```

Confirmed:

```text
REPOSITORY          TAG       IMAGE
nautilus/python-app latest    ...
```

---

### ✅ 5. Run Python Application Container

Created the container with the required name and port mapping:

```bash
docker run -d --name pythonapp_nautilus -p 8097:5002 nautilus/python-app
```

Port mapping:

```text
Host:      8097
Container: 5002
```

---

### ✅ 6. Verify Running Container

```bash
docker ps
```

Expected:

```text
pythonapp_nautilus
```

The container was running successfully.

---

## 🚨 Problems Faced

### ❌ Incorrect Docker Build Command

Initially attempted:

```bash
docker build -t Dockerfile
```

Docker returned an error because the image tag and build context were not specified correctly.

### 🔧 Fix

Used:

```bash
docker build -t nautilus/python-app .
```

Here:

* `-t` → assigns an image name/tag
* `nautilus/python-app` → image name
* `.` → current directory as build context

---

### ❌ Dockerfile COPY Error

Initially received:

```text
COPY requires at least two arguments
Destination could not be determined
```

The `COPY` instruction requires both a source and destination.

Correct format:

```dockerfile
COPY src/requirements.txt ./src/
```

---

### ❌ Container Name

Initially Docker automatically generated a container name:

```text
laughing_lamarr
```

However, the task required:

```text
pythonapp_nautilus
```

The container was recreated using the required name.

---

### ❌ Vim/Bash Confusion

While editing the Dockerfile, `:wq` was accidentally entered in the Bash shell instead of Vim.

This produced:

```text
-bash: :wq: command not found
```

This reinforced the importance of knowing whether commands are being executed in the shell or inside an editor.

---

## ✅ Verification

Tested the application locally on App Server 1:

```bash
curl http://localhost:8097/
```

Output:

```text
Welcome to xFusionCorp Industries!
```

This confirmed that:

```text
Client
   │
   │ :8097
   ▼
Docker Host
   │
   │ Port Mapping
   ▼
Container :5002
   │
   ▼
Python Application
```

---

## 🧠 Key Learnings

* A Dockerfile defines how an application image is built.
* Docker build requires both an image tag and build context.
* `COPY` requires a source and destination.
* `EXPOSE` documents the application's container port.
* `-p` publishes a container port to the host.
* Container names can be explicitly assigned using `--name`.
* A working image does not guarantee that the deployment requirements are completely satisfied.
* Always verify both the **container state** and the **application response**.

---

## 🎤 Interview Questions

### Q1. What is the purpose of a Dockerfile?

A Dockerfile contains instructions used to build a Docker image.

### Q2. What does `-p 8097:5002` mean?

It maps host port `8097` to container port `5002`.

### Q3. Difference between `EXPOSE` and `-p`?

`EXPOSE` documents the port the containerized application uses.
`-p` actually publishes/maps the container port to the host.

### Q4. Why use `python:3.13-slim`?

It provides the Python runtime while keeping the base image smaller than a full Python image.

### Q5. Why use `--no-cache-dir` with pip?

It prevents pip from storing downloaded package caches, helping reduce the final image size.

### Q6. How can you verify that a container is running?

```bash
docker ps
```

### Q7. How can you test the application from the host?

```bash
curl http://localhost:8097/
```

---

## 📌 Final Result

```text
Docker Image
     │
     ▼
nautilus/python-app
     │
     ▼
pythonapp_nautilus
     │
     │ 8097 → 5002
     ▼
Python Application
     │
     ▼
Welcome to xFusionCorp Industries!
```

✅ **Day 46 – Docker Python Application Deployment Completed Successfully** 🚀
