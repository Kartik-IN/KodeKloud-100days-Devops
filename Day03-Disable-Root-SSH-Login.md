# 🔐 Day 03 – Disable Direct Root SSH Login on All App Servers

## 📌 Challenge Description

As part of security hardening, direct SSH login for the root user must be disabled on all application servers.  
This prevents unauthorized access and improves auditability of administrative actions.

This task simulates real-world production security policies used in enterprise environments.

---

## 🎯 Objective

- Identify the correct SSH server configuration file.
- Disable direct root login via SSH.
- Apply the change on all application servers.
- Reload the SSH service to activate the new configuration.
- Verify that root login is blocked.

---

## 🧠 Key Concepts Learned

### ✅ Why Root SSH Login Should Be Disabled

Allowing direct root login is risky because:

- Full administrative access is granted immediately.
- No accountability or traceability of actions.
- Higher impact if credentials are compromised.
- Difficult to audit user activity.

Best practice:
- Login as a normal user.
- Elevate privileges only when required.

---

### ✅ SSH Client vs SSH Server Configuration

There are two SSH configuration types:

Client Configuration:
- Controls outbound SSH connections.
- Affects how this machine connects to other servers.

Server (Daemon) Configuration:
- Controls inbound SSH connections.
- Defines authentication rules and security policies.

Security changes must always be applied to the server configuration.

---

### ✅ SSH Configuration File Location

The SSH daemon configuration file is located at:

/etc/ssh/sshd_config

This file controls root login permissions, authentication methods, ports, and security settings.

---

### ✅ Service Reload Requirement

Configuration changes do not apply automatically.

The SSH service must be reloaded or restarted for changes to take effect.

Failure to reload means the old configuration remains active.

---

### ✅ Multi-Server Awareness

In distributed environments:

- Each server has independent configuration.
- Changes must be applied individually.
- Jump host is used only for access, not configuration.
- Always verify which server you are connected to.

---

## ❌ Mistakes and Learning

- Tried editing SSH config on the jump host instead of app servers.
- Confused file naming (`sshd-config` vs `sshd_config`).
- Forgot administrative privileges initially.
- Learned the importance of absolute file paths.

These mistakes reinforced production-level operational discipline.

---

## ✅ How the Issue Was Solved

- Connected to each application server individually.
- Opened the correct SSH daemon configuration file.
- Updated the root login rule to disable access.
- Reloaded the SSH service to activate changes.
- Verified behavior and configuration.

---

## 🔍 Verification Summary

Verification confirmed:

- Root SSH login is blocked.
- Configuration changes are persistent.
- SSH service is running correctly.
- No impact on normal user access.

---

## 💡 Key Takeaways

- Security hardening is critical in production systems.
- Always verify which machine you are working on.
- Configuration changes require service reloads.
- Small filename mistakes can cause major issues.
- Never allow direct root access in secure environments.

---

## 🎤 Interview Preparation Notes

### Q1: Why should direct root SSH login be disabled?
To reduce security risk, improve accountability, and prevent unauthorized full system access.

---

### Q2: What is the difference between ssh_config and sshd_config?
ssh_config controls client behavior, while sshd_config controls server authentication and access rules.

---

### Q3: Why must the SSH service be restarted after configuration changes?
Because services load configuration into memory at startup.

---

### Q4: What could happen if you disable root login incorrectly?
You could lock yourself out of administrative access.

---

### Q5: How can security changes be safely applied across multiple servers?
By following controlled rollout, validation, and documentation.

---

## 📅 Progress Log

Day 03 : Disable Direct Root SSH Login on All App Servers  ✅ Completed

---

