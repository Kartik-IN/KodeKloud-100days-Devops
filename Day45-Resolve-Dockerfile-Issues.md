# DevOps – Day 45

## Resolve Dockerfile Issues (Apache HTTP Server with SSL)

### 📌 Overview

This project demonstrates how to identify and resolve issues in a Dockerfile while building an Apache HTTP Server container with SSL support.

The goal is to:

* Modify the Apache configuration inside a Docker container
* Enable SSL modules
* Configure the server to run on port **8080**
* Copy SSL certificates and website files into the container
* Successfully build and run the Docker image

This exercise helps understand **Dockerfile debugging, container configuration, and basic DevOps troubleshooting**.

---

## 🛠 Technologies Used

* Docker
* Apache HTTP Server (httpd:2.4.43)
* Linux Shell Commands (sed)
* SSL Configuration

---

## 📂 Project Structure

```
project-folder
│
├── Dockerfile
├── certs
│   ├── server.crt
│   └── server.key
│
└── html
    └── index.html
```

* **Dockerfile** – Defines the container image configuration.
* **certs/** – Contains SSL certificate and private key.
* **html/** – Contains the web page served by Apache.

---

## ⚙️ Dockerfile Explanation

### 1️⃣ Base Image

```dockerfile
FROM httpd:2.4.43
```

Uses the official Apache HTTP Server Docker image as the base.

---

### 2️⃣ Change Apache Listening Port

```dockerfile
RUN sed -i "s/Listen 80/Listen 8080/g" /usr/local/apache2/conf/httpd.conf
```

This command modifies the Apache configuration so the server listens on **port 8080 instead of port 80**.

---

### 3️⃣ Enable SSL Module

```dockerfile
RUN sed -i '/LoadModule ssl_module modules\/mod_ssl.so/s/^#//g' /usr/local/apache2/conf/httpd.conf
```

Uncomments the SSL module to enable HTTPS functionality.

---

### 4️⃣ Enable Shared Memory Cache Module

```dockerfile
RUN sed -i '/LoadModule socache_shmcb_module modules\/mod_socache_shmcb.so/s/^#//g' /usr/local/apache2/conf/httpd.conf
```

This module is required for SSL session caching.

---

### 5️⃣ Include SSL Configuration

```dockerfile
RUN sed -i '/Include conf\/extra\/httpd-ssl.conf/s/^#//g' /usr/local/apache2/conf/httpd.conf
```

Enables the Apache SSL configuration file.

---

### 6️⃣ Copy SSL Certificates

```dockerfile
COPY certs/server.crt /usr/local/apache2/conf/server.crt
COPY certs/server.key /usr/local/apache2/conf/server.key
```

Copies the SSL certificate and key into the Apache configuration directory.

---

### 7️⃣ Copy Website Files

```dockerfile
COPY html/index.html /usr/local/apache2/htdocs/
```

Adds the website HTML file to the Apache document root.

---

## 🚀 Build the Docker Image

Run the following command:

```bash
docker build -t apache-ssl .
```

This builds the Docker image from the Dockerfile.

---

## ▶ Run the Container

```bash
docker run -p 8080:8080 apache-ssl
```

This starts the container and maps port **8080** from the container to the host machine.

---

## 🌐 Access the Application

Open your browser and go to:

```
http://localhost:8080
```

You should see the **index.html page served by Apache**.

---

## 🎯 Learning Outcomes

After completing this task, you will understand:

* How to debug and fix Dockerfile issues
* How to modify configuration files inside Docker containers
* How to enable Apache SSL modules
* How to copy files into Docker images
* How to build and run Docker containers

---

## 📚 DevOps Learning Journey

**Day 45 – Resolve Dockerfile Issues**

This project is part of my **DevOps learning journey**, where I practice containerization, automation, and troubleshooting using real-world scenarios.

---

⭐ If you found this helpful, feel free to star the repository!
