# 🔐 Day 15 – Nginx SSL Configuration & Permission Troubleshooting

## 📌 Scenario
The system admins team of xFusionCorp Industries needed to prepare **App Server 3** for application deployment.

Requirements included:
- Installing and configuring **Nginx**
- Deploying a **self-signed SSL certificate**
- Serving a basic webpage securely over HTTPS
- Troubleshooting permission-related issues

---

## 🎯 Objectives
- Install and configure nginx on App Server 3
- Move SSL certificate and key to proper locations
- Configure nginx to use SSL
- Fix permission errors during nginx startup
- Verify HTTPS access using curl

---

## 🛠️ Tasks Performed

### ✅ 1. Install Nginx
```bash
sudo dnf install nginx -y
```

---

### ✅ 2. Move SSL Certificates to Secure Location
```bash
sudo mkdir -p /etc/nginx/ssl
sudo mv /tmp/nautilus.crt /etc/nginx/ssl/
sudo mv /tmp/nautilus.key /etc/nginx/ssl/
```

---

### ✅ 3. Create Sample Web Page
```bash
sudo vi /usr/share/nginx/html/index.html
```

Content:
```
Welcome!
```

---

### ✅ 4. Configure SSL in Nginx
```bash
sudo vi /etc/nginx/nginx.conf
```

Configured:
- SSL certificate path
- SSL key path
- Listening on port **443**

---

### ✅ 5. Restart Nginx
```bash
sudo systemctl restart nginx
```

---

## 🚨 Issue Faced

When validating nginx configuration:

```bash
nginx -t
```

Errors:
```
Permission denied: /var/log/nginx/error.log
Permission denied: /run/nginx.pid
```

---

## 🛠️ Fix Applied

### ✔️ Fix log directory permissions
```bash
sudo mkdir -p /var/log/nginx
sudo chown -R nginx:nginx /var/log/nginx
```

### ✔️ Run nginx validation with sudo
```bash
sudo nginx -t
```

### ✔️ Restart nginx
```bash
sudo systemctl restart nginx
```

---

## ✅ Verification

### Test HTTPS locally
```bash
curl -k https://stapp03
```

✔️ Output:
```
Welcome!
```

The `-k` flag allows self-signed certificates.

---

## 🧠 Key Learnings

- Nginx requires permission to write logs and PID files.
- Always validate configuration using `nginx -t` with sudo.
- Self-signed SSL certificates require curl `-k` flag.
- File permissions can block service startup even if config is correct.
- Logs are the first place to look during service failures.

---

## 🎤 Interview Questions

### Q1. Why does nginx fail if log permissions are wrong?
Because nginx cannot write logs and PID files without proper permissions.

---

### Q2. What does `nginx -t` do?
It validates nginx configuration syntax without starting the service.

---

### Q3. Why is `curl -k` used?
It skips certificate verification for self-signed certificates.

---

### Q4. Where should SSL certificates be stored?
Secure system locations like `/etc/nginx/ssl`.

---

### Q5. Why should services run with root privileges initially?
To bind to privileged ports and manage system files safely.

---

✅ Task Completed Successfully 🎉
