🚀 Day 01 – Linux User Management (Non-Interactive User)
📌 Challenge Description

The task was to create a user with a non-interactive shell on App Server 3 to support a backup agent tool.
Service users should not be able to log in interactively for security reasons.

🎯 Objective

Create a user account named as required.

Assign a non-interactive shell so that the user cannot log in.

Perform the task on the correct server node.

Verify that the user behaves as expected.

🧠 Key Concepts Learned
✅ Non-Interactive Shell

A non-interactive shell prevents users from logging into the system via SSH or terminal.
Common non-interactive shells:

/sbin/nologin

/bin/false

These are commonly used for:

Backup agents

Monitoring services

Automation users

System daemons

This improves security by preventing misuse of service accounts.

✅ Linux User Information Storage

User details are stored in:

/etc/passwd


Each entry contains:

username : password : UID : GID : comment : home : shell


The last field defines which shell the user uses when logging in.

✅ Privilege Management

Only administrative users can modify system files like:

/etc/passwd

/etc/shadow

/etc/group

Normal users cannot create new users without elevated privileges.

Temporary privilege escalation is required for administrative tasks.

✅ Server Awareness

In multi-server environments:

Each server has its own users and configuration.

Creating a user on one server does not affect another server.

Always verify which server you are connected to before executing commands.

❌ Mistakes I Made

Created the user on the wrong server initially.

Attempted user creation without admin privileges and received permission errors.

Tried switching to a non-interactive user account (login failed, which is expected behavior).

Confused by permission errors while accessing the user home directory.

✅ How I Fixed Them

Verified the hostname to ensure I was on the correct server.

Used temporary administrative privileges to execute system-level commands.

Re-ran the user creation logic correctly.

Verified the user configuration by checking system files and access behavior.

🔍 Verification Steps

Confirmed that the user exists in the system.

Checked that the assigned shell is a non-interactive shell.

Attempted to switch user and observed login restriction.

Verified permissions on the home directory.

💡 Key Takeaways

Always verify the target server before executing changes.

Permission errors usually indicate missing privileges.

Service users should never have interactive login access.

Validation is as important as execution.

Debugging systematically prevents wasted time.
