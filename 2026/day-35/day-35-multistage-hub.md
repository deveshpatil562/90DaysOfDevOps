# 🐳 Docker Challenge – Multi-Stage Builds & Docker Hub

This lab is part of my personal Docker practice repository.  
In this challenge, I explored:

- Why single-stage images are large
- How multi-stage builds reduce image size
- How to push images to Docker Hub
- Docker Hub repository management
- Docker image best practices

---

# 🚀 Task 1: The Problem with Large Images

## 🎯 Objective
- Create a simple app (Node.js Hello World)
- Build it using a **single-stage Dockerfile**
- Check the image size
- Note the size for comparison

---

## 📝 Step 1: Create Simple Node.js App

Create a file `app.js`

```js
console.log("Hello from Docker Single Stage Build!");
```

---

## 🐳 Step 2: Single-Stage Dockerfile

Create a file `Dockerfile`

```dockerfile
# Single Stage Build
FROM node:18

WORKDIR /app

COPY app.js .

CMD ["node", "app.js"]
```

---

## 🏗 Step 3: Build the Image

Run:

[ docker build -t single-stage-app:v1 . ]

---

## 📏 Step 4: Check Image Size

Run:

[ docker images ]

📌 Example Output:

- single-stage-app:v1 → **~900MB (approx depending on base image)**

---

## 📌 Observation

The image is large because:

- Full Node.js image is used
- Contains build tools
- Contains package manager
- Contains unnecessary OS utilities
- Entire runtime environment included

This is inefficient for production.

---

# 🚀 Task 2: Multi-Stage Build

## 🎯 Objective

- Use multi-stage Dockerfile
- Build app in one stage
- Copy only required artifacts into minimal image
- Compare sizes

---

## 🐳 Multi-Stage Dockerfile

```dockerfile
# Stage 1: Builder
FROM node:18 AS builder

WORKDIR /app
COPY app.js .

# Stage 2: Minimal Runtime
FROM node:18-alpine

WORKDIR /app
COPY --from=builder /app/app.js .

CMD ["node", "app.js"]
```

---

## 🏗 Build Multi-Stage Image

[ docker build -t multi-stage-app:v1 . ]

---

## 📏 Check Image Size Again

[ docker images ]

📌 Example Comparison:

- single-stage-app:v1 → ~900MB  
- multi-stage-app:v1 → ~120MB  

---

## 🧠 Why is Multi-Stage Smaller?

- Builder tools are discarded
- Only required artifacts are copied
- Minimal base image (alpine)
- Fewer layers
- No unnecessary dependencies

Multi-stage keeps runtime clean and production-ready.

---

# 🚀 Task 3: Push to Docker Hub

## 🎯 Objective

- Create Docker Hub account
- Login from terminal
- Tag image properly
- Push image
- Verify by pulling again

---

## 🔐 Login to Docker Hub

[ docker login ]

Enter Docker Hub credentials.

---

## 🏷 Tag Image

[ docker tag multi-stage-app:v1 yourusername/multi-stage-app:v1 ]

---

## 📤 Push Image

[ docker push yourusername/multi-stage-app:v1 ]

---

## 🧪 Verify by Pulling

Remove local image:

[ docker rmi yourusername/multi-stage-app:v1 ]

Pull again:

[ docker pull yourusername/multi-stage-app:v1 ]

If it pulls successfully → Push verified ✅

---

# 🚀 Task 4: Docker Hub Repository

## 🎯 Objective

- Check repository on Docker Hub
- Add description
- Explore tags
- Understand versioning

---

## 🔎 Steps

1. Login to Docker Hub website
2. Open your repository
3. Add description (About this image)
4. Go to **Tags tab**

---

## 🏷 Understanding Tags

When pulling:

[ docker pull yourusername/multi-stage-app:v1 ]

You get exact version.

When pulling:

[ docker pull yourusername/multi-stage-app:latest ]

You get the image tagged as latest.

⚠ If no tag specified:

[ docker pull yourusername/multi-stage-app ]

Docker automatically pulls `latest`.

---

# 🚀 Task 5: Image Best Practices

Now we improve our Dockerfile.

---

## 🐳 Optimized Production Dockerfile

```dockerfile
# Stage 1: Builder
FROM node:18.19.0-alpine AS builder

WORKDIR /app
COPY app.js .

# Stage 2: Minimal Runtime
FROM node:18.19.0-alpine

WORKDIR /app

# Create non-root user
RUN adduser -D appuser

COPY --from=builder /app/app.js .

USER appuser

CMD ["node", "app.js"]
```

---

## ✅ Best Practices Applied

✔ Use minimal base image (alpine instead of full node)  
✔ Use specific version tag (not latest)  
✔ Use multi-stage build  
✔ Run container as non-root user  
✔ Keep image minimal  

---

## 📏 Compare Sizes Again

[ docker images ]

Observe difference between:

- node:18
- node:18-alpine
- optimized multi-stage image

Alpine-based images are significantly smaller.

---

# 🧠 Key Learnings

- Single-stage images are heavy
- Multi-stage builds reduce size drastically
- Smaller images:
  - Build faster
  - Deploy faster
  - More secure
  - Consume less storage
- Docker Hub tagging is critical for version control
- Never use `latest` in production blindly
- Avoid running containers as root

---

# 🏁 Final Summary

In this lab I:

✔ Built single-stage image  
✔ Compared size  
✔ Implemented multi-stage build  
✔ Reduced image size significantly  
✔ Pushed image to Docker Hub  
✔ Verified pull  
✔ Applied production best practices  

---

This challenge strengthened my understanding of:

- Docker image optimization
- Multi-stage builds
- Docker Hub workflow
- Production-grade Dockerfile writing

---

📌 End of Docker Multi-Stage & Docker Hub Challenge
