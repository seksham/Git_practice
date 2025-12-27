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
- Module 4: Undoing Changes (reset, revert, restore) ✅ DONE
- Module 5: Rewriting History (amend, rebase -i, squash) ✅ DONE
- Module 6: Advanced (cherry-pick, stash, reflog, bisect) ✅ DONE
- Module 7: Collaboration Workflows ✅ DONE

REPOSITORY SETUP:
- Path: /Users/sakshambhayana/saksham/Git_practice
- Remote: git@github-seksham:seksham/Git_practice.git
- GitHub Username: seksham
- Uses custom SSH key: ~/.ssh/id_seksham (for seksham account)
- SSH config alias: github-seksham

FILES IN REPO:
- README.md, shopping.txt, fruits.txt, vegetables.txt, snacks.txt
- GIT_MASTERCLASS.md (this file - learning reference)
```

### 🔄 Quick Resume Prompt

Copy this to quickly resume:

```
I'm learning Git with you. Please read the GIT_MASTERCLASS.md file in my workspace
at /Users/sakshambhayana/saksham/Git_practice/ - it contains our progress and
instructions. Continue teaching me from where we left off (Module 7 Complete - Advanced Topics).
Remember to be structured, explain before running commands, use visual diagrams,
and ask me questions to test understanding.
```

---

> **Created:** December 27, 2025
> **Purpose:** Complete Git learning reference with LLM context for continuation
> **Status:** Complete - All Core Modules Done!

---

## 📋 Course Outline

| Module | Topic | Status |
|--------|-------|--------|
| 0 | Git Fundamentals & Remote Concepts | ✅ Complete |
| 1 | Viewing History (log, show, diff, blame) | ✅ Complete |
| 2 | Branching & Switching | ✅ Complete |
| 3 | Merging | ✅ Complete |
| 4 | Undoing Changes (restore, reset, revert) | ✅ Complete |
| 5 | Rewriting History (amend, rebase -i, squash) | ✅ Complete |
| 6 | Advanced (cherry-pick, stash, reflog, bisect) | ✅ Complete |
| 7 | Collaboration (fetch, pull, push, PRs) | ✅ Complete |

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

## 4.1 The Three Areas

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│    WORKING      │     │    STAGING      │     │   REPOSITORY    │
│   DIRECTORY     │────►│     AREA        │────►│    (commits)    │
│                 │ add │    (index)      │commit│                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘
        │                       │                       │
   git restore             git restore            git reset
   (discard edits)         --staged               git revert
```

## 4.2 `git restore` - Discard Uncommitted Changes

```bash
git restore <file>                    # Discard changes in working directory
git restore --staged <file>           # Unstage a file (keep changes)
git restore --source=HEAD~1 <file>    # Restore file from specific commit
```

## 4.3 `git reset` - Move HEAD and Undo Commits

```bash
git reset --soft <commit>    # Undo commit, keep changes STAGED
git reset --mixed <commit>   # Undo commit, keep changes UNSTAGED (default)
git reset --hard <commit>    # Undo commit, DELETE all changes ⚠️
```

### The Three Modes:

| Mode | HEAD | Staging | Working Dir | Use Case |
|------|------|---------|-------------|----------|
| --soft | Moves | Unchanged | Unchanged | Redo commit with same changes |
| --mixed | Moves | Cleared | Unchanged | Edit before recommitting |
| --hard | Moves | Cleared | Cleared | Completely discard changes ⚠️ |

## 4.4 `git revert` - Safe Undo for Shared History

```bash
git revert <commit>           # Create new commit that undoes specified commit
git revert HEAD               # Revert the last commit
git revert --no-edit HEAD     # Revert without opening editor
```

### Reset vs Revert:

| | Reset | Revert |
|---|-------|--------|
| History | Rewrites | Preserves |
| Safe for pushed code | ❌ No | ✅ Yes |
| Use when | Local commits only | Already pushed |

---

# 📘 MODULE 5: REWRITING HISTORY

## 5.1 `git commit --amend` - Fix the Last Commit

