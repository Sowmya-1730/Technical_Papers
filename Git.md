# 1. Introduction to Git

## What is Git?

Git is a distributed version control system used to track changes in source code and files during software development. It helps developers collaborate, manage versions, and maintain project history.

Git was created by Linus Torvalds in 2005 for Linux kernel development.

## Why Git is Used

* Tracks file changes over time
* Allows multiple developers to work together
* Maintains project history
* Helps recover older versions
* Supports branching and merging
* Makes collaboration easier


## Version Control System (VCS)

A Version Control System is a software tool that helps developers manage changes to source code over time.

### Types of Version Control Systems

#### 1. Centralized Version Control System (CVCS)

* Uses a central server
* Developers depend on server access
* Example: SVN

#### 2. Distributed Version Control System (DVCS)

* Every user has a complete copy of the repository
* Faster and more reliable
* Example: Git


## Git vs GitHub

| Git                  | GitHub                  |
| -------------------- | ----------------------- |
| Version control tool | Cloud hosting platform  |
| Works locally        | Works online            |
| Tracks changes       | Stores repositories     |
| Command-line based   | Web-based collaboration |


---

# 2. Installing Git

## Install Git on Linux

```bash
sudo apt update
sudo apt install git
```

## Install Git on Windows

1. Download Git from Git official website
2. Run the installer
3. Complete installation wizard

## Install Git on macOS

```bash
brew install git
```

## Verify Installation

```bash
git --version
```

---

# 3. Git Configuration

Git configuration stores username and email information.

## Configure Username

```bash
git config --global user.name "Sowmya"
```

## Configure Email

```bash
git config --global user.email "sowmya.sri.37.2@mountblue.tech"
```

or

``` bash
nano ~/.gitconfig
```
## Check Configuration

```bash
git config --list
```

## Types of Git Configuration

| Type   | Scope              |
| ------ | ------------------ |
| System | Entire computer    |
| Global | Current user       |
| Local  | Current repository |

---

# 4. Creating a Repository

## What is a Repository?

A repository (repo) is a storage location where Git tracks files and changes.



## Initialize a New Repository

```bash
git init
```

This command creates a hidden `.git` folder.



## Clone an Existing Repository

```bash
git clone <repository-url>
```

Example:

```bash
git clone https://github.com/user/project.git
```

---

# 5. Git File Lifecycle

## Stages in Git Lifecycle

### 1. Untracked

Git does not track the file.

### 2. Tracked

Git tracks the file.

### 3. Modified

File has changes.

### 4. Staged

Changes are ready to commit.

### 5. Committed

Changes are permanently saved.

## Git Workflow

Working Directory → Staging Area(git add) → Commit area (git commit) → git push → Make a pull request
## Github Workflow

Write Code → Commit changes → Pull request

---

# 6. Basic Git Commands

## Check Repository Status

```bash
git status
```

Shows:

* Modified files
* Untracked files
* Staged files



## Add Files to Staging Area

### Add Single File

```bash
git add filename
```

### Add All Files

```bash
git add .
```

## Commit Changes

```bash
git commit -m "Initial commit"
```


## View Commit History

```bash
git log
```

### Compact History

```bash
git log --oneline
```

### List out commits done by user in single line
```bash
git shortlog
```

---

# 7. Staging Area

## What is Staging Area?

The staging area is an intermediate area where changes are prepared before committing.


## Why Staging Area is Important

* Helps organize commits
* Allows selective commits
* Prevents unwanted changes from being committed



## Difference Between Add and Commit

| git add                       | git commit                |
| ----------------------------- | ------------------------- |
| Moves changes to staging area | Saves changes permanently |
| Temporary                     | Permanent snapshot        |

---

# 8. Viewing Changes

## View Unstaged Changes

```bash
git diff
```

## View Staged Changes

```bash
git diff --staged
```

---

# 9. Git Ignore

## What is .gitignore?

`.gitignore` prevents unnecessary files from being tracked.


## Example

```gitignore
node_modules/
*.log
.env
__pycache__/
```

---

# 10. Branching in Git

## What is a Branch?

