# ⏰ Day 06 – Cron Job Automation Across App Servers

## 📌 Challenge Description

The infrastructure team required validation of scheduled automation using cron before deploying scripts across production servers.  
A sample cron job was created to verify scheduled execution and output generation.

---

## 🎯 Objective

- Install cron service on all application servers.
- Start the cron daemon service.
- Create a root-level cron job to execute a test command every 5 minutes.
- Verify successful execution across servers.

---

## 🧠 Key Concepts Learned

### ✅ What is Cron?

Cron is a time-based job scheduler used to automate recurring tasks such as backups, cleanup jobs, and monitoring scripts.

---

### ✅ Cron Scheduling Syntax

Cron format consists of five time fields:
Minute Hour Day Month Weekday


Example:


*/5 * * * *


Runs every 5 minutes.

---

### ✅ Root Cron Jobs

Root cron jobs allow system-level automation and require elevated privileges.

---

### ✅ Service Dependency

Cron jobs only run if the cron daemon is active and running.

---

### ✅ Multi-Server Consistency

Each application server must independently have:
- Cron installed
- Service running
- Cron job configured

---

## ❌ Mistakes and Learning

- Attempted to execute cron schedule directly in shell.
- Initially misunderstood crontab syntax.
- Reinforced importance of using cron editor.

---

## ✅ How the Issue Was Solved

- Installed cron package using system package manager.
- Started cron service.
- Opened root cron editor.
- Added scheduled job entry.
- Verified file output after execution.
- Repeated configuration on all servers.

---

## 🔍 Verification Summary

Verification confirmed:

- Cron service running successfully.
- Cron job present in root crontab.
- Output file generated and updated periodically.

---

## 💡 Key Takeaways

- Cron syntax must be configured inside crontab.
- Always verify scheduled jobs.
- Automation must be consistent across servers.
- Debugging improves reliability.

---

## 🎤 Interview Preparation Notes

### Q1: What is cron used for?
Automating repetitive system tasks.

---

### Q2: Where are cron jobs stored?
In user-specific crontab files managed by the system.

---

### Q3: Why must cron daemon be running?
Cron jobs execute only when the service is active.

---

### Q4: Difference between user cron and root cron?
Root cron has system-level privileges.

---

---

## 📅 Progress Log

Day 06 : Cron Job Automation Across App Servers  ✅ Completed

---


