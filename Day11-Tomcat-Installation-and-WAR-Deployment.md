# 🚀 Day 11 – Tomcat Installation and WAR Deployment

## 📌 Scenario
The Nautilus development team completed a beta version of a Java-based application and decided to deploy it using Apache Tomcat on App Server 3 in Stratos Datacenter.

The task involved installing Tomcat, configuring a custom port, deploying a WAR file, and validating application availability.

---

## 🎯 Objective
- Install Tomcat application server.
- Change default HTTP port to a custom port.
- Deploy ROOT.war application package.
- Ensure application loads on base URL.
- Validate using curl.

---

## 🧭 High-Level Approach

1. Install Tomcat package on the server.
2. Locate Tomcat configuration file and update the listening port.
3. Restart the service to apply configuration changes.
4. Transfer application WAR file from Jump Host.
5. Deploy WAR into Tomcat deployment directory.
6. Validate application accessibility.

---

## 🔍 Key Concepts

### 🔹 What is Tomcat?
Apache Tomcat is a Java-based web application server used to deploy and run Java web applications packaged as WAR files.

---

### 🔹 What is ROOT.war?
- WAR = Web Application Archive.
- Applications deployed as ROOT.war automatically map to the base URL `/`.
- Accessing `http://server:port/` directly loads the application.

---

### 🔹 Why Port Configuration Matters
- Default Tomcat runs on port 8080.
- Production systems often require custom ports for routing and security.
- Port changes are done in the Tomcat connector configuration.

---

### 🔹 How WAR Deployment Works
- Tomcat monitors the deployment directory.
- When a WAR file is placed, Tomcat extracts and serves the application automatically after restart.

---

## 🛠️ Implementation Summary

✔ Tomcat installed successfully on App Server 3  
✔ HTTP connector port updated to 3004  
✔ ROOT.war transferred from Jump Host  
✔ WAR deployed into Tomcat webapps directory  
✔ Correct ownership applied  
✔ Tomcat restarted successfully  
✔ Application accessible on base URL  

---

## ✅ Verification

Validation was done using curl to confirm application response on configured port:

- Service reachable on the expected port.
- Web content returned successfully.

---

## 🧠 Key Learnings
- Service configuration files control runtime behavior.
- Changing network ports requires service restart.
- Correct file ownership is essential for application deployment.
- WAR packaging simplifies Java application deployment.
- Validation is critical after every configuration change.

---

## 🎤 Interview Questions

### Q1. Why does Tomcat use WAR files?
WAR files package application code, dependencies, and configuration into a single deployable unit.

---

### Q2. Why is ROOT.war mapped to the base URL?
Tomcat treats ROOT application as the default context.

---

### Q3. Where is Tomcat configuration stored?
In the server configuration directory containing files like server.xml.

---

### Q4. Why must Tomcat be restarted after configuration change?
Changes are loaded only during service startup.

---

### Q5. How do you verify application availability?
Using HTTP requests and checking service status.

---

## 📅 Status
Completed ✅