```bash
git commit --amend                    # Change message (opens editor)
git commit --amend -m "New message"   # Change message directly
git commit --amend --no-edit          # Add staged changes, keep message
```

⚠️ Only amend commits that haven't been pushed!

## 5.2 `git rebase` - Move Commits to New Base

```bash
git rebase <target-branch>     # Replay current branch onto target
git rebase -i <commit>         # Interactive rebase
git rebase --abort             # Cancel rebase
git rebase --continue          # Continue after resolving conflicts
```

### Rebase vs Merge:

```
MERGE: Preserves branch history (creates merge commit)
    A ── B ── C ── F ── M
               \      /
                D ── E

REBASE: Linear history (no merge commit)
    A ── B ── C ── F ── D' ── E'
```

## 5.3 Interactive Rebase Commands

```bash
git rebase -i <commit>    # Opens editor with commit list
```

| Command | Short | What It Does |
|---------|-------|--------------|
| pick | p | Keep commit as-is |
| reword | r | Keep commit, edit message |
| edit | e | Stop at commit to make changes |
| squash | s | Combine with previous commit (merge messages) |
| fixup | f | Combine with previous (discard this message) |
| drop | d | Delete commit entirely |

### Squash Example:

```
# BEFORE (in editor):
pick abc1234 Add feature
pick def5678 Fix typo
pick ghi9012 Another fix

# CHANGE TO:
pick abc1234 Add feature
squash def5678 Fix typo
squash ghi9012 Another fix

# RESULT: One commit with all changes
```

---

# 📘 MODULE 6: ADVANCED COMMANDS

## 6.1 `git cherry-pick` - Copy Specific Commits

Cherry-pick copies a specific commit from one branch to another.

### When to Use:
- Apply a hotfix from feature branch to master
- Copy specific changes without merging entire branch
- Port commits between long-running branches

### Syntax:

```bash
git cherry-pick <commit-hash>           # Copy one commit
git cherry-pick <hash1> <hash2>         # Copy multiple commits
git cherry-pick A..B                    # Copy range (exclusive of A)
git cherry-pick --no-commit <hash>      # Apply changes without committing
git cherry-pick --abort                 # Cancel in case of conflicts
git cherry-pick --continue              # Continue after resolving conflicts
```

### Visual:

```
BEFORE cherry-pick:
master:    A ── B ── C
                 \
feature:          D ── E ── F (want to copy E to master)

AFTER git cherry-pick E:
master:    A ── B ── C ── E' (copy of E)
                 \
feature:          D ── E ── F
```

---

## 6.2 `git stash` - Save Work-in-Progress

Stash temporarily saves uncommitted changes so you can switch branches.

### Syntax:

```bash
git stash                        # Stash tracked file changes
git stash -u                     # Include untracked files
git stash -a                     # Include ignored files too
git stash save "message"         # Stash with description
git stash push -m "message"      # Modern syntax

git stash list                   # Show all stashes
git stash show                   # Show latest stash changes
git stash show -p                # Show as patch (diff)
git stash show stash@{2}         # Show specific stash

git stash pop                    # Apply latest & remove from stash
git stash apply                  # Apply latest & keep in stash
git stash pop stash@{2}          # Apply specific stash

git stash drop                   # Delete latest stash
git stash drop stash@{2}         # Delete specific stash
git stash clear                  # Delete ALL stashes ⚠️
```

### Workflow:

```
SCENARIO: Working on feature, urgent bug comes in

$ git status
  modified: feature.txt

$ git stash -m "WIP: feature work"
  Saved working directory

$ git switch main
$ # fix bug, commit, push

$ git switch feature-branch
$ git stash pop
  # Your changes are back!
```

---

## 6.3 `git reflog` - Recovery Safety Net

Reflog records every time HEAD changes. It's your "undo history" for Git.

### What it tracks:
- Commits, resets, rebases
- Branch switches
- Cherry-picks, merges
- Any HEAD movement

### Syntax:

```bash
git reflog                       # Show full reflog
git reflog -n 10                 # Last 10 entries
git reflog show master           # Reflog for specific branch
```

### Recovering Lost Commits:

