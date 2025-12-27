# 🎓 GIT MASTERCLASS - Complete Reference Guide

---

## 🤖 LLM SESSION CONTEXT (For Continuing in New Sessions)

> **IMPORTANT:** Copy this entire section when starting a new chat session to provide context.

### 📋 Session Instructions for LLM

```
You are teaching me (Saksham) Git from basics to advanced level. Here are your instructions:

TEACHING STYLE:
1. Be STRUCTURED - Complete one module fully before moving to next
2. EXPLAIN before EXECUTE - Always explain what a command does before running it
3. Follow this pattern for each command:
   - What it does
   - Syntax & options
   - When to use it
   - Practical example with explanation
4. Use VISUAL diagrams (ASCII art) to explain concepts
5. ASK QUESTIONS periodically to test my understanding
6. Keep UPDATING this markdown file as we progress

WHAT I ALREADY KNOW:
- Basic git workflow (add, commit, push, pull)
- Have some experience but want EXPERT-level knowledge

WHAT I WANT TO LEARN:
- All advanced topics: reset, rebase, amend, restore, revert
- Interactive rebase, squash commits
- Cherry-pick, stash, reflog, bisect
- Branching strategies
- How to visualize git (graphs, log options)
- When to use which command (practical scenarios)

CURRENT PROGRESS:
- Module 0: Remote Concepts ✅ DONE
- Module 1: Viewing History (log, show, diff, blame) ✅ DONE
- Module 2: Branching (branch, checkout, switch, detached HEAD) ✅ DONE
- Module 3: Merging (merge, conflicts) ✅ DONE
- Module 4: Undoing Changes (reset, revert, restore) 🔄 NEXT UP
- Module 5: Rewriting History (amend, rebase -i, squash) ⏳ PENDING
- Module 6: Advanced (cherry-pick, stash, reflog, bisect) ⏳ PENDING
- Module 7: Collaboration Workflows ⏳ PENDING

REPOSITORY SETUP:
- Path: /Users/sakshambhayana/saksham/Git_practice
- Remote: git@github-seksham:seksham/Git_practice.git
- GitHub Username: seksham
- Uses custom SSH key: ~/.ssh/id_seksham (for seksham account)
- SSH config alias: github-seksham

FILES IN REPO:
- README.md (project readme)
- shopping.txt (practice file with items list)
- fruits.txt (practice file)
- vegetables.txt (practice file)
- GIT_MASTERCLASS.md (this file - learning reference)

BRANCHES:
- master (main branch)
- feature-vegetables (merged)
- feature-dairy (merged)

HOW TO CONTINUE:
Say "Let's continue with Git masterclass from Module X" 
or "Continue from where we left off"
```

### 🔄 Quick Resume Prompt

Copy this to quickly resume:

```
I'm learning Git with you. Please read the GIT_MASTERCLASS.md file in my workspace 
at /Users/sakshambhayana/saksham/Git_practice/ - it contains our progress and 
instructions. Continue teaching me from where we left off (Module 4: Undoing Changes). 
Remember to be structured, explain before running commands, use visual diagrams, 
and ask me questions to test understanding.
```

---

> **Created:** December 27, 2025  
> **Purpose:** Complete Git learning reference with LLM context for continuation  
> **Status:** In Progress - Currently at Module 4

---

## 📋 Course Outline

| Module | Topic | Status |
|--------|-------|--------|
| 0 | Git Fundamentals & Remote Concepts | ✅ Complete |
| 1 | Viewing History (log, show, diff, blame) | ✅ Complete |
| 2 | Branching & Switching | ✅ Complete |
| 3 | Merging | ✅ Complete |
| 4 | Undoing Changes (restore, reset, revert) | 🔄 In Progress |
| 5 | Rewriting History (amend, rebase, rebase -i, squash) | ⏳ Pending |
| 6 | Advanced (cherry-pick, stash, reflog, bisect) | ⏳ Pending |
| 7 | Collaboration (fetch, pull, push workflows) | ⏳ Pending |

---

# 📘 MODULE 0: GIT FUNDAMENTALS & REMOTE CONCEPTS

## 0.1 Local vs Remote Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                           YOUR COMPUTER                                  │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │                    LOCAL REPOSITORY                              │    │
│  │                                                                  │    │
│  │   ┌──────────────┐    ┌──────────────┐    ┌──────────────┐      │    │
│  │   │  WORKING     │    │   STAGING    │    │    LOCAL     │      │    │
│  │   │  DIRECTORY   │───►│    AREA      │───►│   COMMITS    │      │    │
│  │   │              │add │   (index)    │commit             │      │    │
│  │   │ Your files   │    │  Ready to    │    │  Saved       │      │    │
│  │   │ you edit     │    │  commit      │    │  snapshots   │      │    │
│  │   └──────────────┘    └──────────────┘    └──────────────┘      │    │
│  │                                                   │              │    │
│  └───────────────────────────────────────────────────│──────────────┘    │
│                                                      │ push               │
└──────────────────────────────────────────────────────│──────────────────┘
                                                       ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                   REMOTE REPOSITORY (GitHub/GitLab)                      │
