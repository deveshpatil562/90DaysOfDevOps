# 🚀 Day 22 – Introduction to Git: Your First Repository

## 📌 Task Overview

Today marks the beginning of my Git journey. Git is the backbone of modern DevOps — every tool, pipeline, and workflow revolves around version control.

Before diving into advanced concepts, I focused on understanding the fundamentals by doing hands-on practice.

---

# 🎯 Objectives

- Understand what Git is and why it matters
- Set up my first Git repository from scratch
- Start building a living document of Git commands

---

# ✅ Expected Output

- A local Git repository with a clean commit history
- A file called `git-commands.md` (to keep updating daily)
- A file called `day-22-notes.md` with my answers

---

# 🔥 Challenge Tasks

---

## 🛠 Task 1: Install and Configure Git

### Verify Git Installation

[git --version]

Example Output:
```
git version 2.47.3
```

### Set Git Identity

[git config --global user.name "Devesh"]

[git config --global user.email "deveshpatil562@gmail.com"]

### Verify Configuration

[git config --list]

Example Output:
```
user.name=Devesh
user.email=deveshpatil562@gmail.com
```

---

## 📁 Task 2: Create Your Git Project

### Create Project Folder

[mkdir devops-git-practice]

[cd devops-git-practice]

### Initialize Git Repository

[git init]

### Check Repository Status

[git status]

### Explore Hidden Git Directory

[ls -la]

[cd .git]

[ls]

📌 The `.git/` folder contains:
- HEAD
- config
- objects/
- refs/
- hooks/
- index

This folder is the heart of Git. It stores the entire version history.

---

## 📚 Task 3: Create Git Commands Reference

### Create Reference File

[touch git-commands.md]

### Add Commands Categorized

---

### 🔹 Setup & Config

| Command | What It Does | Example |
|---------|--------------|----------|
| git --version | Shows installed Git version | [git --version] |
| git config --global user.name | Sets username | [git config --global user.name "Devesh"] |
| git config --global user.email | Sets email | [git config --global user.email "deveshpatil562@gmail.com"] |
| git config --list | Shows config | [git config --list] |

---

### 🔹 Basic Workflow

| Command | What It Does | Example |
|---------|--------------|----------|
| git init | Initializes repo | [git init] |
| git status | Shows working state | [git status] |
| git add | Stages files | [git add git-commands.md] |
| git commit | Saves snapshot | [git commit -m "Initial commit"] |

---

### 🔹 Viewing Changes

| Command | What It Does | Example |
|---------|--------------|----------|
| git log | Shows commit history | [git log] |
| git log --oneline | Compact history | [git log --oneline] |
| git diff | Shows unstaged changes | [git diff] |
| git diff --staged | Shows staged changes | [git diff --staged] |

---

## 💾 Task 4: Stage and Commit

### Stage File

[git add git-commands.md]

### Check Staged Files

[git status]

### Commit with Meaningful Message

[git commit -m "Add initial Git commands reference"]

### View Commit History

[git log]

---

## 🔄 Task 5: Build Commit History

### Edit File and Add More Commands

(Add new commands as discovered)

### Check What Changed

[git diff]

### Stage and Commit Again

[git add git-commands.md]

[git commit -m "Update Git commands with diff examples"]

Repeat at least 3 times to build history.

### View Compact History

[git log --oneline]

📌 Goal: Maintain clean, descriptive commits.

---

## 🧠 Task 6: Understand Git Workflow (day-22-notes.md)

Create file:

[touch day-22-notes.md]

Add answers:

---

### 1️⃣ Difference between git add and git commit?

- `git add` moves changes to the staging area.
- `git commit` saves staged changes permanently in repository history.

---

### 2️⃣ What does the staging area do?

The staging area acts as a preparation zone.  
It allows selective commits instead of committing everything at once.

---

### 3️⃣ What does git log show?

- Commit ID (SHA)
- Author
- Date
- Commit message

---

### 4️⃣ What is the .git/ folder?

The `.git/` folder stores:
- Complete commit history
- Branch information
- Configuration
- Object database

If deleted → Git stops tracking the project completely.

---

### 5️⃣ Difference between Working Directory, Staging Area, Repository?

| Area | Meaning |
|------|---------|
| Working Directory | Where you edit files |
| Staging Area | Where files wait before commit |
| Repository | Where commits are permanently stored |

---

# 🔁 Ongoing Task

- Update `git-commands.md` daily
- One clean commit per update
- Clear commit messages
- Maintain readable history

---

# 💡 Helpful Commands

Use help pages:

[man git]

[git <command> --help]

Example:

[git status --help]

---

# 📤 Submission Checklist

- Screenshot of [git log --oneline] with multiple commits
- Add `day-22-notes.md` to:

[mkdir -p 2026/day-22]

- Commit changes:

[git add .]

[git commit -m "Add Day 22 Git practice files"]

- Push to fork:

[git push origin main]

- Submit for Community Builder of the Week on Discord 🚀

---

# 🏆 Day 22 Summary

Today I:

✔ Installed and configured Git  
✔ Created my first repository  
✔ Built structured Git command documentation  
✔ Created multiple commits  
✔ Understood Git workflow deeply  

This is the foundation of everything in DevOps.

Git mastery begins today. 🚀
