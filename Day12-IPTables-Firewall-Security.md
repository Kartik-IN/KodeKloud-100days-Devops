# 🔥 Day 12 – Securing Apache Port Using iptables Firewall

## 📌 Scenario
The security team identified that Apache port **5000** was open to everyone on all app servers in the Stratos Datacenter.  
There was no firewall installed on these servers, creating a security risk.

The requirement was to:
- Install iptables
- Allow access to port **5000** only from the **LBR host**
- Block all other incoming traffic on port 5000
- Ensure firewall rules persist after reboot

---

## 🎯 Objective
- Harden server network security using iptables.
- Restrict Apache access to trusted source only.
- Maintain system accessibility (SSH + loopback).
- Persist firewall rules permanently.

---

## 🛠️ Implementation Steps

### 1️⃣ Install iptables
```bash
sudo yum install -y iptables-services
```

> Note: On modern Linux systems, iptables does not run as a systemd service.  
> It works directly as kernel firewall rules.

---

### 2️⃣ Flush Existing Rules
```bash
sudo iptables -F
```

This ensures no conflicting rules exist before applying new policies.

---

### 3️⃣ Allow Loopback Traffic
```bash
sudo iptables -A INPUT -i lo -j ACCEPT
```

Allows internal system communication.

---

### 4️⃣ Allow Established Connections
```bash
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```

Prevents breaking existing sessions (SSH, active connections).

---

### 5️⃣ Allow SSH Access
```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

Ensures remote access remains available.

---

### 6️⃣ Allow Port 5000 Only From LBR Host
```bash
sudo iptables -A INPUT -p tcp -s 172.16.238.14 --dport 8088 -j ACCEPT
```

Allows Apache traffic only from trusted Load Balancer host.

---

### 7️⃣ Block All Other Traffic on Port 5000
```bash
sudo iptables -A INPUT -p tcp --dport 8088 -j DROP
```

Blocks unauthorized access.

---

### 8️⃣ Verify Firewall Rules
```bash
sudo iptables -L -n --line-numbers
```

Confirms rule order and correctness.

---

### 9️⃣ Persist Firewall Rules
```bash
sudo service iptables save
```

Ensures rules remain after reboot.

---

## ✅ Verification

- ✔ Access from LBR host → Allowed
- ❌ Access from Jump host → Blocked
- ✔ SSH connectivity → Working
- ✔ Firewall rules visible using iptables list

---

## 🧠 Key Learnings

- iptables does not run as a service on modern Linux distributions.
- Firewall rule order is critical.
- Always allow loopback and established connections.
- Never block SSH access accidentally.
- Persistence must be configured manually.
- Security should follow least privilege principle.

---

## 🎤 Interview Questions

### Q1. Why is iptables.service not found on modern Linux?
Because iptables operates as kernel rules, not as a running daemon.

---

### Q2. Why allow ESTABLISHED,RELATED traffic?
To prevent breaking existing network connections.

---

### Q3. Why is rule order important in iptables?
iptables evaluates rules sequentially from top to bottom.

---

### Q4. How do you make iptables rules persistent?
By saving rules using iptables service save or persistent rule files.

---

### Q5. What happens if DROP rule comes before ACCEPT rule?
Legitimate traffic will be blocked.

---

🚀 **Day 12 Completed Successfully**
