# 🐳 Day 40 – Install & Configure Apache Inside Docker Container

## 📌 Scenario

A Nautilus DevOps team member was configuring services inside a running Docker container named `kkloud` on Application Server 1.

Due to unavailability, the remaining work had to be completed:

- Install Apache inside the container
- Configure Apache to listen on port 8084 (instead of default 80)
- Ensure it listens on all interfaces (not just localhost)
- Keep the container running after configuration

---

## 🎯 Objectives

- Access running container
- Install apache2 using apt
- Modify Apache configuration
- Start Apache service inside container
- Keep container running state intact

---

## 🛠️ Tasks Performed

### ✅ 1. Verify Running Container

```bash
docker ps
```
Confirmed container:

kkloud
✅ 2. Access Container Shell
docker exec -it kkloud bash
✅ 3. Update Package Index
apt update
✅ 4. Install Apache2
apt install apache2 -y
✅ 5. Configure Apache to Listen on Port 8084

Edit ports configuration file:

vi /etc/apache2/ports.conf

Change:

Listen 80

To:

Listen 8084
✅ 6. Update Virtual Host Configuration
vi /etc/apache2/sites-available/000-default.conf

Change:

<VirtualHost *:80>

To:

<VirtualHost *:8084>
✅ 7. Start Apache Service Inside Container
service apache2 start

Or:

apachectl start
✅ 8. Verify Apache is Running
ps aux | grep apache

Or:

netstat -tulnp | grep 8084
🚨 Common Mistakes

Forgetting to modify both ports.conf and virtual host file

Apache binding only to localhost

Not starting Apache inside container

Exiting container before confirming service status

🧠 Key Learnings

Containers do not run systemd by default

Services inside containers must be manually started

Port binding must be updated in both Apache config files

Docker containers isolate services from host

Always verify service status before exiting container

🎤 Interview Questions
Q1. Why doesn’t systemctl work inside most containers?

Because containers typically don’t run systemd as PID 1.

Q2. How do you install packages inside a running container?

Using:

docker exec -it <container> bash

Then install normally using apt/yum.

Q3. Why modify both ports.conf and VirtualHost file?

Because Apache listens based on both global and virtual host configuration.

Q4. How to verify service inside container?

Use:

ps aux
netstat -tulnp
Q5. What is the difference between host port mapping and container internal port?

Container port → Service running inside container

Host port → Port exposed via Docker mapping

✅ Day 40 Task Completed Successfully
