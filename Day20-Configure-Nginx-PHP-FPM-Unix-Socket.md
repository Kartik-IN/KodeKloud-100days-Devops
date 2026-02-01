# ⚙️ Day 20 – Configure Nginx + PHP-FPM Using Unix Socket

## 📌 Scenario
The Nautilus application team needed to deploy a **PHP-based application** on **App Server 1** in **Stratos Datacenter**.

The requirement was to configure **Nginx and PHP-FPM** to work together using a **Unix socket**, ensuring better performance and secure local communication.

Pre-created application files (`index.php` and `info.php`) were already present under the web root and were **not to be modified**.

---

## 🎯 Objectives
- Install and configure **Nginx** on App Server 1
- Configure Nginx to listen on a custom port
- Install **PHP-FPM 8.3**
- Configure PHP-FPM to use a Unix socket
- Integrate Nginx with PHP-FPM
- Verify PHP execution via curl

---

## 🛠️ Tasks Performed

### ✅ 1. Install Nginx
```bash
sudo yum install -y nginx
✅ 2. Configure Nginx Port & Document Root
sudo vi /etc/nginx/nginx.conf
Updated:

listen 8095;
root /var/www/html;
index index.php index.html;
✅ 3. Install PHP-FPM 8.3
sudo yum install -y php-fpm php-cli
✅ 4. Configure PHP-FPM to Use Unix Socket
sudo vi /etc/php-fpm.d/www.conf
Updated:

listen = /var/run/php-fpm/default.sock
Create socket directory if missing:

sudo mkdir -p /var/run/php-fpm
sudo chown -R nginx:nginx /var/run/php-fpm
✅ 5. Configure Nginx to Work with PHP-FPM
sudo vi /etc/nginx/nginx.conf
Added PHP block:

location ~ \.php$ {
    include fastcgi_params;
    fastcgi_pass unix:/var/run/php-fpm/default.sock;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
}
✅ 6. Start and Enable Services
sudo systemctl start php-fpm
sudo systemctl enable php-fpm

sudo systemctl start nginx
sudo systemctl enable nginx
✅ Verification
Test PHP Application from Jump Host
curl http://stapp01:8095/index.php
✔️ PHP page loaded successfully
✔️ Nginx and PHP-FPM working via Unix socket

🧠 Key Learnings
Unix sockets are faster and more secure than TCP for local services

PHP-FPM must match Nginx user permissions

Incorrect socket paths break PHP rendering

fastcgi_param SCRIPT_FILENAME is critical

Logs and socket permissions are common failure points

🎤 Interview Questions
Q1. Why use Unix socket instead of TCP?
Unix sockets provide faster communication and improved security for local services.

Q2. What happens if socket permissions are incorrect?
Nginx cannot communicate with PHP-FPM, resulting in 502 errors.

Q3. Which directive connects Nginx to PHP-FPM?
fastcgi_pass

Q4. Where are PHP-FPM pool configurations stored?
/etc/php-fpm.d/www.conf

Q5. Why should application files not be modified?
To ensure configuration validation without altering application logic.

✅ Day 20 Completed Successfully 🎉
