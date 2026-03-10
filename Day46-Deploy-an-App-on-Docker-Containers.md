Deploy PHP & MariaDB using Docker Compose
📌 Overview

This project demonstrates how to deploy a multi-container web application using Docker Compose.

The goal is to:

Run a PHP Apache web server container

Run a MariaDB database container

Configure container networking

Map ports and volumes

Create a database with a custom user

Access the web service using curl

This exercise helps understand Docker Compose orchestration, container networking, and service configuration.

🛠 Technologies Used

Docker

Docker Compose

PHP Apache

MariaDB

Linux

📂 Project Structure
project-folder
│
├── docker-compose.yml
│
└── /var/www/html
    └── index.php (optional test file)

docker-compose.yml – Defines and manages the multi-container application.

⚙️ Docker Compose Configuration
1️⃣ Web Service (PHP + Apache)

This service runs the PHP Apache web server.

Key configurations:

Container Name: php_host

Image: php:8.2-apache

Port Mapping: 6400 → 80

Volume Mapping: /var/www/html

web:
  image: php:8.2-apache
  container_name: php_host
  ports:
    - "6400:80"
  volumes:
    - /var/www/html:/var/www/html
  depends_on:
    - db

This allows the web server to serve PHP files from the host directory.

2️⃣ Database Service (MariaDB)

This service runs the MariaDB database server.

Key configurations:

Container Name: mysql_host

Image: mariadb:latest

Port Mapping: 3306 → 3306

Volume Mapping: /var/lib/mysql

Database: database_host

Custom User: appuser

db:
  image: mariadb:latest
  container_name: mysql_host
  ports:
    - "3306:3306"
  volumes:
    - /var/lib/mysql:/var/lib/mysql
  environment:
    MYSQL_DATABASE: database_host
    MYSQL_USER: appuser
    MYSQL_PASSWORD: Str0ngP@ssw0rd!
    MYSQL_ROOT_PASSWORD: RootStr0ngP@ss123

This creates:

A database named database_host

A custom database user appuser

A secure password for database connections

🚀 Run the Application

Start the containers using:

docker compose up -d

or

docker-compose up -d

This will start:

PHP Apache container (php_host)

MariaDB container (mysql_host)

🌐 Access the Web Application

Test the web server using:

curl localhost:6400

or

curl <server-ip>:6400

Example:

curl 192.168.1.10:6400
🧪 Optional Test File

Create a PHP test file:

/var/www/html/index.php
<?php
phpinfo();
?>

Now open:

http://localhost:6400

You should see the PHP information page.

🎯 Learning Outcomes

After completing this task, you will understand:

How to deploy multi-container applications

How to configure Docker Compose services

How to connect web and database containers

How to use environment variables in containers

How to configure port and volume mapping

📚 DevOps Learning Journey

Day 46 – Deploy PHP & MariaDB using Docker Compose

This project is part of my DevOps learning journey, where I practice containerization, automation, and troubleshooting using real-world scenarios.

⭐ If you found this helpful, feel free to star the repository!