A branch is an independent line of development.


## Why Branches are Used

* Separate features
* Avoid affecting main code
* Easier testing
* Better collaboration


## Create Branch

```bash
git branch branch-name
```


## List Branches

```bash
git branch
```


## Switch Branch

```bash
git checkout branch-name
```

or

```bash
git switch branch-name
```


## Create and Switch Together

```bash
git checkout -b new-branch
```

or 

```bash
git switch -c new-branch
```

## Delete Branch

```bash
git branch -d branch-name
```

## See difference in branches
```bash
git diff branch1 branch2
```

## Rename a HEAD branch
```bash
git branch -m <new_name>
```

## Rename a Non-HEAD branch
```bash
git branch -m <old_name> <new_name>
```

## To see current repository in visual format (By third-part software)
```bash
gittower .
```

## Rename Remote branch
First, delete that branch
```bash
git push origin --delete <old_name>
```
Now, simply push the new branch
```bash
git push -u origin <new_name>
```

## Tracking
First way, to track is by giving destination for the track files
```bash
git branch --track feature/login<to where> origin/feature/login <from where>
```
Another way is by using checkout command by not saying to where we need to track those files
```bash
git checkout --track origin/feature/login
```

## To view summary of what need to be done and what was done
```bash
git branch -v
```

## Move branch forcefully to three previous commits back
```bash
git branch -f master HEAD~3
```

---


# 11. Merging

## What is Merging?

Merging combines changes from one branch into another branch.


## Merge Syntax

```bash
git merge branch-name
```

## Merging a branch to master
```bash
git checkout master
git merge <branch_name>
```

## Types of Merge

### 1. Fast Forward Merge

Occurs when there is a straight path between branches.

### 2. Three-Way Merge

Occurs when branches diverge.


## Merge Conflict

A merge conflict happens when Git cannot automatically decide which changes to keep.

## Resolving Merge Conflicts

1. Open conflicted file
2. Remove conflict markers
3. Keep required code
4. Save file
5. Add file
6. Commit changes

---

## Conflict Markers Example

```text
<<<<<<< HEAD
Current branch code
=======
Incoming branch code
>>>>>>> feature
```

---

# 12. Rebasing

## What is Rebase?

Rebasing moves commits from one branch onto another base branch.


## Rebase Syntax

```bash
git rebase branch-name
```


## Merge vs Rebase

| Merge             | Rebase                 |
| ----------------- | ---------------------- |
| Preserves history | Creates linear history |
| Adds merge commit | No merge commit        |
| Easier for teams  | Cleaner history        |


## Interactive Rebase

```bash
git rebase -i HEAD~3
```

Used for:

* Squashing commits
* Editing commit messages
* Reordering commits


## Rebase Conflict Resolution

```bash
git rebase --continue
```

Abort rebase:

```bash
git rebase --abort
```

---

# 13. Cherry Picking

## What is Cherry Picking?

Cherry-picking applies a specific commit from one branch to another.


## Syntax

```bash
git cherry-pick <commit-id> <commit-id> ..
```

## Use Cases

* Copy bug fixes
* Apply selected features
* Transfer important commits

---

# 14. Git Stash

## What is Git Stash?

Git stash temporarily saves uncommitted changes.


## Stash Changes

```bash
git stash
```

## View Stash List

```bash
git stash list
```


## Apply Stash

```bash
git stash apply
```

## Pop Stash

```bash
git stash pop
```


## Delete Stash

```bash
git stash drop
```

---

# 15. Undoing Changes

## Restore File

```bash
git restore filename
```

## Unstage File

```bash
git restore --staged filename
```

## Reset Commits

### Soft Reset

```bash
git reset --soft HEAD~1
```

Keeps staging area changes.


### Mixed Reset

```bash
git reset --mixed HEAD~1
```

Removes staging changes.


### Hard Reset

```bash
git reset --hard HEAD~1
```

Deletes all changes permanently.

---

# 16. Reverting Changes

## What is Revert?

Revert creates a new commit that undoes previous changes.


## Syntax

```bash
git revert commit-id
```


