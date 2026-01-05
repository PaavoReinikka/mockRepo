# Git Basics

A comprehensive guide to fundamental Git operations and workflows.

## Table of Contents
1. [What is Git?](#what-is-git)
2. [Configuration](#configuration)
3. [Creating a Repository](#creating-a-repository)
4. [Basic Workflow](#basic-workflow)
5. [Viewing Changes](#viewing-changes)
6. [Branching and Merging](#branching-and-merging)
7. [Remote Repositories](#remote-repositories)
8. [Practical Examples](#practical-examples)

---

## What is Git?

Git is a distributed version control system that tracks changes in your code over time. It allows multiple developers to collaborate on projects, maintain history, and manage different versions of code.

**Key Concepts:**
- **Repository (repo)**: A project tracked by Git
- **Commit**: A snapshot of your code at a specific point in time
- **Branch**: An independent line of development
- **Remote**: A version of your repository hosted elsewhere (e.g., GitHub)

---

## Configuration

Before using Git, configure your identity:

```bash
# Set your name
git config --global user.name "Your Name"

# Set your email
git config --global user.email "your.email@example.com"

# View all configuration
git config --list

# View a specific setting
git config user.name
```

---

## Creating a Repository

### Initialize a New Repository

```bash
# Create a new directory
mkdir my-project
cd my-project

# Initialize Git
git init
```

### Clone an Existing Repository

```bash
# Clone a remote repository
git clone https://github.com/username/repo-name.git

# Clone into a specific directory
git clone https://github.com/username/repo-name.git my-folder
```

---

## Basic Workflow

The typical Git workflow involves three main areas:
1. **Working Directory**: Where you modify files
2. **Staging Area (Index)**: Where you prepare changes for commit
3. **Repository**: Where commits are stored

### Check Status

```bash
# See which files have changed
git status

# Short status format
git status -s
```

### Adding Files

```bash
# Add a specific file
git add filename.txt

# Add multiple files
git add file1.txt file2.txt

# Add all files in current directory
git add .

# Add all files in the repository
git add -A
```

### Committing Changes

```bash
# Commit with a message
git commit -m "Add new feature"

# Add and commit in one step (only for tracked files)
git commit -am "Update existing files"

# Open editor for detailed commit message
git commit
```

### Removing Files

```bash
# Remove file from Git and filesystem
git rm filename.txt

# Remove from Git but keep in filesystem
git rm --cached filename.txt
```

---

## Viewing Changes

### View Commit History

```bash
# View commit log
git log

# Compact one-line format
git log --oneline

# Show last 5 commits
git log -5

# View graphical branch structure
git log --graph --oneline --all

# View changes in each commit
git log -p
```

### View Differences

```bash
# See unstaged changes
git diff

# See staged changes
git diff --staged

# Compare two commits
git diff commit1 commit2

# Compare two branches
git diff branch1 branch2
```

---

## Branching and Merging

Branches allow you to work on features independently without affecting the main codebase.

### Working with Branches

```bash
# List all branches
git branch

# Create a new branch
git branch feature-branch

# Switch to a branch
git checkout feature-branch

# Create and switch to a new branch
git checkout -b feature-branch

# Modern alternative (Git 2.23+)
git switch feature-branch
git switch -c new-feature
```

### Merging Branches

```bash
# Switch to the branch you want to merge INTO
git checkout main

# Merge another branch into current branch
git merge feature-branch
```

**Merge without conflicts example:**
```bash
# Create and switch to new branch
git checkout -b add-readme

# Make changes and commit
echo "# My Project" > README.md
git add README.md
git commit -m "Add README"

# Switch back to main
git checkout main

# Merge the changes (no conflicts if main hasn't changed)
git merge add-readme
```

### Deleting Branches

```bash
# Delete a merged branch
git branch -d feature-branch

# Force delete an unmerged branch
git branch -D feature-branch
```

---

## Remote Repositories

### Managing Remotes

```bash
# View remote repositories
git remote -v

# Add a remote repository
git remote add origin https://github.com/username/repo.git

# Change remote URL
git remote set-url origin https://github.com/username/new-repo.git

# Remove a remote
git remote remove origin
```

### Pushing Changes

```bash
# Push to remote repository
git push origin main

# Push and set upstream branch
git push -u origin main

# Push all branches
git push --all origin
```

### Pulling Changes

```bash
# Fetch and merge changes from remote
git pull origin main

# Fetch without merging
git fetch origin

# Pull with rebase instead of merge
git pull --rebase origin main
```

---

## Practical Examples

### Example 1: Starting a New Project

```bash
# Create project directory
mkdir my-website
cd my-website

# Initialize Git repository
git init

# Create initial files
echo "<!DOCTYPE html>" > index.html
echo "body { margin: 0; }" > style.css

# Stage all files
git add .

# First commit
git commit -m "Initial commit: Add index.html and style.css"

# Add remote repository
git remote add origin https://github.com/yourusername/my-website.git

# Push to GitHub
git push -u origin main
```

### Example 2: Feature Branch Workflow

```bash
# Start on main branch
git checkout main

# Create feature branch
git checkout -b add-contact-form

# Make changes
echo "<form>Contact Form</form>" >> contact.html
git add contact.html
git commit -m "Add contact form"

# Switch back to main
git checkout main

# Merge feature branch (no conflicts)
git merge add-contact-form

# Delete feature branch
git branch -d add-contact-form

# Push to remote
git push origin main
```

### Example 3: Collaborating on a Project

```bash
# Clone a repository
git clone https://github.com/teamrepo/project.git
cd project

# Create a feature branch
git checkout -b update-docs

# Make changes
echo "## Installation" >> README.md
git add README.md
git commit -m "Update documentation with installation steps"

# Push your branch to remote
git push -u origin update-docs

# After code review, merge on GitHub or locally:
git checkout main
git pull origin main
git merge update-docs
git push origin main
```

### Example 4: Checking Out Someone Else's Branch

```bash
# Fetch all remote branches
git fetch origin

# List all branches including remote
git branch -a

# Check out a remote branch
git checkout -b feature-x origin/feature-x

# Or use tracking branch (Git 2.23+)
git checkout --track origin/feature-x
```

### Example 5: Undoing Changes

```bash
# Discard changes in working directory
git checkout -- filename.txt

# Unstage a file (keep changes)
git reset HEAD filename.txt

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Create a new commit that undoes previous commit
git revert HEAD
```

---

## Common Git Commands Cheat Sheet

| Command | Description |
|---------|-------------|
| `git init` | Initialize a new repository |
| `git clone <url>` | Clone a remote repository |
| `git status` | Check status of working directory |
| `git add <file>` | Stage file for commit |
| `git commit -m "msg"` | Commit staged changes |
| `git push` | Upload commits to remote |
| `git pull` | Download and merge remote changes |
| `git branch` | List branches |
| `git checkout <branch>` | Switch to a branch |
| `git merge <branch>` | Merge branch into current branch |
| `git log` | View commit history |
| `git diff` | Show changes between commits |

---

## Best Practices

1. **Commit Often**: Make small, logical commits with clear messages
2. **Write Good Commit Messages**: Be descriptive and use present tense
3. **Pull Before Push**: Always pull latest changes before pushing
4. **Use Branches**: Keep main branch stable, develop in feature branches
5. **Review Before Commit**: Use `git status` and `git diff` to review changes
6. **Don't Commit Sensitive Data**: Use `.gitignore` for passwords, API keys, etc.

---

## Additional Resources

- [Official Git Documentation](https://git-scm.com/doc)
- [GitHub Guides](https://guides.github.com/)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)
- [Pro Git Book (Free)](https://git-scm.com/book/en/v2)
