# 🚀 Day 29 – Introduction to Docker

## 🎯 Task Overview

Today’s goal was to understand what Docker is and run my first container.

### ✅ Objectives
- Learn why containers exist and how they differ from Virtual Machines
- Install Docker
- Run and explore containers from Docker Hub
- Work with real containers (Nginx & Ubuntu)
- Practice core Docker commands

---

# 📚 Task 1: What is Docker?

## 🐳 What is Docker?

Docker is a containerization platform that allows developers to package applications with their dependencies into lightweight, portable containers.

### 📦 What is a Container?

A container is a lightweight, isolated environment that includes:
- Application code
- Runtime
- Libraries
- Dependencies

### ❓ Why Do We Need Containers?

- Solve “It works on my machine” problem
- Consistent development & production environments
- Faster deployment
- Lightweight and efficient
- Easy scalability

---

## 🖥 Containers vs Virtual Machines

| Feature | Virtual Machine | Container |
|----------|----------------|------------|
| OS | Each VM has its own OS | Shares host OS |
| Size | Large (GBs) | Small (MBs) |
| Boot Time | Minutes | Seconds |
| Performance | Slower | Faster |
| Resource Usage | Heavy | Lightweight |

### 🔥 Real Difference
VMs virtualize hardware.  
Containers virtualize the OS layer.

---

## 🏗 Docker Architecture

Docker follows a client-server architecture:

User → Docker Client → Docker Daemon → Images/Containers → Docker Registry

### 🔹 Docker Client
Used to run commands like:
[docker run nginx]

### 🔹 Docker Daemon
Background service that:
- Builds images
- Runs containers
- Manages networks & volumes

### 🔹 Docker Images
Blueprint for containers.

### 🔹 Docker Containers
Running instances of images.

### 🔹 Docker Registry
Stores Docker images (e.g., Docker Hub).

---

# ⚙ Task 2: Install Docker

## ✅ Verify Installation

[docker --version]

## ✅ Run Hello World Container

[docker run hello-world]

### 🔎 What Happened?

1. Docker client contacted the daemon
2. Image pulled from Docker Hub
3. Container created
4. Container executed program
5. Output streamed to terminal

---

## 📸 Hello World Output Screenshot

![Hello World Output](./bdf319cc-1e49-4cf1-9f6e-f1feaab786b6.png)

---

# 🐳 Task 3: Run Real Containers

## 🌐 Run Nginx Container

[docker run -d -p 80:80 nginx]

Access in browser:
http://localhost

## 🐧 Run Ubuntu in Interactive Mode

[docker run -it ubuntu]

Explore inside container:
[ls]  
[pwd]  
[whoami]

Exit container:
[exit]

---

## 📋 List Running Containers

[docker ps]

## 📋 List All Containers

[docker ps -a]

---

## 🛑 Stop a Container

[docker stop container_name]

## ❌ Remove a Container

[docker rm container_name]

---

## 📸 Running Containers Screenshot

![Running Containers](./bdf319cc-1e49-4cf1-9f6e-f1feaab786b6.png)

---

# 🔍 Task 4: Explore Docker Features

## 🟢 Detached Mode

[docker run -d nginx]

Runs container in background.

---

## 🏷 Custom Name

[docker run -d --name mynginx nginx]

---

## 🔌 Port Mapping

[docker run -d -p 8080:80 nginx]

Maps host port 8080 to container port 80.

---

## 📜 Check Logs

[docker logs container_name]

---

## 🖥 Execute Inside Running Container

[docker exec -it container_name /bin/bash]

---

# 💡 Important Flags Learned

- -it → Interactive mode
- -d → Detached mode
- -p → Port mapping
- --name → Custom container name
- docker logs → View logs
- docker exec → Execute command inside container

---

# 🎯 Why This Matters for DevOps

Docker is the foundation of modern deployment.

Every:
- CI/CD pipeline
- Kubernetes cluster
- Microservice architecture

Starts with containers.

Today marks my first practical step into containerization and DevOps 🚀

---

# ✅ Day 29 Summary

✔ Understood containers  
✔ Compared Containers vs VMs  
✔ Learned Docker architecture  
✔ Installed Docker  
✔ Ran hello-world  
✔ Deployed Nginx  
✔ Explored Ubuntu interactively  
✔ Managed container lifecycle  

---

**Author:** Devesh Patil  
**Journey:** DevOps | Cloud | Containers  
