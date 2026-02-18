# Day 24 – Advanced Git: Merge, Rebase, Stash & Cherry Pick

Repository: devops-git-practice  
Folder: 2026/day-24/  
File: day-24-notes.md  

---

# 📘 Topic 1: Git Merge

## 🔹 Notes

Git Merge is used to combine changes from one branch into another.

There are two main types of merges:

1. Fast-Forward Merge
2. Merge Commit

A Fast-Forward merge happens when the target branch has no new commits since the branch was created.

A Merge Commit happens when both branches have progressed separately.

---

## 🛠 Task 1 – Hands-On

### Step 1: Create feature-login branch

[git checkout main]  
[git checkout -b feature-login]

Make changes and commit:

[vim nginx.sh]  
[chmod +x nginx.sh]  
[git add nginx.sh]  
[git commit -m "Add nginx testing script"]

---

### Step 2: Merge into main

[git checkout main]  
[git merge feature-login]

### 🔍 Observation

If no new commits were added to main → Fast-forward merge happened.  
Git simply moved the main pointer forward.

---

### Step 3: Create feature-signup branch

[git checkout -b feature-signup]

Make commits:

[vim signup.txt]  
[git add signup.txt]  
[git commit -m "Add signup feature"]

Now add a commit to main before merging:

[git checkout main]  
[vim main-update.txt]  
[git add main-update.txt]  
[git commit -m "Main updated separately"]

Now merge:

[git merge feature-signup]

### 🔍 Observation

Git created a Merge Commit because both branches had diverged.

---

## ✅ Answers

### What is a fast-forward merge?

A fast-forward merge happens when the target branch has no new commits and Git simply moves the branch pointer forward without creating a new commit.

### When does Git create a merge commit instead?

When both branches have new commits and their histories have diverged.

### What is a merge conflict?

A merge conflict occurs when Git cannot automatically merge changes because the same line in a file was modified in different branches.

To create conflict intentionally:

Edit same line in both branches and then merge.

Resolve conflict manually → then:

[git add file-name]  
[git commit]

---

# 📘 Topic 2: Git Rebase

## 🔹 Notes

Rebase rewrites commit history by moving your branch commits on top of another branch.

Unlike merge, it creates a linear history.

---

## 🛠 Task 2 – Hands-On

Create feature-dashboard:

[git checkout main]  
[git checkout -b feature-dashboard]

Add commits:

[vim dashboard.txt]  
[git add dashboard.txt]  
[git commit -m "Dashboard part 1"]  
[git commit -m "Dashboard part 2"]

Now move main ahead:

[git checkout main]  
[vim hotfix.txt]  
[git add hotfix.txt]  
[git commit -m "Hotfix on main"]

Now rebase:

[git checkout feature-dashboard]  
[git rebase main]

Visualize:

[git log --oneline --graph --all]

---

## ✅ Answers

### What does rebase actually do?

Rebase takes your branch commits and replays them on top of another branch.

### How is history different from merge?

Merge → Non-linear history with merge commits.  
Rebase → Clean, linear history.

### Why should you never rebase shared commits?

Because rebase rewrites commit history and changes commit hashes, which can break collaboration.

### When to use rebase vs merge?

Use rebase:
- For clean history
- Before merging feature branch into main

Use merge:
- When working in shared/public branches

---

# 📘 Topic 3: Squash Commit vs Merge Commit

## 🛠 Task 3 – Hands-On

Create feature-profile:

[git checkout -b feature-profile]

Add multiple small commits:

[git commit -m "Fix typo"]  
[git commit -m "Formatting update"]  
[git commit -m "Refactor code"]  
[git commit -m "Minor improvement"]

Squash merge:

[git checkout main]  
[git merge --squash feature-profile]  
[git commit -m "Add feature-profile (squashed)"]

Check history:

[git log --oneline]

Observation: Only ONE commit added to main.

---

Now regular merge:

[git checkout -b feature-settings]  
[git commit -m "Settings part 1"]  
[git commit -m "Settings part 2"]

Merge normally:

[git checkout main]  
[git merge feature-settings]

Observation: All commits preserved.

---

## ✅ Answers

### What does squash merging do?

Combines all commits from a branch into a single commit before merging.

### When to use squash merge?

When feature branch has many small or messy commits.

### Trade-off of squashing?

You lose detailed commit history of that branch.

---

# 📘 Topic 4: Git Stash

## 🔹 Notes

Git Stash temporarily saves uncommitted changes so you can switch branches safely.

---

## 🛠 Task 4 – Hands-On

Make changes but do not commit:

[vim temp.txt]

Try switching branch:

[git checkout main]

Git blocks switching if changes conflict.

Use stash:

[git stash push -m "WIP changes"]

List stashes:

[git stash list]

Switch branch and return:

[git checkout feature-login]

Apply stash:

[git stash pop]

Apply specific stash:

[git stash apply stash@{1}]

---

## ✅ Answers

### Difference between git stash pop and apply?

git stash pop → Applies and deletes stash  
git stash apply → Applies but keeps stash

### When would you use stash?

- Urgent hotfix
- Context switching
- Pulling latest changes without committing incomplete work

---

# 📘 Topic 5: Cherry Pick

## 🔹 Notes

Cherry-pick allows applying a specific commit from one branch to another.

---

## 🛠 Task 5 – Hands-On

Create feature-hotfix:

[git checkout -b feature-hotfix]

Make 3 commits:

[git commit -m "Hotfix 1"]  
[git commit -m "Hotfix 2"]  
[git commit -m "Hotfix 3"]

Find commit hash:

[git log --oneline]

Switch to main:

[git checkout main]

Cherry-pick second commit:

[git cherry-pick <commit-hash>]

Verify:

[git log --oneline --graph --all]

Observation: Only selected commit applied.

---

## ✅ Answers

### What does cherry-pick do?

It applies a specific commit from one branch onto another branch.

### When to use cherry-pick?

- Production hotfix
- Applying selective bug fixes
- Backporting changes

### What can go wrong?

- Merge conflicts
- Duplicate commits
- History confusion

---

# 📊 Final Observations

Merge → Safe and preserves history  
Rebase → Clean history but rewrites commits  
Squash → Single clean commit  
Stash → Temporary work storage  
Cherry-pick → Selective commit transfer  

---

# 📌 Commands to Add in git-commands.md

[git merge branch-name]  
[git merge --squash branch-name]  
[git rebase branch-name]  
[git stash]  
[git stash push -m "message"]  
[git stash list]  
[git stash pop]  
[git stash apply stash@{n}]  
[git cherry-pick commit-hash]  
[git log --oneline --graph --all]

---

# 🚀 Submission Steps

[git add 2026/day-24/day-24-notes.md]  
[git add git-commands.md]  
[git commit -m "Day 24 - Advanced Git: Merge, Rebase, Stash & Cherry Pick"]  
[git push origin main]

---

✅ Day 24 Completed – Advanced Git concepts mastered.  
DevOps 90 Days Journey Continues 🔥
