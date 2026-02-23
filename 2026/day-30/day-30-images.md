# Day 30 – Docker Images & Container Lifecycle

## 🎯 Goal
Understand how Docker images and containers actually work, including:
- Relationship between images and containers
- Image layers & caching
- Full container lifecycle
- Working with running containers
- Proper cleanup

---

# 🧠 Theory Notes

## 🔹 Images vs Containers

- **Image** = Blueprint (Read-only template)
- **Container** = Running instance of an image
- One image → Multiple containers possible

Example:
An `nginx` image can be used to create multiple running Nginx containers.

---

## 🔹 What Are Image Layers?

- Docker images are built in **layers**
- Each instruction in a Dockerfile creates a new layer
- Layers are:
  - Cached
  - Reusable
  - Read-only

Why Docker uses layers:
- Faster builds (layer caching)
- Efficient storage
- Easy image distribution

---

# 🚀 Task 1: Docker Images

## ✅ Pull Required Images

[ docker pull nginx ]  
[ docker pull ubuntu ]  
[ docker pull alpine ]

---

## ✅ List All Images

[ docker images ]

📌 Observations:
- `ubuntu` is much larger (~70MB+)
- `alpine` is very small (~5MB)

### 🤔 Why is Alpine smaller?
- Alpine is a minimal Linux distribution
- Uses musl instead of glibc
- Designed for containers
- Fewer packages preinstalled

---

## ✅ Inspect an Image

[ docker inspect nginx ]

Information visible:
- Image ID
- Layers
- Environment variables
- Entrypoint
- Working directory
- OS & architecture

---

## ✅ Remove an Unused Image

[ docker rmi ubuntu ]

---

# 🧱 Task 2: Image Layers

## ✅ View Image History

[ docker image history nginx ]

Observations:
- Each row represents a layer
- Some layers show sizes (files added)
- Some show 0B (metadata instructions)

📌 Notes:
Layers make Docker builds efficient and cacheable.

---

# 🔄 Task 3: Container Lifecycle

Practiced full lifecycle using one container.

## ✅ Create Container (Without Starting)

[ docker create --name container-lifecycle nginx ]

Status: Created

---

## ✅ Start Container

[ docker start container-lifecycle ]

Status: Up

---

## ✅ Pause Container

[ docker pause container-lifecycle ]

Check status:

[ docker ps -a ]

Status: Paused

---

## ✅ Unpause Container

[ docker unpause container-lifecycle ]

Status: Running

---

## ✅ Stop Container

[ docker stop container-lifecycle ]

Status: Exited

---

## ✅ Restart Container

[ docker restart container-lifecycle ]

Status: Up

---

## ✅ Kill Container

[ docker kill container-lifecycle ]

Status: Exited (137)

---

## ✅ Remove Container

[ docker rm container-lifecycle ]

---

## 📌 After Each Step

Checked container state using:

[ docker ps -a ]

Observed transitions:
- Created → Up → Paused → Running → Exited

---

# 🌐 Task 4: Working with Running Containers

## ✅ Run Nginx in Detached Mode

[ docker run -d -p 80:80 --name nginx-server nginx ]

---

## ✅ View Logs

[ docker logs nginx-server ]

---

## ✅ Follow Logs (Real-Time)

[ docker logs -f nginx-server ]

---

## ✅ Exec Into Container

[ docker exec -it nginx-server /bin/sh ]

Explore filesystem:
[ ls ]
[ cd /usr/share/nginx/html ]
[ pwd ]

---

## ✅ Run Single Command Without Entering

[ docker exec nginx-server ls / ]

---

## ✅ Inspect Container

[ docker inspect nginx-server ]

Important details found:
- Container IP Address
- Port mappings (0.0.0.0:80 → 80/tcp)
- Mount points
- Network settings

---

# 🧹 Task 5: Cleanup

## ✅ Stop All Running Containers

[ docker stop $(docker ps -q) ]

---

## ✅ Remove All Stopped Containers

[ docker container prune ]

---

## ✅ Remove Unused Images

[ docker image prune ]

---

## ✅ Check Docker Disk Usage

[ docker system df ]

---

## 💡 Bonus Cleanup (Optional)

[ docker system prune ]

Removes:
- Stopped containers
- Unused networks
- Dangling images
- Build cache

---

# 📸 Screenshots

✔ docker images output  
✔ docker image history nginx  
✔ container lifecycle transitions  
✔ docker inspect output  
✔ cleanup commands  

---

# 📂 Submission

File Location:
`2026/day-30/day-30-images.md`

## Final Steps:

[ git add 2026/day-30/day-30-images.md ]  
[ git commit -m "Day 30 - Docker Images & Container Lifecycle" ]  
[ git push origin main ]

---

# 🚀 Key Learnings

- Images are blueprints
- Containers are running instances
- Layers improve efficiency
- Lifecycle management is critical
- Cleanup prevents disk bloat

---

🔥 Day 30 Completed – Docker Deep Dive  
DevOps 90 Days Journey Continues!
