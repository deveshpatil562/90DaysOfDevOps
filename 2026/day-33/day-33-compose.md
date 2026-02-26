# 🚀 Day 33 – Docker Compose: Multi-Container Basics

## 🎯 Task
Today's goal is to run multi-container applications using a single command with Docker Compose.

Instead of manually creating:
- Containers
- Networks
- Volumes

Docker Compose allows defining everything inside one `docker-compose.yml` file.

---

# 🧪 Task 1: Install & Verify

## ✅ Check Docker Compose Version
[docker compose version]

## ✅ Verify Docker is Running
[docker info]

Docker Compose is successfully available and working.

---

# 🧪 Task 2: Your First Compose File (Single Nginx Container)

## Step 1: Create Project Folder
[mkdir compose-basics]  
[cd compose-basics]

## Step 2: Create docker-compose.yml
[vim docker-compose.yml]

### docker-compose.yml

```yaml
services:
  nginx:
    image: nginx:latest
    container_name: nginx-compose
    ports:
      - "80:80"
```

## Step 3: Start Service
[docker compose up -d]

## Verify Running Container
[docker compose ps]

## 🌐 Access in Browser
http://192.168.31.96

### 📸 Screenshot
(Add your Nginx screenshot here)

Successfully accessed Nginx static page.

## Stop & Remove
[docker compose down]

This removed:
- Containers
- Default network

---

# 🧪 Task 3: Two-Container Setup (WordPress + MySQL)

Created a multi-container application.

## docker-compose.yml

```yaml
services:
  db:
    image: mysql:8.0
    container_name: wordpress-db
    restart: always
    environment:
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
      MYSQL_ROOT_PASSWORD: root
    volumes:
      - db-data:/var/lib/mysql

  wordpress:
    image: wordpress:latest
    container_name: wordpress-app
    restart: always
    ports:
      - "8008:80"
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
    depends_on:
      - db

volumes:
  db-data:
```

## Start Application
[docker compose up -d]

## Verify Services
[docker compose ps]

## 🌐 Access WordPress
http://192.168.31.96:8008

Completed WordPress setup successfully.

### 📸 Screenshot
(Add your WordPress setup screenshot here)

---

## 🔁 Persistence Test

Stop services:
[docker compose down]

Start again:
[docker compose up -d]

✔ WordPress data remained intact.  
✔ Named volume ensured persistence.

---

# 🧪 Task 4: Compose Commands Practice

## Start in Detached Mode
[docker compose up -d]

## View Running Services
[docker compose ps]

## View Logs (All Services)
[docker compose logs]

## Follow Logs
[docker compose logs -f]

## View Logs of Specific Service
[docker compose logs wordpress]

## Stop Services Without Removing
[docker compose stop]

## Remove Containers & Networks
[docker compose down]

## Remove Including Volumes
[docker compose down -v]

## Rebuild Images After Change
[docker compose up -d --build]

---

# 🧪 Task 5: Environment Variables

## Add Variables Directly in Compose File

```yaml
environment:
  MYSQL_DATABASE: wordpress
  MYSQL_USER: wordpress
```

---

## Create .env File
[vim .env]

Add:

MYSQL_DATABASE=wordpress  
MYSQL_USER=wordpress  
MYSQL_PASSWORD=wordpress  
MYSQL_ROOT_PASSWORD=root  

---

## Reference Variables in docker-compose.yml

```yaml
environment:
  MYSQL_DATABASE: ${MYSQL_DATABASE}
  MYSQL_USER: ${MYSQL_USER}
```

---

## Verify Variables Are Picked Up

[docker compose config]

OR

[docker compose exec db env]

Environment variables successfully loaded from `.env` file.

---

# 🧠 Key Learnings

- Docker Compose automatically creates a default network.
- Service names act as DNS names.
- Named volumes provide data persistence.
- Multi-container apps can be managed with a single command.
- `.env` helps manage configuration cleanly.

---

# 📂 Submission

Added files to:

2026/day-33/

- day-33-compose.md
- docker-compose.yml files

Committed and pushed to repository.

---

# 🌍 Learn in Public

Shared WordPress + MySQL running via Docker Compose on LinkedIn.

#90DaysOfDevOps  
#DevOpsKaJosh  
#TrainWithShubham  

Happy Learning 🚀
