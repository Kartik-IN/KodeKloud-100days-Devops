# 🌐 Day 12 – Linux Network Services (Apache Connectivity Troubleshooting)

## 📌 Scenario
Monitoring tools reported that the Apache service on an application server in Stratos Datacenter was not reachable on port 5003.

The issue could be caused by:
- Apache service not running
- Port not listening
- Firewall blocking the port
- Incorrect configuration

The task was to investigate using networking tools and restore service accessibility without compromising security.

---

## 🎯 Objective
- Identify why Apache was unreachable on port 5003.
- Validate port listening status.
- Check service health.
- Verify firewall configuration.
- Restore network accessibility.
- Confirm access from jump host.

---

## 🧭 High-Level Troubleshooting Flow

1. Validate network connectivity from jump host.
2. Check if the service port is listening on the server.
3. Verify Apache service status.
4. Inspect firewall rules.
5. Apply corrective actions.
6. Re-test connectivity.

---

## 🔍 Tools Used

### 🔹 telnet
Used to test whether a TCP port is reachable.

### 🔹 netstat / ss
Used to verify if a service is actively listening on a port.

### 🔹 systemctl
Used to check and manage service status.

### 🔹 firewall-cmd
Used to validate and manage firewall rules.

### 🔹 curl
Used to verify HTTP service availability.

---

## 🛠️ Investigation Summary

✔ Confirmed that port 5003 was not reachable initially  
✔ Verified Apache service status  
✔ Checked port listening behavior  
✔ Reviewed firewall configuration  
✔ Identified misconfiguration blocking access  
✔ Applied necessary corrections  
✔ Restored service accessibility  

---

## ✅ Verification

Service was successfully validated from the jump host using HTTP request:

- Apache responded correctly on port 5003.
- Network connectivity restored without reducing security posture.

---

## 🧠 Key Learnings
- Network issues can originate from service, firewall, or port configuration.
- Always validate listening ports before changing firewall rules.
- Use layered troubleshooting instead of guessing.
- Tools like telnet and netstat help isolate network issues quickly.
- Never weaken security to solve connectivity problems.

---

## 🎤 Interview Questions

### Q1. How do you verify if a port is listening on a server?
Using netstat or ss to check listening sockets.

---

### Q2. Why might Apache be unreachable even if it is running?
Firewall restrictions, incorrect binding address, or wrong port configuration.

---

### Q3. What is the purpose of telnet in troubleshooting?
To test raw TCP connectivity to a port.

---

### Q4. Why should security rules not be disabled blindly?
It increases risk and violates production security standards.

---

### Q5. How do you confirm service availability after fixing?
Using curl or browser-based HTTP validation.

---

## 📅 Status
Completed ✅