└─────────────────────────────────────────────────────────────────────────┘
```

## 0.2 Key Terms

| Term | Definition |
|------|------------|
| **Remote** | A bookmark/reference to a repository hosted elsewhere (GitHub) |
| **Origin** | Default name for your main remote repository |
| **Master/Main** | Default primary branch name |
| **origin/master** | Remote-tracking branch (local copy of remote's state) |
| **Upstream** | Default push/pull destination for a branch |
| **HEAD** | Pointer to your current commit/position |

## 0.3 Remote Commands

```bash
# List remotes
git remote -v

# Add a remote
git remote add origin <url>

# Change remote URL
git remote set-url origin <new-url>

# Remove a remote
git remote remove origin

# Push and set upstream (first time)
git push -u origin master

# Push (after upstream is set)
git push
```

## 0.4 SSH Key Setup

```bash
# Generate new SSH key
ssh-keygen -t ed25519 -C "your_email@example.com" -f ~/.ssh/id_keyname

# Test SSH connection
ssh -T git@github.com

# View public key (add this to GitHub)
cat ~/.ssh/id_keyname.pub
```

### SSH Config for Multiple Accounts (~/.ssh/config)

```
# Account 1
Host github.com
    HostName ssh.github.com
    Port 443
    User git
    IdentityFile ~/.ssh/id_rsa

# Account 2 (personal)
Host github-personal
    HostName ssh.github.com
    Port 443
    User git
    IdentityFile ~/.ssh/id_personal
```

**Usage with multiple accounts:**
```bash
# Use default account
git remote set-url origin git@github.com:username/repo.git

# Use personal account (uses Host alias)
git remote set-url origin git@github-personal:username/repo.git
```

---

# 📘 MODULE 1: VIEWING HISTORY

## 1.1 `git log` - View Commit History

### What it does:
Shows the list of commits from newest to oldest.

### Syntax & Options:

```bash
# Basic log (full details)
git log

# One line per commit (most used!)
git log --oneline

# With visual branch graph
git log --oneline --graph --all

# Limit number of commits
git log -n 5
git log -5

# Show file change statistics
git log --stat
git log --oneline --stat

# Show actual changes (patches)
git log -p

# Filter by author
git log --author="seksham"

# Filter by date
git log --since="2025-01-01"
git log --after="2 weeks ago"
git log --until="2025-12-31"

# Filter by file
git log -- filename.txt

# Search commit messages
git log --grep="bug fix"

# Combine options
git log --oneline --author="seksham" --since="2025-01-01" -- src/
```

### Output Explained:

```
4a1fbfd (HEAD -> master, origin/master) Add eggs to shopping list
   │          │              │                    │
   │          │              │                    └── Commit message
   │          │              └── Remote tracking branch
   │          └── Your current position (HEAD) on master branch
   └── Short commit hash (7 characters)
```

---

## 1.2 `git show` - View One Commit in Detail

### What it does:
Shows complete details of a single commit including the actual changes (diff).

### Syntax:

```bash
# Show latest commit
git show

# Show specific commit
git show abc1234

# Show previous commit
git show HEAD~1

# Show commit 3 steps back
git show HEAD~3

# Show only commit message (no diff)
git show --stat abc1234

# Show file content at specific commit
git show HEAD~1:filename.txt
git show abc1234:src/app.js
```

---

## 1.3 `git diff` - Compare Changes

### What it does:
Shows the difference between two states.

### Visual Explanation:

```
┌────────────────┐   git diff    ┌────────────────┐  git diff --staged  ┌──────────────┐
│   WORKING      │ ◄───────────► │    STAGING     │ ◄────────────────► │ LAST COMMIT  │
│   DIRECTORY    │               │     AREA       │                     │   (HEAD)     │
└────────────────┘               └────────────────┘                     └──────────────┘
                  ◄──────────────── git diff HEAD ─────────────────────►
```

### Syntax:

```bash
# Working directory vs Staging area (unstaged changes)
git diff

# Staging area vs Last commit (staged changes, ready to commit)
git diff --staged
git diff --cached    # same as --staged

# Working directory vs Last commit (all uncommitted changes)
git diff HEAD

# Compare two commits
git diff abc1234 def5678

# Compare with previous commit
git diff HEAD~1 HEAD

# Compare two branches
git diff main feature-branch

