
# 🚀 Day 02 – Temporary User Account with Expiry Date

## 📌 Challenge Description

As part of a temporary assignment, a developer required access for a limited duration.  
The task was to create a user account with a predefined expiry date on a specific server.

This simulates real-world scenarios where contractors, interns, or temporary developers are granted time-bound access for security and audit purposes.

---

## 🎯 Objective

- Create a user named in lowercase as per standard convention.
- Set an account expiry date to automatically disable access.
- Perform the task on the correct application server.
- Verify that the account expiry date is configured correctly.

---

## 🧠 Key Concepts Learned

### ✅ Account Expiry in Linux

Linux allows administrators to define an expiration date for user accounts.  
Once the expiry date is reached:

- The user cannot log in.
- Authentication is automatically blocked.
- No manual deletion is required.
- System audit trails remain intact.

This is commonly used for:
- Contractors
- Temporary employees
- External vendors
- Intern access control

---

### ✅ Difference Between Account Expiry and Password Expiry

Account Expiry:
- Entire account becomes unusable after the specified date.
- Login is completely blocked.

Password Expiry:
- Only the password becomes invalid.
- User must reset the password to continue access.

Both are used for different security purposes.

---

### ✅ User Information Storage

User metadata is maintained internally by the system and linked to:
- `/etc/passwd`
- `/etc/shadow`

These files store user configuration and security policies.

---

### ✅ Privilege Management

Modifying user accounts requires administrative privileges because system files are protected.  
Normal users cannot create or modify user accounts.

Temporary privilege elevation is used to safely perform administrative tasks.

---

### ✅ Server Awareness

In multi-server environments:

- Each server maintains its own users and configurations.
- Changes on one server do not affect others.
- Always verify the server name before executing administrative actions.

---

## ❌ Mistakes and Learning

- Attempted to view account information without sufficient privileges.
- Initially tried incorrect verification syntax.
- Forgot that system-level commands require elevated permissions.

These mistakes helped reinforce security boundaries and correct workflows.

---

## ✅ How the Issue Was Solved

- Verified the correct application server.
- Used temporary administrative privileges.
- Applied the expiry configuration correctly.
- Validated the account expiry information using system tools.

---

## 🔍 Verification Summary

Verification confirmed:

- The user exists in the system.
- The account expiry date is correctly configured.
- Password aging information is visible.
- The system enforces account lifecycle rules.

---

## 💡 Key Takeaways

- Account expiry is essential for secure access control.
- Always validate changes after applying them.
- Permission errors usually indicate missing privileges.
- Server awareness prevents configuration mistakes.
- Automation and security go hand in hand.

---

## 🎤 Interview Preparation Notes

### Q1: Why should temporary users have expiry dates?
To ensure automatic access removal, reduce security risks, and maintain audit compliance.

---

### Q2: What is the difference between account expiry and password expiry?
Account expiry disables the entire user account, while password expiry only forces a password reset.

---

### Q3: Why are administrative privileges required to manage users?
Because user information is stored in protected system files which normal users cannot modify.

---

### Q4: How can you verify user account expiry?
By using system tools that display account aging and expiry information.

---

### Q5: Why is it important to verify the target server before making changes?
Because each server has independent configuration and users.

---

## 📅 Progress Log

Day 02 : Temporary User Account with Expiry Date  ✅ Completed

---

