# 🛠️ Day 09 – MariaDB Service Recovery (Production Incident Simulation)

## 📌 Scenario
The Nautilus application was unable to connect to the database in Stratos Datacenter.  
Investigation revealed that the MariaDB service was down on the database server.

The task was to troubleshoot the issue and restore the database service safely.

---

## 🎯 Objective
- Identify why MariaDB service failed to start.
- Fix the root cause without data loss.
- Restore database service.
- Validate database connectivity.

---

## 🔍 Investigation Steps

### 1️⃣ Check Service Status
```bash
sudo systemctl status mariadb
```
Observed

Service was inactive (dead).

No clear failure reason visible in summary output.

2️⃣ Check Detailed Logs
sudo journalctl -xeu mariadb.service --no-pager
Observed

Service exited immediately after startup.

No package or binary errors detected.

3️⃣ Validate Data Directory
ls -ld /var/lib/mysql
Observed

Directory existed but ownership was incorrect.

🚨 Root Cause
Incorrect ownership on /var/lib/mysql directory prevented the MariaDB service (running as mysql user) from accessing database files.

🛠️ Fix Applied
# Fix directory ownership
sudo chown -R mysql:mysql /var/lib/mysql

# Start MariaDB service
sudo systemctl start mariadb

# Verify service status
sudo systemctl status mariadb
✅ Verification
# Login to MariaDB
sudo mysql
Result

Successfully connected to MariaDB.

Service status showed: active (running).

🧠 Key Learnings
Always analyze logs before applying fixes.

Linux permissions directly affect service behavior.

MariaDB depends on proper ownership of /var/lib/mysql.

systemctl and journalctl are critical troubleshooting tools.

Validate service recovery using real connectivity testing.

🎤 Interview Questions
Q1. Why does MariaDB fail if /var/lib/mysql permissions are wrong?
Because the mysql user cannot read/write database files.

Q2. How do you troubleshoot a failed service?
systemctl status <service>
journalctl -xeu <service>
Q3. Why should you avoid blind restarts?
Blind restarts can hide real issues and risk data integrity.

Q4. How do you verify database health?
Check service status

Connect using mysql client

