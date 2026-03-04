# 🌐 Day 42 – Create a Docker Network

## 📌 Scenario

The Nautilus DevOps team needed to enable communication between multiple Docker containers running on the same application server.

To achieve this, a **custom Docker network** needed to be created so containers could communicate using container names instead of IP addresses.

---

## 🎯 Objectives

- Create a custom Docker network
- Verify network creation
- Understand container networking concepts
- Enable inter-container communication

---

## 🛠️ Tasks Performed

### ✅ 1. List Existing Docker Networks

```bash
docker network ls
```
Default networks observed:

bridge
host
none
✅ 2. Create a Custom Docker Network
docker network create my_network

Docker created a new bridge network.

✅ 3. Verify Network Creation
docker network ls

Output confirmed:

my_network
✅ 4. Inspect Network Details
docker network inspect my_network

This command shows:

Subnet

Gateway

Connected containers

Network driver

🔍 Explanation

Docker networks allow containers to:

Communicate with each other

Use container names as DNS

Isolate traffic between services

Default network driver used:

bridge
🧠 Key Learnings

Docker provides three default networks:

bridge

host

none

Custom networks improve container communication

Containers in the same network can resolve names via DNS

Network isolation improves security

docker network inspect is useful for debugging

🎤 Interview Questions
Q1. What is a Docker network?

A virtual network that allows containers to communicate with each other.

Q2. Default Docker network drivers?

bridge

host

none

Q3. Why create a custom network?

For container-to-container communication and isolation.

Q4. How to attach a container to a network?
docker run --network my_network <image>
Q5. How to inspect a Docker network?
docker network inspect <network_name>

✅ Day 42 Task Completed Successfully