## Reset vs Revert

| Reset                     | Revert            |
| ------------------------- | ----------------- |
| Removes history           | Preserves history |
| Dangerous in shared repos | Safe for teams    |

---

# 17. Remote Repositories

## Add Remote Repository

```bash
git remote add origin <url>
```

## View Remote Repository

```bash
git remote -v
```


## Push Changes

```bash
git push -u origin master
```

## Pull Changes

```bash
git pull origin main
```

## Fetch Changes

```bash
git fetch
```


## Pull vs Fetch

| Pull                      | Fetch                 |
| ------------------------- | --------------------- |
| Downloads and merges      | Only downloads        |
| Changes working directory | Does not change files |

---

# 18. GitHub Basics

## What is GitHub?

GitHub is a cloud-based platform for hosting Git repositories.

---

## Features of GitHub

* Repository hosting
* Collaboration
* Pull requests
* Issue tracking
* Actions and CI/CD

---

## HTTPS vs SSH

| HTTPS                        | SSH           |
| ---------------------------- | ------------- |
| Uses username/password/token | Uses SSH keys |
| Easier setup                 | More secure   |

---

# 19. Forking

## What is Forking?

Forking creates a personal copy of another user's repository.


## Fork vs Clone

| Fork             | Clone       |
| ---------------- | ----------- |
| Server-side copy | Local copy  |
| GitHub feature   | Git command |


## Fork Workflow

1. Fork repository
2. Clone repository
3. Create branch
4. Make changes
5. Commit changes
6. Push changes
7. Create Pull Request

## How to create SSH key
```bash
ssh-keygen -t rsa -b 4096 -c "<Github email>"
filename : testkey <will ask for file name>
Now how to see that file
ls | grep testkey <will contains two files in it one is for public key with .pb extension and another is private key>
```

---

# 20. Pull Requests

## What is a Pull Request?

A Pull Request (PR) requests merging changes into another branch.

## Benefits of Pull Requests

* Code review
* Team discussion
* Quality improvement
* Collaboration

---

# 21. Collaboration Workflows

## Feature Branch Workflow

Each feature is developed in a separate branch.

## Gitflow Workflow

Uses:

* main branch
* develop branch
* feature branches
* release branches
* hotfix branches


## Trunk-Based Development

Developers frequently merge small changes into main branch.

---

# 22. Tags

## What are Tags?

Tags mark important points in project history.

## Create Tag

```bash
git tag v1.0
```


## View Tags

```bash
git tag
```


## Push Tag

```bash
git push origin v1.0
```

---

# 23. Git Aliases

## What are Aliases?

Aliases create shortcuts for Git commands.


## Example

```bash
git config --global alias.st status
```

Usage:

```bash
git st
```

---

# 24. Git Internals

## HEAD

HEAD points to the current branch or commit.


## Detached HEAD

Occurs when HEAD points directly to a commit instead of a branch.


## Git Objects

### Blob

Stores file data.

### Tree

Stores directory structure.

### Commit

Stores metadata and snapshots.


## SHA Hash

Git identifies objects using SHA hashes.

Example:

```text
4f5a8c9d7e6f2a1b
```

---

# 25. Git Hooks

## What are Git Hooks?

Hooks are scripts triggered automatically before or after Git events.


## Types of Hooks

### Pre-commit Hook

Runs before commit.

### Post-commit Hook

Runs after commit.

### Pre-push Hook

Runs before push.

## Uses of Hooks

* Code formatting
* Testing
* Security checks
* Automation

---

# 26. Git Best Practices

* Write meaningful commit messages
* Commit frequently
* Pull before pushing
* Use branches for features
* Avoid pushing directly to main
* Keep commits small
* Review code before merging

---

# 27. Common Git Errors

## Merge Conflict

Occurs during merge when same lines are modified.

## Detached HEAD Error

Occurs when checking out a commit directly.

Fix:

```bash
git switch branch-name
```


## Failed Push

Occurs when remote has newer changes.

Fix:

```bash
git pull origin main
```

Then push again.

## Authentication Error

Occurs because of invalid credentials or tokens.
