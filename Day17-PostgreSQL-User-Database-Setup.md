🐘 Day 17 – PostgreSQL User & Database Provisioning
📌 Scenario

The Nautilus application development team planned to deploy a new application on Nautilus infrastructure in Stratos Datacenter.
The application requires a PostgreSQL database, and the database server was already installed.

The task was to:

Create a database user

Assign a secure password

Create a database

Grant full access permissions
⚠️ PostgreSQL service restart was not allowed.

🎯 Objectives

Create PostgreSQL user kodekloud_aim

Set password securely

Create database kodekloud_db4

Grant full privileges to the user

Validate successful configuration

🛠️ Tasks Performed
✅ 1. Switch to PostgreSQL Shell
sudo su - postgres
psql


✅ 2. Create Database User
CREATE USER kodekloud_aim WITH PASSWORD 'ksH85UJjhb';


✔️ User created successfully.

✅ 3. Create Database
CREATE DATABASE kodekloud_db4;


✔️ Database created successfully.

✅ 4. Grant Full Privileges
GRANT ALL PRIVILEGES ON DATABASE kodekloud_db4 TO kodekloud_aim;


✔️ User now has full access to the database.

✅ Verification

(Optional but recommended)

psql -U kodekloud_aim -d kodekloud_db4


✔️ Successful login confirms correct permissions.

🧠 Key Learnings

PostgreSQL user creation is done using SQL commands.

Database access is controlled through privilege grants.

Service restarts should be avoided in production environments.

Always validate access after configuration.

Clear separation between system users and database users improves security.

🎤 Interview Questions
Q1. What is the difference between a PostgreSQL role and user?

A role can act as both a user and a group depending on privileges assigned.

Q2. Why should database services not be restarted in production?

It can cause downtime and impact live applications.

Q3. How do you grant full access to a database?

Using:

GRANT ALL PRIVILEGES ON DATABASE dbname TO username;

Q4. How can you verify database access?

By logging in using the created user and accessing the database.

Q5. Where are PostgreSQL users stored?

Inside PostgreSQL system catalogs, not in Linux OS users.

✅ Task Completed Successfully 🎉
