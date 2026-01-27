🌐 Day 16 – Configure Nginx Load Balancer (LBR)
📌 Scenario

Due to increasing traffic on one of the production websites managed by the Nautilus support team, performance degradation was observed.

To improve availability and scalability, the application was migrated to a high availability architecture. The remaining task was to configure the Load Balancer (LBR) using Nginx to distribute traffic across multiple application servers.

🎯 Objectives

Install and enable Nginx on the Load Balancer server.

Configure load balancing using the main nginx configuration file.

Add all application servers as backend targets.

Ensure Apache services remain running on all backend servers.

Validate website accessibility through the Load Balancer.

🛠️ Tasks Performed
✅ 1. Verify Nginx Installation
which nginx


If not installed:

sudo yum install nginx -y

✅ 2. Verify Nginx Service Availability
systemctl list-unit-files | grep nginx

✅ 3. Enable and Start Nginx
sudo systemctl enable --now nginx
sudo systemctl status nginx

✅ 4. Configure Load Balancing

Edit the main configuration file:

sudo vi /etc/nginx/nginx.conf


Add backend servers inside the http block:

upstream backend {
    server 172.16.238.10:8088;
    server 172.16.238.11:8088;
    server 172.16.238.12:8088;
}


Configure request forwarding:

location / {
    proxy_pass http://backend;
}

✅ 5. Validate Configuration
sudo nginx -t

✅ 6. Restart Nginx
sudo systemctl restart nginx

✅ 7. Verify Backend Services

On all App Servers:

sudo systemctl status httpd


Ensure Apache is running successfully.

✅ 8. Final Testing

Access the application using the provided StaticApp button or browser and confirm the website loads correctly through the Load Balancer.

🧠 Key Learnings

Nginx can act as a reverse proxy and load balancer.

The upstream block defines backend server pools.

proxy_pass forwards client requests to backend servers.

Always validate configuration before restarting services.

Load balancing improves availability and scalability in production environments.

Service state validation prevents unnecessary downtime.

🚨 Issue Faced

Initially, nginx failed to start with the error:

Unit nginx.service not found

🛠️ Fix Applied

Verified nginx binary existence.

Confirmed nginx service registration using systemctl.

Identified that nginx service was disabled.

Enabled and started the nginx service successfully.

✅ Verification
sudo systemctl status nginx


✔️ Output:

Active: active (running)


Website accessible through Load Balancer successfully.

🎤 Interview Questions
Q1. What is a Load Balancer?

A component that distributes incoming traffic across multiple servers to improve performance and availability.

Q2. What does proxy_pass do in Nginx?

It forwards incoming client requests to backend servers.

Q3. What is the purpose of the upstream block?

Defines a pool of backend servers for load balancing.

Q4. Why should nginx -t be executed before restart?

To validate configuration and prevent service downtime.

Q5. Difference between reverse proxy and load balancer?

A reverse proxy forwards requests, while a load balancer distributes requests across multiple servers.

✅ Task Completed Successfully 🎉