```bash
# SCENARIO: Accidentally ran git reset --hard HEAD~3

$ git reflog
# Find the commit hash BEFORE the reset

$ git reset --hard <hash>
# OR
$ git cherry-pick <hash>
# OR  
$ git branch recovery <hash>
```

### Visual:

```
AFTER git reset --hard HEAD~3:

"Lost" commits:  X ── Y ── Z  (orphaned, but still in reflog!)
                 ↑
Current HEAD: A ── B ── C

RECOVERY:
$ git reflog
abc1234 HEAD@{0}: reset: moving to HEAD~3
xyz9876 HEAD@{1}: commit: Z (this is what we want!)

$ git reset --hard xyz9876
# Commits recovered!
```

### ⚠️ Reflog Limits:
- Entries expire after **90 days** (default)
- Only exists locally (not pushed)
- `git gc` may clean orphaned objects

---

## 6.4 `git bisect` - Binary Search for Bugs

Bisect finds which commit introduced a bug using binary search.

### How it Works:

```
1000 commits to search?
Binary search: log₂(1000) ≈ 10 tests only!

[GOOD] ─── ? ─── ? ─── ? ─── ? ─── [BAD]
                  ↓
            Test middle commit
            Good? Search right half
            Bad?  Search left half
```

### Syntax:

```bash
git bisect start                 # Start session
git bisect bad                   # Mark current as bad
git bisect bad <commit>          # Mark specific commit as bad
git bisect good <commit>         # Mark known good commit

# Git checks out middle commit, test it, then:
git bisect good                  # If this version works
git bisect bad                   # If this version has the bug
git bisect skip                  # Can't test this commit

git bisect reset                 # End session, return to HEAD
git bisect log                   # Show bisect history

# Automated bisect with test script:
git bisect run ./test.sh         # Script returns 0=good, 1=bad
```

### Complete Workflow:

```bash
$ git bisect start
$ git bisect bad HEAD            # Current version has bug
$ git bisect good v1.0           # v1.0 was working

# Git checks out middle commit
Bisecting: 15 revisions left (roughly 4 steps)

$ ./run-tests.sh                 # Test this version
# If broken:
$ git bisect bad
# If working:
$ git bisect good

# Repeat until:
abc1234 is the first bad commit
commit abc1234
Author: ...
    Refactor login module    ← THE CULPRIT!

$ git bisect reset               # Done, back to original HEAD
```

---

# 📘 MODULE 7: COLLABORATION WORKFLOWS

## 7.1 Local vs Remote Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         REMOTE (GitHub)                         │
│         origin/master: [A]───[B]───[C]───[D]                    │
└─────────────────────────────────────────────────────────────────┘
                              ↑↓
                    fetch ↓   ↑ push
                              ↑↓
┌─────────────────────────────────────────────────────────────────┐
│                         LOCAL (Your Machine)                    │
│  origin/master (tracking): [A]───[B]───[C]───[D]                │
│  master (your work):       [A]───[B]───[C]───[D]───[E]───[F]    │
└─────────────────────────────────────────────────────────────────┘
```

## 7.2 Remote Commands

```bash
git remote -v                    # List remotes with URLs
git remote add origin <url>      # Add a remote
git remote add upstream <url>    # Add upstream (for forks)
git remote remove origin         # Remove a remote
git remote set-url origin <url>  # Change remote URL
git remote rename origin new     # Rename a remote
```

## 7.3 `git fetch` - Download Without Merging

Fetch downloads commits but doesn't change your working files. Safe to run anytime!

```bash
git fetch origin                 # Fetch all branches from origin
git fetch origin master          # Fetch specific branch
git fetch --all                  # Fetch from all remotes
git fetch --prune                # Remove deleted remote branches
```

### After Fetch:

```bash
git log master..origin/master    # See what's new on remote
git log origin/master..master    # See what you have locally
git diff master origin/master    # Compare differences
```

## 7.4 `git pull` - Fetch + Merge

```bash
git pull                         # Fetch + merge current branch
git pull origin master           # Pull specific branch
git pull --rebase                # Fetch + rebase (linear history)
git pull --ff-only               # Only if fast-forward possible
```

### Pull vs Pull --rebase:

```
PULL (merge):
Remote:  [A]───[B]───[X]
Local:   [A]───[B]───[Y]
Result:  [A]───[B]───[X]───[M]  ← merge commit
              └───[Y]───┘

