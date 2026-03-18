```markdown
# 🚀 Kubernetes Architecture and Cluster Setup

> Welcome to the real DevOps world.  
> You are moving from **running containers → orchestrating distributed systems**.

---

# 📘 1. Concept First (Strong Foundation)

## 🔥 Why Kubernetes?

Docker helps you:
- Build containers
- Run containers on a single host

❌ But Docker alone cannot:
- Manage hundreds of containers across multiple servers
- Auto-heal failed containers
- Perform auto-scaling
- Handle service discovery & networking

👉 Kubernetes solves this by acting as a **container orchestration platform**

---

## 🧠 Kubernetes Story (Recall + Verified)

### ✍️ Your Recall (Before Docs)
```

Kubernetes was created to manage containerized applications at scale.
It solves problems like scaling, self-healing, and multi-node deployments.
It was built by Google based on Borg.
Kubernetes means "helmsman" or "ship pilot".

```

### ✅ Mentor Validation
✔️ Correct — focus on:
- **Automation**
- **Distributed systems management**

---

## 🏗️ Kubernetes Architecture

### 🔷 Control Plane (Brain)

- API Server → Entry point (kubectl communicates here)
- etcd → Stores cluster state (key-value DB)
- Scheduler → Assigns pods to nodes
- Controller Manager → Maintains desired state

---

### 🔷 Worker Node (Execution Layer)

- kubelet → Communicates with API server, manages pods
- kube-proxy → Handles networking
- Container Runtime → Runs containers (containerd / CRI-O)

---

## 🔄 Request Flow

### Command:
[ kubectl apply -f pod.yaml ]

### Flow:
1. kubectl → API Server
2. API Server → stores data in etcd
3. Scheduler → selects node
4. kubelet → pulls image & runs container
5. Controller → ensures desired state

---

## ⚠️ Failure Scenarios

- API Server Down → ❌ Cluster becomes unusable
- Worker Node Down → ✅ Pods rescheduled automatically

---

# 🛠️ 2. Hands-On Tasks

---

# ✅ Task 1: Kubernetes Story

### ✔️ Final Answer
```

Kubernetes is a container orchestration platform that manages applications across multiple nodes. It was created by Google based on Borg to solve scaling and automation challenges. It handles deployment, scaling, and self-healing of containers. The name Kubernetes means "helmsman".

```

---

# 🎯 Task 2: Architecture Diagram

```

```
            +----------------------+
            |     API Server       |
            +----------+-----------+
                       |
    +------------------+------------------+
    |                                     |
```

+----v-----+                         +------v------+
|   etcd   |                         | Scheduler   |
+----------+                         +-------------+
|
+----v-----------------------------+
| Controller Manager              |
+---------------------------------+

```
      Worker Nodes
```

+-----------------------------------+
| kubelet | kube-proxy | runtime    |
+-----------------------------------+

```

---

## 🔍 Verification Answers

### Q: What happens on apply?
✔️ API → etcd → Scheduler → kubelet → Pod runs

### Q: API Server down?
❌ No operations possible

### Q: Worker node down?
✔️ Pods rescheduled

---

# 🧰 Task 3: Install kubectl

## Linux Installation
[
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
]

## Verify
[ kubectl version --client ]

### 📸 Screenshot
```

[ Screenshot: kubectl version ]

```

---

# ⚙️ Task 4: Setup Cluster

## ✅ Option A: kind (Recommended)

### Install
[
curl -Lo ./kind https://kind.sigs.k8s.io/dl/latest/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
]

---

### Create Cluster
[
kind create cluster --name devops-cluster
]

---

### Verify
[
kubectl cluster-info
kubectl get nodes
]

### 📸 Screenshot
```

[ Screenshot: kubectl get nodes ]

```

---

## 🧠 Choice
```

I chose KIND because it is lightweight, fast, and uses Docker internally.

```

---

# 🔍 Task 5: Explore Cluster

## Commands
[
kubectl cluster-info
kubectl get nodes
kubectl describe node <node-name>
kubectl get namespaces
kubectl get pods -A
]

---

## Check System Pods
[
kubectl get pods -n kube-system
]

---

## 🧠 Mentor Insight

These pods represent Kubernetes components:
- kube-apiserver
- etcd
- kube-scheduler
- kube-controller-manager
- coredns
- kube-proxy

---

## ✅ Mapping

| Component | Pod |
|----------|-----|
| API Server | kube-apiserver |
| etcd | etcd |
| Scheduler | kube-scheduler |
| Controller | kube-controller-manager |

---

### 📸 Screenshot
```

[ Screenshot: kube-system pods ]

```

---

# 🔁 Task 6: Cluster Lifecycle

## Delete Cluster
[
kind delete cluster --name devops-cluster
]

---

## Recreate
[
kind create cluster --name devops-cluster
]

---

## Verify
[
kubectl get nodes
]

---

## Useful Commands
[
kubectl config current-context
kubectl config get-contexts
kubectl config view
]

---

## 🧠 kubeconfig Explanation

- Stores cluster access details
- Includes:
  - Clusters
  - Users
  - Contexts

### 📍 Location
```

~/.kube/config

```

---

# 📘 Documentation (For GitHub Repo)

## Kubernetes History

Kubernetes is an orchestration platform designed to manage containerized applications at scale. It was developed by Google based on Borg. It automates deployment, scaling, and self-healing. Kubernetes means "helmsman", symbolizing control over container workloads.

---

## Architecture Summary

- Control plane manages decisions
- Worker nodes execute workloads
- Components run as pods internally

---

## Tool Used

```

Kind (Kubernetes in Docker)

```

---

## kube-system Pods Explanation

- kube-apiserver → API entry point
- etcd → Stores cluster state
- scheduler → Assigns pods
- controller-manager → Maintains desired state
- kube-proxy → Networking
- coredns → DNS resolution

---

# 🎯 Final Outcome

✅ Local Kubernetes cluster created  
✅ Architecture understood  
✅ kubectl commands practiced  
✅ Control plane observed as pods  

---

# 🚀 LinkedIn Post

Started my Kubernetes journey today 🚀  
Set up a local cluster, explored architecture, and saw control plane components running as pods.

The orchestration chapter begins.

#90DaysOfDevOps #DevOpsKaJosh #TrainWithShubham

---

# 💡 Mentor Tip

> Don’t memorize Kubernetes.  
> Understand **how components interact** — that’s what interviews test.

---

🔥 You’ve officially entered **real DevOps engineering**.
```
