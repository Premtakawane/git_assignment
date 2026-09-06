# 🚀 Git & GitHub — Step-by-Step Notes

> Learn in this order 👇 Each topic builds on the previous one.

---

## 📦 PART 1: Local Git Basics

### 1️⃣ `git init`
Turns a normal folder into a Git repository. Run once, inside the project folder.

### 2️⃣ `git status`
Shows what's changed — new, modified, or staged files. Run this often; it's your "what's going on?" command. 🔍

### 3️⃣ `git add <file>` or `git add .`
Moves changes into the **staging area** (a waiting room before commit). `.` stages everything at once.

### 4️⃣ `git commit -m "message"`
Saves the staged changes permanently into history, with a message describing what changed. ✅

### 5️⃣ `git commit -am "message"`
Shortcut for add + commit — but **only works on already-tracked files**, not new ones. ⚠️

### 6️⃣ `git diff`
Shows exact line-by-line changes *before* you stage/commit. Good habit: always check diff before committing. 👀

### 7️⃣ `git log --oneline`
Shows commit history in short form — one line per commit.

```
9239145 1st commit
699bddc 2nd commit
4a3de79 3rd commit
```
Each hash is a snapshot you can jump back to. 🕰️

---

## ⏪ PART 2: Undoing Things

### 8️⃣ `git reset --hard <commit-hash>`
Moves history backward and **deletes** everything after that commit. Fast but 🚨 **dangerous** — never use on a branch others share or that's already pushed.

### 9️⃣ `git revert <commit-hash>`
Safely undoes a commit by creating a **new commit** that reverses it. Nothing deleted — history stays clean and traceable. 🛡️

**Reset vs Revert:**
```
🔴 RESET --hard          🟢 REVERT
   |                        |
[C3] deleted           [C3] stays
[C2] <-- HEAD          [C2]
[C1]                   [C1]
                       [Revert-C3] <-- HEAD ✅
```
> 💡 Use `revert` on shared/pushed branches. Use `reset` only on your own local, unpushed work.

---

## 🌿 PART 3: Branching

### 🔟 `git branch`
Lists all branches; `*` shows which one you're currently on.

### 1️⃣1️⃣ `git checkout -b <branch-name>`
Creates a new branch **and** switches to it — one step. ⚡

### 1️⃣2️⃣ `git checkout <branch-name>`
Switches to an existing branch.

### 1️⃣3️⃣ Branches are isolated 🏝️
A commit made on `feature` doesn't exist on `master` until merged. Each branch has its own separate snapshot.

```
master:    C1───C2───C3
                        ╲
feature:                 C4  🌿 (only here until merged)
```

### 1️⃣4️⃣ `git merge <branch-name>`
Run while standing on the branch you want to merge **into** (usually `master`).

- **Fast-forward merge** 🏃 → happens when master hasn't moved. Git just slides the pointer forward, no extra commit.
- `git merge --squash <branch>` 🎁 → combines all commits from that branch into a single clean commit.

---

## ☁️ PART 4: Remote & GitHub

> 🗣️ **Vocabulary:** what Git calls "remote" = the server copy on GitHub. Your local folder is your working copy.

### 1️⃣5️⃣ `git remote -v`
Shows which remote (GitHub URL) your local repo is connected to. Empty output = not connected yet.

### 1️⃣6️⃣ `git remote add origin <url>`
Connects your local repo to a GitHub repository. Do this once. 🔗

### 1️⃣7️⃣ `git push -u origin master`
Pushes commits to GitHub for the **first time**. `-u` = upstream, so Git remembers this link — after this, just type `git push`. 🚀

### 1️⃣8️⃣ `git clone <url>`
Downloads a full copy of a GitHub repo (with history) to your machine. 📥

### 1️⃣9️⃣ `git pull`
= `fetch` + `merge` combined. Pulls new commits **and** merges them right away.

### 2️⃣0️⃣ `git fetch`
Downloads new commits but does **not** merge — lets you review first.

> 🆚 **Fetch = look, don't touch. Pull = look and apply.**

---

## 🤝 PART 5: Real Collaboration Workflow (Pull Requests)

Most real projects **lock `master`** 🔒 — nobody pushes directly. Correct flow:

1. `git checkout -b feat/something` → create your own branch 🌱
2. Make changes → `git add` → `git commit`
3. First push on a new branch needs upstream:
   ```
   git push --set-upstream origin feat/something
   ```
   (Only needed the very first time — after that, plain `git push` works ✅)
4. On GitHub → **Create Pull Request** → "merge my branch into master" 📝
5. Once approved → merge the PR on GitHub ✅
6. Back in terminal:
   ```
   git checkout master
   git pull
   ```
   Brings the merged code into your local master. 🎉

```
feat/something ──push──▶ GitHub ──PR + merge──▶ master (GitHub)
                                                     │
                                            git pull ▼
                                        local master catches up 🔄
```

---

## 📋 Quick Reference Table

| Goal | Command |
|---|---|
| 🆕 Start tracking a folder | `git init` |
| 👀 See what changed | `git status` |
| 📥 Stage changes | `git add .` |
| 💾 Save a snapshot | `git commit -m "msg"` |
| 🔍 See exact line changes | `git diff` |
| 🕰️ See history | `git log --oneline` |
| 🛡️ Undo (safe, shared branch) | `git revert <hash>` |
| 🚨 Undo (local only, destructive) | `git reset --hard <hash>` |
| 🌿 New branch + switch | `git checkout -b name` |
| 🔀 Merge branch into current | `git merge name` |
| 🔗 Connect to GitHub | `git remote add origin <url>` |
| 🚀 First push | `git push -u origin master` |
| 📤 Push a new branch first time | `git push --set-upstream origin name` |
| 🔄 Get + merge latest from GitHub | `git pull` |
| 👁️ Get latest without merging | `git fetch` |

---

## 🎯 Still To Learn
- **Rebase** — an alternative to merge for a straight-line history. Saving this for a separate, focused session since it's easy to mix up with merge. 📚

---

<div align="center">

Made with 💻 + ☕ while learning Git the hands-on way

</div>