# Diff for specific file only
git diff -- filename.txt
git diff HEAD~1 HEAD -- src/app.js

# Show only file names that changed
git diff --name-only HEAD~1 HEAD

# Show stats (insertions/deletions)
git diff --stat HEAD~1 HEAD
```

### Reading Diff Output:

```diff
diff --git a/shopping.txt b/shopping.txt
index 94112a5..a5928b3 100644
--- a/shopping.txt          ← Old version (a/)
+++ b/shopping.txt          ← New version (b/)
@@ -2,3 +2,4 @@             ← Line numbers: old file line 2, new file line 2
 This is my shopping list   ← Unchanged (no prefix)
 1. Milk                    ← Unchanged
 2. Bread                   ← Unchanged
+3. Eggs                    ← Added (+ prefix, green)
-Old item                   ← Removed (- prefix, red)
```

---

## 1.4 `git blame` - Who Changed Each Line

### What it does:
Shows who last modified each line of a file and in which commit.

### Syntax:

```bash
# Blame entire file
git blame filename.txt

# Blame specific lines (1 to 10)
git blame -L 1,10 filename.txt

# Blame starting from line 5, next 3 lines
git blame -L 5,+3 filename.txt

# Show email instead of name
git blame -e filename.txt

# Ignore whitespace changes
git blame -w filename.txt
```

### Output Explained:

```
09e34959 (seksham 2025-12-27 12:44:57 +0530 1) This is my shopping list
   │         │         │              │    │         │
   │         │         │              │    │         └── Line content
   │         │         │              │    └── Line number
   │         │         │              └── Timezone
   │         │         └── Date & time
   │         └── Author
   └── Commit hash
```

---

## 1.5 HEAD~n and HEAD^ Reference

### Understanding HEAD:
- `HEAD` = Where you are right now (current commit)

### Tilde `~` = Go back N generations (linear)

```
HEAD~1  or HEAD~   = 1 commit back
HEAD~2             = 2 commits back  
HEAD~3             = 3 commits back
```

### Caret `^` = Select parent (important for merges)

```
For linear history (no merges):
HEAD^   = HEAD~1  (same thing)
HEAD^^  = HEAD~2  (same thing)

For merge commits (2 parents):
HEAD^1  = First parent (branch you were ON)
HEAD^2  = Second parent (branch you merged IN)
```

### Visual:

```
LINEAR HISTORY:
    HEAD~3     HEAD~2     HEAD~1     HEAD
       ↓          ↓          ↓         ↓
       A ──────── B ──────── C ─────── D

MERGE COMMIT:
       E ─── F (feature branch)
      /       \
     A ─ B ─ C ─ M (HEAD) ← Merge commit
                 │
                 ├── M^1 = C (first parent)
                 └── M^2 = F (second parent)
```

---

# 📘 MODULE 2: BRANCHING & SWITCHING

## 2.1 What is a Branch?

A branch is just a **pointer** to a commit. Creating a branch is instant and lightweight.

```
                                    master (pointer)
                                        │
                                        ▼
    A ──── B ──── C ──── D ──── E ──── F
                                        ▲
                                        │
                                    feature (new pointer, same commit)
```

After commits on feature branch:

```
                                    master
                                        │
                                        ▼
    A ──── B ──── C ──── D ──── E ──── F
                                         \
                                          G ──── H
                                                  ▲
                                                  │
                                              feature
```

## 2.2 `git branch` - Manage Branches

```bash
# List local branches (* = current)
git branch

# List all branches (including remote)
git branch -a

# List with last commit info
git branch -v

# List with tracking info
git branch -vv

# Create new branch (stay on current branch)
git branch feature-login

# Create branch from specific commit
git branch feature-login abc1234

# Rename branch
git branch -m old-name new-name

# Delete branch (safe - only if merged)
git branch -d feature-login

# Force delete branch (even if not merged)
git branch -D feature-login

# Set upstream tracking
git branch --set-upstream-to=origin/master master
```

## 2.3 `git switch` - Switch Branches (Modern)

```bash
# Switch to existing branch
git switch feature-login

# Create and switch to new branch
git switch -c new-feature

# Create branch from specific commit and switch
git switch -c new-feature abc1234

# Switch back to previous branch
git switch -

# Discard local changes and switch (force)
git switch -f master
```

## 2.4 `git checkout` - Switch Branches (Classic)

```bash
# Switch to existing branch
git checkout feature-login

# Create and switch to new branch
git checkout -b new-feature

# Switch back to previous branch
git checkout -

# Checkout specific commit (detached HEAD)
git checkout abc1234

