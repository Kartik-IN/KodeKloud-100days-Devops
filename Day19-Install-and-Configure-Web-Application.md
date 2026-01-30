# 🌐 Day 19 – Install and Configure Web Application (Apache Virtual Paths)

## 📌 Scenario
xFusionCorp Industries planned to host **two static websites** on their infrastructure in **Stratos Datacenter**.  
The websites are still under development, but the servers needed to be prepared in advance.

The task involved configuring **Apache HTTPD** on **App Server 2** to serve two different applications from separate paths.

---

## 🎯 Objectives
- Install Apache HTTPD on App Server 2
- Configure Apache to listen on a custom port
- Deploy two static applications (`news` and `demo`)
- Serve applications using path-based URLs
- Verify accessibility using curl

---

## 🛠️ Tasks Performed

### ✅ 1. Install Apache HTTPD
```bash
sudo yum install -y httpd
```

✅ 2. Configure Apache to Run on Port 6300
sudo vi /etc/httpd/conf/httpd.conf
Updated:

Listen 6300
✅ 3. Start and Enable Apache Service
sudo systemctl start httpd
sudo systemctl enable httpd
✅ 4. Prepare Web Root Directory
sudo mkdir -p /var/www/html
sudo chown -R steve:steve /var/www/html
✅ 5. Copy Website Backups from Jump Host
From jump host:

sudo scp -r /home/thor/news steve@stapp02:/var/www/html/
sudo scp -r /home/thor/demo steve@stapp02:/var/www/html/
✅ 6. Verify Directory Structure
On App Server 2:

ls /var/www/html/
Expected:

news
demo
✅ Verification
Test locally on App Server 2:
curl http://localhost:6300/news/
curl http://localhost:6300/demo/
✔️ Both URLs returned expected static content.

🧠 Key Learnings
Apache can serve multiple applications using path-based routing.

Destination directories must exist before using scp.

Custom Apache ports require updating httpd.conf.

Permissions are critical for successful file deployment.

Always verify services using curl from the server itself.

🎤 Interview Questions
Q1. Why did SCP fail initially?
Because the destination directory /var/www/html did not exist on the remote server.

Q2. How does Apache serve multiple apps on one server?
By using different subdirectories under the document root.

Q3. Why use curl for verification?
It confirms service availability without needing a browser.

Q4. Which file controls Apache’s listening port?
/etc/httpd/conf/httpd.conf

Q5. What is the Apache document root by default?
/var/www/html

✅ Task Completed Successfully – Day 19 🎉