PULL --REBASE:
Remote:  [A]───[B]───[X]
Local:   [A]───[B]───[Y]
Result:  [A]───[B]───[X]───[Y']  ← linear, Y rebased
```

## 7.5 `git push` - Upload Commits

```bash
git push                         # Push to upstream
git push origin master           # Push specific branch
git push -u origin feature       # Push + set upstream tracking
git push --all                   # Push all branches
git push --tags                  # Push all tags
```

### Push Rejection:

```
ERROR: Updates were rejected because the remote contains work that you do not have locally.

SOLUTION:
git pull --rebase                # Get remote changes first
git push                         # Now push
```

## 7.6 Force Push ⚠️

```bash
git push --force                 # Overwrite remote history ⚠️
git push --force-with-lease      # Safer: fails if remote changed
git push -f origin feature       # Force push specific branch
```

### ⚠️ Force Push Rules:

```
✅ OK to force push:
   • Your own feature branches (after rebase/amend)
   • Branches ONLY you work on

❌ NEVER force push:
   • main / master
   • develop / staging
   • Any shared branch

💡 After rebase:
   • Your feature branch NEEDS force push
   • That's expected and safe (it's YOUR branch)
```

## 7.7 Fork & Pull Request Workflow

```
┌─────────────────────────────────────────────────────────────────┐
│  FORK & PR WORKFLOW                                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. FORK the original repo (creates YOUR copy on GitHub)        │
│     [Original Repo] ─── Fork ───> [Your Fork]                   │
│      (upstream)                    (origin)                     │
│                                                                 │
│  2. CLONE your fork                                             │
│     git clone git@github.com:YOU/repo.git                       │
│     git remote add upstream <original-repo-url>                 │
│                                                                 │
│  3. Create FEATURE BRANCH                                       │
│     git checkout -b feature-awesome                             │
│                                                                 │
│  4. Make changes, commit, PUSH to YOUR fork                     │
│     git push origin feature-awesome                             │
│                                                                 │
│  5. Create PULL REQUEST on GitHub                               │
│     [Your Fork:feature-awesome] ──PR──> [Original:main]         │
│                                                                 │
│  6. Code review, discussion, more commits if needed             │
│                                                                 │
│  7. Maintainer MERGES your PR 🎉                                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Keep Fork Updated:

```bash
git fetch upstream               # Get upstream changes
git checkout main
git merge upstream/main          # Merge upstream into your main
git push origin main             # Update your fork
```

## 7.8 Force Push After Rebase — PR Impact

When you force push a rebased feature branch:

| Aspect | What Happens |
|--------|--------------|
| PR stays open | Same PR number, updated commits |
| Old commits replaced | [X,Y] → [X',Y'] |
| Review comments | May become "outdated" |
| CI/CD | Re-runs on new commits |
| Teammates on same branch | Must `git fetch && git reset --hard origin/branch` |

### ⚠️ If Teammate Pulls After Your Force Push:

```
DISASTER: They get duplicate commits + conflicts!

SOLUTION for teammate:
git fetch origin
git reset --hard origin/feature-branch
```

**Rule: Communicate before force pushing shared branches!**

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
> **Progress:** ✅ ALL MODULES COMPLETE! (Modules 0-7)

---

# 🏆 TOPICS MASTERED

| Topic | Commands Learned |
|-------|------------------|
| History | `log`, `show`, `diff`, `blame` |
| Branching | `branch`, `switch`, `checkout` |
| Merging | `merge`, conflict resolution |
| Undoing | `restore`, `reset`, `revert` |
| Rewriting | `commit --amend`, `rebase -i` |
| Advanced | `cherry-pick`, `stash`, `reflog`, `bisect` |
| Collaboration | `fetch`, `pull`, `push`, force push, PRs |

---

# 🎓 GIT EXPERTISE LEVEL: ADVANCED ⭐⭐⭐⭐⭐
