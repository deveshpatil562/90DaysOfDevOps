# Day 32 – Docker Volumes & Networking

## 🎯 Goal
Today’s mission was to solve two real-world Docker problems:

- **Data Persistence**
- **Container Communication**

Containers are **ephemeral** — when removed, their data is gone.  
By default, containers also **cannot easily communicate by name**.

Today I fixed both. 🚀

---

# 🔥 Task 1: The Problem (Data Loss Without Volumes)

### Step 1: Run a Database Container
[ docker run -d --name mydb -e POSTGRES_PASSWORD=pass postgres ]

### Step 2: Create Sample Data
[ docker exec -it mydb psql -U postgres ]  
Create a table and insert rows.

### Step 3: Stop & Remove Container
[ docker stop mydb ]  
[ docker rm mydb ]

### Step 4: Run New Container
[ docker run -d --name mydb -e POSTGRES_PASSWORD=pass postgres ]

### ❓ What Happened?
The data was **gone**.

### 🧠 Why?
Because containers are temporary.  
Without a volume, data is stored inside the container filesystem — which is deleted when the container is removed.

📸 _Add Screenshot: Before & After Data Removal_

---

# 💾 Task 2: Named Volumes (Data Persistence)

### Step 1: Create Named Volume
[ docker volume create my-db-volume ]

### Step 2: Run Database with Volume
[ docker run -d --name mydb -e POSTGRES_PASSWORD=pass -v my-db-volume:/var/lib/postgresql/data postgres ]

### Step 3: Add Data
[ docker exec -it mydb psql -U postgres ]

### Step 4: Remove Container
[ docker stop mydb ]  
[ docker rm mydb ]

### Step 5: Run New Container with Same Volume
[ docker run -d --name mydb -e POSTGRES_PASSWORD=pass -v my-db-volume:/var/lib/postgresql/data postgres ]

### ✅ Result
Data was still there 🎉

### 🔍 Verification
[ docker volume ls ]  
[ docker volume inspect my-db-volume ]

📸 _Add Screenshot: Volume Inspection_

### 🧠 Why It Worked
Named volumes store data outside the container lifecycle.  
Even if the container is deleted, the volume remains.

---

# 📂 Task 3: Bind Mounts

### Step 1: Create Folder on Host
Create folder and add index.html.

### Step 2: Run Nginx with Bind Mount
[ docker run -d --name mynginx -p 8080:80 -v /host/path:/usr/share/nginx/html nginx ]

### Step 3: Access in Browser
Open: http://localhost:8080

You should see:

> Hello from Bind Mount!

📸 _Add Screenshot: Browser Output_

### Step 4: Edit index.html on Host
Refresh browser → Changes appear instantly 🔥

---

### 📘 Difference: Named Volume vs Bind Mount

| Named Volume | Bind Mount |
|--------------|------------|
| Managed by Docker | Managed by Host |
| Stored in Docker directory | Directly maps host folder |
| Best for databases | Best for development |
| More portable | Depends on host path |

---

# 🌐 Task 4: Docker Networking Basics

### List Networks
[ docker network ls ]

### Inspect Default Bridge
[ docker network inspect bridge ]

### Run Two Containers on Default Bridge
[ docker run -dit --name c1 ubuntu ]  
[ docker run -dit --name c2 ubuntu ]

### Try Ping by Name
[ docker exec c1 ping c2 ]

❌ Does NOT work (name resolution fails)

### Try Ping by IP
[ docker inspect c2 ]

[ docker exec c1 ping <container_ip> ]

✅ Works

### 🧠 Why?
Default bridge does not provide automatic DNS resolution.

---

# 🌉 Task 5: Custom Networks

### Create Custom Network
[ docker network create my-app-net ]

### Run Containers on Custom Network
[ docker run -dit --name c1 --network my-app-net ubuntu ]  
[ docker run -dit --name c2 --network my-app-net ubuntu ]

### Ping by Name
[ docker exec c1 ping c2 ]

✅ Works perfectly 🎉

### 🧠 Why Custom Network Works?
User-defined bridge networks include automatic DNS resolution.  
Containers can communicate using container names.

---

# 🧩 Task 6: Put It All Together

### 1️⃣ Create Custom Network
[ docker network create my-app-net ]

### 2️⃣ Run Database with Volume on Network
[ docker run -d --name mydb --network my-app-net -e POSTGRES_PASSWORD=pass -v my-db-volume:/var/lib/postgresql/data postgres ]

### 3️⃣ Run App Container on Same Network
[ docker run -dit --name myapp --network my-app-net ubuntu ]

### 4️⃣ Verify Communication
[ docker exec myapp ping mydb ]

✅ App container can reach database using container name.

---

# 🚀 Key Learnings

✔ Containers are ephemeral  
✔ Volumes solve data persistence  
✔ Named volumes are best for databases  
✔ Bind mounts are best for development  
✔ Default bridge has limited DNS  
✔ Custom networks enable name-based communication  

---

# 💡 Aha Moment

Deleting a container without a volume = Losing data permanently.

That moment hits hard 😅

---

# 📂 Submission

- Add `day-32-volumes-networking.md` to `2026/day-32/`
- Commit & Push

[ git add . ]  
[ git commit -m "Day 32 - Docker Volumes & Networking" ]  
[ git push origin main ]

---

# 🌍 Learn in Public

Sharing today’s lesson on LinkedIn 🚀  

#90DaysOfDevOps  
#DevOpsKaJosh  
#TrainWithShubham  

---

**Happy Learning! 🚀**  
TrainWithShubham
