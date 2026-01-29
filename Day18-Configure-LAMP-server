🚀 Day 18 – WordPress Infrastructure Setup (Apache + PHP + MariaDB)
📌 Scenario

xFusionCorp Industries planned to host a WordPress website on their infrastructure in Stratos Datacenter.

A shared storage directory /var/www/html was already mounted across all App Servers.
The task was to prepare the web servers, configure database services, and validate application connectivity via Load Balancer (LBR).

🎯 Objectives

Install and configure Apache (httpd) and PHP on all App Servers.

Configure Apache to run on port 6100.

Install and configure MariaDB on Database Server.

Create database and user with proper privileges.

Validate application accessibility from LBR.

🛠️ Tasks Performed
✅ 1. Install Apache and PHP on All App Servers
# Verify Apache installation
httpd -v

# Verify PHP installation
php -v

# Check Apache service status
systemctl status httpd


✔️ Apache and PHP verified successfully on all App Servers.

✅ 2. Configure Apache to Run on Port 6100
# Edit Apache configuration
vi /etc/httpd/conf/httpd.conf

# Update Listen directive
Listen 6100

# Restart Apache service
systemctl restart httpd

# Verify port listening
ss -tulnp | grep 6100


✔️ Apache confirmed running on port 6100.

✅ 3. Verify Shared Web Directory
# Verify mount point
df -h | grep /var/www/html

# Check directory content
ls /var/www/html


✔️ Shared storage confirmed mounted correctly across all App Servers.

✅ 4. Install and Configure MariaDB on DB Server
# Check MariaDB status
systemctl status mariadb

# Login to MariaDB shell
mysql -u root -p

🗄️ Database Setup
CREATE DATABASE kodekloud_db2;
CREATE USER 'kodekloud_roy'@'%' IDENTIFIED BY 'TmpCzjtRQx';
GRANT ALL PRIVILEGES ON kodekloud_db2.* TO 'kodekloud_roy'@'%';
FLUSH PRIVILEGES;


✔️ Database and user created successfully.

✅ 5. Validate Database Access
mysql -u kodekloud_roy -p kodekloud_db2


✔️ User login and database access verified successfully.

✅ 6. Final Application Validation via Load Balancer

Accessed application using App button / LBR link.

Verified successful message:

App is able to connect to the database successfully


✔️ Application working correctly through Load Balancer.

🧠 Key Learnings

Multi-tier architecture requires coordination between Web, DB, and Networking layers.

Apache port changes must be validated using socket inspection tools.

Database permissions directly impact application connectivity.

Shared storage simplifies multi-node deployments.

Always validate from Load Balancer to simulate real production access.

🎤 Interview Questions
Q1. Why run Apache on a non-default port?

To avoid port conflicts and improve flexibility in multi-service environments.

Q2. Why use shared storage for web content?

It ensures consistency across multiple app servers in load-balanced setups.

Q3. Why grant least-required privileges to DB users?

For better security and reduced attack surface.

Q4. How do you verify a service is listening on a specific port?

Using tools like:

ss -tulnp

Q5. How do you validate application connectivity end-to-end?

By accessing through Load Balancer and verifying application response.

✅ Task Completed Successfully 🎉
