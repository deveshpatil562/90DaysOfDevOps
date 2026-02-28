# Day 34 – Docker Compose: Real-World Multi-Container Apps

## 🎯 Objective

Today's goal was to build a production-like multi-container application using Docker Compose.

Instead of running single containers, this task focuses on:

- App + Database + Cache architecture
- Service communication
- Restart policies
- Real-world stack structure

---

# 🏗 Architecture Overview

This stack includes:

1️⃣ Web Application – Python Flask  
2️⃣ Database – MySQL 8.0  
3️⃣ Cache – Redis 7  


---

# 🔹 Task 1 – Build Your Own App Stack ✅ (Completed)

## 🧾 docker-compose.yml

[docker-compose.yml]

[
version: "3.9"

services:
  web:
    build: ./web
    ports:
      - "5000:5000"
    environment:
      - DATABASE_URL=mysql+pymysql://root:rootpassword@db:3306/mydb
      - REDIS_URL=redis://cache:6379/0
    depends_on:
      - db
      - cache

  db:
    image: mysql:8.0
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: mydb
    volumes:
      - db_data:/var/lib/mysql

  cache:
    image: redis:7
    restart: always

volumes:
  db_data:
]

---

## 🐳 Web Application Dockerfile

[web/Dockerfile]

[
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
]

---

## 🐍 Flask Application Code

[web/app.py]

[
from flask import Flask, render_template

app = Flask(__name__)

@app.route("/")
def home():
    return render_template("index.html")

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
]

---

# 🚀 How to Run the Stack

Start all services:

[docker compose up -d]

View logs:

[docker compose logs -f]

Stop everything:

[docker compose down]

Rebuild after code changes:

[docker compose up --build]

---

# 🗄 Database Configuration

- Image: mysql:8.0
- Root password: rootpassword
- Database created automatically: mydb
- Persistent storage using named volume: db_data
- Restart policy: always

The volume ensures data persists even if the container stops or is removed.

---

# 🔴 Redis Cache

- Image: redis:7
- Restart policy: always
- Internal communication via service name: cache

Redis runs internally and is accessible from the web container using:

redis://cache:6379/0

---

# 🔗 Service Communication

Docker Compose creates a default internal network.

Services communicate using service names:

- db
- cache
- web

The web app connects to MySQL using:

db:3306

NOT localhost.

---

# 🔹 Task 2 – depends_on & Healthchecks ❌ (Not Implemented Yet)

Currently using basic depends_on:

[
depends_on:
  - db
  - cache
]

This ensures container startup order but does NOT wait for DB readiness.

Healthcheck with condition: service_healthy will be implemented in next update.

---

# 🔹 Task 3 – Restart Policies ✅ (Partially Implemented)

Database and Redis use:

[
restart: always
]

### Behavior Observed:
If the container is manually killed, Docker automatically restarts it.

### When to use:
- restart: always → Production services that must stay running
- restart: on-failure → Jobs or services that may fail temporarily

---

# 🔹 Task 4 – Custom Dockerfile in Compose ✅ (Completed)

Instead of using a prebuilt image, the web service uses:

[
build: ./web
]

This allows:
- Custom dependencies
- Code changes
- Full control over the image

Rebuild with one command:

[docker compose up --build]

---

# 🔹 Task 5 – Named Volumes ✅ (Completed)

Defined named volume:

[
volumes:
  db_data:
]

Mounted to:

[
- db_data:/var/lib/mysql
]

This ensures database data persistence.

---

# 🔹 Task 6 – Scaling (Bonus) ❌ Not Performed

Scaling was not implemented in this task.

Example command (not executed):

[docker compose up --scale web=3]

Why scaling may break:
Port mapping 5000:5000 conflicts when multiple replicas try to bind the same host port.

To scale properly, a reverse proxy or load balancer would be required.

---

# 📌 What I Learned

- How to build multi-container applications
- Docker Compose service communication
- Named volumes for persistence
- Restart policies in production
- Custom Dockerfile integration
- Difference between container startup and service readiness

---

# 📂 GitHub Repository

All files are pushed here:

https://github.com/deveshpatil562/Docker-Labs/tree/main/day-34

---

# 🏁 Conclusion

Day 34 helped me understand how real-world applications are structured using Docker Compose.

This is no longer just running containers — this is building application stacks.

More advanced configurations (healthchecks & scaling) will be implemented in upcoming updates.
All services are managed using Docker Compose.

---