# Checkout specific file from another branch
git checkout main -- filename.txt
```

### switch vs checkout

| Feature | `git switch` | `git checkout` |
|---------|--------------|----------------|
| Switch branches | ✅ `switch branch` | ✅ `checkout branch` |
| Create + switch | ✅ `switch -c new` | ✅ `checkout -b new` |
| Checkout files | ❌ | ✅ `checkout -- file` |
| Detached HEAD | ❌ (use `--detach`) | ✅ `checkout abc123` |
| Introduced | Git 2.23 (2019) | Original |
| Recommended | ✅ For branches | For files/commits |

---

# 📘 MODULE 3: MERGING

## 3.1 What is Merging?

Merging combines the changes from one branch into another.

```
BEFORE MERGE:
              feature
                  │
                  ▼
    A ── B ── C ── D
              ▲
              │
           master (HEAD)

AFTER MERGE (git merge feature):
              feature
                  │
                  ▼
    A ── B ── C ── D
              │     \
              │      M (merge commit)
              │     /
              └────┘
                   ▲
                   │
                master (HEAD)
```

## 3.2 Types of Merges

### Fast-Forward Merge
When there are no new commits on the base branch. No merge commit needed.

```
BEFORE:
    A ── B ── C (master)
               \
                D ── E (feature)

AFTER (fast-forward):
    A ── B ── C ── D ── E (master, feature)
```

### 3-Way Merge
When both branches have new commits. Creates a merge commit with 2 parents.

```
BEFORE:
    A ── B ── C ── F (master)
               \
                D ── E (feature)

AFTER:
    A ── B ── C ── F ──── M (master) ← merge commit (2 parents: F and E)
               \        /
                D ── E ─┘ (feature)
```

## 3.3 `git merge` - Combine Branches

```bash
# Basic merge (merge feature into current branch)
git checkout master
git merge feature-branch

# Merge with commit message
git merge feature-branch -m "Merge feature into master"

# No fast-forward (always create merge commit)
git merge --no-ff feature-branch

# Fast-forward only (fail if not possible)
git merge --ff-only feature-branch

# Abort merge in progress
git merge --abort

# Continue after resolving conflicts
git add .
git merge --continue
# or just: git commit
```

## 3.4 Merge Conflicts

Conflicts happen when the same lines are changed in both branches.

### Conflict Markers:

```
<<<<<<< HEAD
Your changes (current branch)
=======
Their changes (branch being merged)
>>>>>>> feature-branch
```

### Resolving Conflicts:

```bash
# 1. See which files have conflicts
git status

# 2. Open conflicted file, you'll see:
<<<<<<< HEAD
5. Yogurt
=======
5. Cheese
>>>>>>> feature-dairy

# 3. Edit to resolve (keep one, both, or write new):
5. Yogurt
6. Cheese

# 4. Stage the resolved file
git add shopping.txt

# 5. Complete the merge
git commit -m "Merge feature-dairy: resolved conflicts"
```

### Resolution Options:

```bash
# Keep your version (current branch)
git checkout --ours filename.txt

# Keep their version (merging branch)  
git checkout --theirs filename.txt

# Use a merge tool
git mergetool
```

---

# 📘 MODULE 4: UNDOING CHANGES
*Coming soon...*

---

# 📘 MODULE 5: REWRITING HISTORY
*Coming soon...*

---

# 📘 MODULE 6: ADVANCED COMMANDS
*Coming soon...*

---

# 📘 MODULE 7: COLLABORATION
*Coming soon...*

---

# 🔧 Quick Reference Cheat Sheet

## Most Used Commands

```bash
# Check status
git status

# Stage changes
git add filename.txt       # Single file
git add .                  # All files
git add -p                 # Interactive staging

# Commit
git commit -m "message"
git commit -am "message"   # Add tracked files + commit

# View history
git log --oneline --graph --all

# Push/Pull
git push
git pull

# Branches
git branch                 # List
git switch -c new-branch   # Create + switch
git switch main            # Switch back
```

## Configuration

```bash
# Set identity
git config user.name "Your Name"
git config user.email "your@email.com"

# Global config
git config --global user.name "Your Name"

# View config
git config --list

# Set default editor
git config --global core.editor "code --wait"

# Set default branch name
git config --global init.defaultBranch main
```

---

# 📝 Practice Commands Log

Commands we ran during this session:

```bash
# Initialize and configure
git init
git config user.name "seksham"
git config user.email "saksham.bhayana@gmail.com"

# Create commits
echo "content" > file.txt
git add file.txt
git commit -m "message"

# Remote setup
git remote add origin git@github-seksham:seksham/Git_practice.git
git push -u origin master

# View history
git log --oneline --graph --all
git show HEAD
git diff --staged
git blame shopping.txt
```

---

> **Last Updated:** December 27, 2025  
> **Progress:** Module 3 (Merging) complete, Module 4 next
