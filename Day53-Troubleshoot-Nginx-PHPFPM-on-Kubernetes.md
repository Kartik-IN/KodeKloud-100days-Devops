# ☸️ Day 53 – Troubleshoot Nginx + PHP-FPM on Kubernetes

## 📌 Scenario
The Nginx and PHP-FPM application running in Kubernetes was not working correctly.

Pod:

```
nginx-phpfpm
```

ConfigMap:

```
nginx-config
```

The task was to identify and fix the issue, then copy `index.php` into the Nginx document root and verify the application.

---

## 🛠️ Tasks Performed

### ✅ 1. Check PHP-FPM Logs

```bash
kubectl logs nginx-phpfpm -c php-fpm-container
```

PHP-FPM was running successfully:

```text
fpm is running, pid 1
ready to handle connections
```

---

### ✅ 2. Check PHP-FPM Port

```bash
kubectl exec nginx-phpfpm -c php-fpm-container -- sh -c "netstat -tlnp 2>/dev/null || ss -tlnp"
```

Confirmed PHP-FPM was listening on:

```text
:::9000
```

---

### ✅ 3. Check Nginx Configuration

```bash
kubectl get configmap nginx-config -o yaml
```

Found the PHP configuration:

```text
location ~ \.php$ {
    include fastcgi_params;
    fastcgi_param REQUEST_METHOD $request_method;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    fastcgi_pass 127.0.0.1:9000;
}
```

The issue was the PHP script path being passed to PHP-FPM.

Nginx uses:

```text
/var/www/html
```

while PHP-FPM uses:

```text
/usr/share/nginx/html
```

---

### ✅ 4. Fix the ConfigMap

Updated:

```text
fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
```

to:

```text
fastcgi_param SCRIPT_FILENAME /usr/share/nginx/html$fastcgi_script_name;
```

---

### ✅ 5. Recreate the Pod

The existing Pod was deleted while applying the configuration fix.

The Pod was recreated using the configuration with:

```bash
kubectl apply -f nginx-phpfpm.yaml
```

Verified:

```bash
kubectl get pods
```

Pod returned to:

```text
nginx-phpfpm   2/2   Running
```

---

### ✅ 6. Copy `index.php`

Copied the PHP file from the jump host into the Nginx document root:

```bash
kubectl cp /home/thor/index.php nginx-phpfpm:/var/www/html/ -c nginx-container
```

---

### ✅ 7. Verify the File

```bash
kubectl exec nginx-phpfpm -c nginx-container -- ls -l /var/www/html/
```

Confirmed:

```text
index.php
```

---

### ✅ 8. Test the Application

```bash
kubectl exec nginx-phpfpm -c nginx-container -- curl -i http://localhost:8099/index.php
```

The application responded successfully.

---

## 🧠 Key Learnings

- Kubernetes Pods can contain multiple containers
- Nginx can forward PHP requests to PHP-FPM using FastCGI
- Containers in the same Pod share the network namespace
- Shared volumes can be mounted at different paths in different containers
- `kubectl logs` helps identify application/service problems
- `kubectl exec` allows troubleshooting inside containers
- `kubectl cp` copies files between the jump host and containers
- **The path visible to Nginx and PHP-FPM must match when executing PHP files**

---

## 🎯 Final Result

```text
Nginx + PHP-FPM
      ↓
Configuration Fixed
      ↓
Pod Recreated
      ↓
index.php Copied
      ↓
Application Tested Successfully
```

# 🎉 Day 53 Completed Successfully!
