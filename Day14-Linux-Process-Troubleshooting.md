# 🧠 Day 14 – Linux Process Troubleshooting

## 📌 Scenario
Monitoring tools reported that the Apache service was unavailable on one of the app servers in the **Stratos Datacenter**.

The objective was to identify the faulty app host, troubleshoot the issue at process level, restore the Apache service, and ensure the service is running correctly on the required port.

---

## 🎯 Objective
- Identify the faulty app server.
- Troubleshoot Apache process issues.
- Start and enable Apache service.
- Verify Apache is running and reachable.
- Validate port accessibility from jump host.

---

## 🔍 Investigation & Troubleshooting

### 1️⃣ Check Apache Service Status
```bash
sudo systemctl status httpd
```
2️⃣ Analyze Service Logs
```bash
sudo journalctl -xeu httpd
```

Purpose:

Identify process startup errors and dependency issues.

3️⃣ Verify Active Listening Ports
```bash
sudo ss -tulnp | grep 3000
```

Observation:

Apache process was not initially reachable on the expected port.

4️⃣ Restart & Enable Apache Service
```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```

Result:

Apache process started successfully and persisted after reboot.

5️⃣ Validate Service Accessibility
```bash
curl http://stapp01:3000
```

Result:

Apache responded successfully confirming service recovery.

✅ Final Verification
```bash
sudo systemctl status httpd
sudo ss -tulnp | grep 3000
curl http://stapp01:3000
```

✔ Apache service is running
✔ Process healthy and listening correctly
✔ Service accessible from jump host

🧠 Key Learnings

Process-level troubleshooting prevents blind fixes.

Logs provide actionable root cause information.

Network validation confirms real service availability.

Enabling services ensures uptime after reboot.

System commands help isolate failures quickly.

🎤 Interview Questions

Q1. How do you check whether a process/service is running?

systemctl status <service>
ps aux | grep <process>


Q2. How do you investigate service startup failures?

journalctl -xeu <service>


Q3. How do you verify which ports are open on a server?

ss -tulnp
netstat -tulnp


Q4. Why is process monitoring important in production?
To ensure uptime, detect failures early, and maintain system stability.

Q5. How do you validate application availability from another server?

curl http://<host>:<port>

