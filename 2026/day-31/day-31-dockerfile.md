# Day 31 – Dockerfile: Build Your Own Images

## 🚀 Objective

Today’s goal is to write Dockerfiles and build custom images.

This is the skill that separates someone who **uses Docker** from someone who actually **ships with Docker**.

---

# 📦 Task 1: Your First Dockerfile

## Step 1: Create Project Folder

[mkdir my-first-image]  
[cd my-first-image]

## Step 2: Create Dockerfile

Create a file named `Dockerfile`

```Dockerfile
FROM ubuntu:latest

RUN apt-get update && apt-get install -y curl

CMD ["echo", "Hello from my custom image!"]
```

## 🔎 Explanation

- **FROM ubuntu:latest** → Base image.
- **RUN apt-get update && apt-get install -y curl** → Installs curl during build time.
- **CMD** → Default command executed when container runs.

## Step 3: Build Image

[docker build -t my-ubuntu:v1 .]

⚠ The `.` at the end represents the **build context** (current directory).

## Step 4: Run Container

[docker run my-ubuntu:v1]

✅ Output should print:

```
Hello from my custom image!
```

---

# 📘 Task 2: Understanding Dockerfile Instructions

Create another Dockerfile:

```Dockerfile
FROM ubuntu:latest

WORKDIR /app

RUN apt-get update && apt-get install -y curl

COPY . .

EXPOSE 8080

CMD ["bash"]
```

## 🔎 Instruction Breakdown

- **FROM** → Base image.
- **WORKDIR** → Sets working directory inside container.
- **RUN** → Executes commands at build time.
- **COPY . .** → Copies all files from host to container.
- **EXPOSE 8080** → Documents that container uses port 8080.
- **CMD** → Default runtime command.

## Build & Run

[docker build -t dockerfile-demo:v1 .]  
[docker run -it dockerfile-demo:v1]

---

# ⚖ Task 3: CMD vs ENTRYPOINT

## Image 1: Using CMD

```Dockerfile
FROM ubuntu
CMD ["echo", "hello"]
```

Build:

[docker build -t cmd-demo .]

Run:

[docker run cmd-demo]

Override command:

[docker run cmd-demo ls]

### 🧠 What happens?
- CMD gets replaced if a new command is passed.

---

## Image 2: Using ENTRYPOINT

```Dockerfile
FROM ubuntu
ENTRYPOINT ["echo"]
```

Build:

[docker build -t entry-demo .]

Run:

[docker run entry-demo hello world]

### 🧠 What happens?
- ENTRYPOINT does NOT get replaced.
- Arguments get appended.

---

## 📌 When to Use?

| CMD | ENTRYPOINT |
|------|------------|
| Default command | Fixed executable |
| Easily overridden | Used for CLI-style containers |

Use **CMD** for flexibility.  
Use **ENTRYPOINT** when container behaves like a command/tool.

---

# 🌐 Task 4: Build a Simple Web App Image

## Step 1: Create index.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Docker Website</title>
</head>
<body>
    <h1>Hello from my Nginx Docker Image 🚀</h1>
</body>
</html>
```

## Step 2: Create Dockerfile

```Dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html
```

📌 Nginx serves files from:  
`/usr/share/nginx/html/`

## Step 3: Build Image

[docker build -t my-website:v1 .]

## Step 4: Run Container

[docker run -d -p 8080:80 my-website:v1]

Open browser:

http://localhost:8080

✅ Your custom static website should load.

---

# 🚫 Task 5: .dockerignore

Create `.dockerignore`

```
node_modules
.git
*.md
.env
```

## Why?

- Prevent unnecessary files from being sent in build context.
- Improves build speed.
- Reduces image size.
- Improves security.

Rebuild image:

[docker build -t optimized-image:v1 .]

Verify ignored files are not included.

---

# ⚡ Task 6: Build Optimization & Layer Caching

## Test Docker Cache

Build image:

[docker build -t cache-demo:v1 .]

Change one line in Dockerfile and rebuild:

[docker build -t cache-demo:v2 .]

You will notice:

```
CACHED
```

Docker reuses unchanged layers.

---

## 🔎 Why Layer Order Matters?

Docker builds images in layers.

Each instruction = one layer.

If you change a layer:
- All layers below it rebuild.

### 🔥 Best Practice

Put:
- Frequently changing lines → LAST
- Stable dependencies → FIRST

Example (Optimized):

```Dockerfile
FROM ubuntu:latest

RUN apt-get update && apt-get install -y curl

COPY . .
```

This way dependency install is cached unless base changes.

---

# 📂 Submission

Add files to:

```
2026/day-31/
```

Include:
- All Dockerfiles
- day-31-dockerfile.md

Commit & Push:

[git add .]  
[git commit -m "Day 31 - Dockerfile: Build Your Own Images"]  
[git push]

---

# 🌍 Learn in Public

Share:
- Your custom Docker image
- Nginx website screenshot
- Caching demo screenshot

Use hashtags:

#90DaysOfDevOps  
#DevOpsKaJosh  
#TrainWithShubham  

---

## 🎯 What You Learned Today

- Writing Dockerfiles
- Building custom images
- Understanding layers
- CMD vs ENTRYPOINT difference
- Nginx container customization
- Docker build cache optimization
- Importance of .dockerignore

---

🔥 Day 31 Complete.  
Happy Learning! TrainWithShubham 🚀
