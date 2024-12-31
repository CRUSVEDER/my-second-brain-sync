
# Git Workflow and Commands Explained

## Introduction
Git is a **distributed version control system** designed for collaborative work and efficient version tracking. This guide covers the essential Git commands and workflows, from basic setup to advanced branching.

---

## Interfaces
- **Command Line**: Fastest and most inclusive.
- **GUI Options**:
  - **GitKraken**: Free for open-source projects.
  - **Sourcetree**: Free for Windows and macOS.

---

## Initial Setup

### Check Git Version
```bash
git --version
````

### Git Bash

Emulates a Linux environment for running Git commands on Windows.

### Git Configuration Levels

1. **System**: Applies to all users on the computer.
2. **Global**: Applies to all repositories of the current user.
3. **Local**: Applies only to the current repository.

Set user details globally:

```bash
git config --global user.name "Nate Argaw"
git config --global user.email nateargaw@gmail.com
```

> No quotes are needed if no spaces exist in the name or email.

Edit global configuration:

```bash
git config --global -e
```

### Line Ending Compatibility

Set line-ending conversion for different operating systems:

- **Windows**: `\r\n`
- **Linux/macOS**: `\n`

```bash
git config --global core.autocrlf true    # For Windows
git config --global core.autocrlf input   # For Linux/macOS
```

---

## Basic Commands

### Initialize Repository

```bash
mkdir Jelly
cd Jelly
git init
ls -a  # Shows hidden .git folder
```

### Staging and Committing

1. **Staging Area**: Prepares snapshots for recording.
2. **Commit**: Saves the snapshot.

Example:

```bash
echo hello > file1.js
echo hello2 > file2.js
git status  # Check repository status
git add .   # Stage all files
git commit  # Save snapshot
```

### Commit Message Etiquette

- Keep commits meaningful and specific.
- Use present or past tense (e.g., "Add feature" or "Added feature").

---

## File Management

### Remove Files

```bash
rm file1.js
git add file1.js
git commit -m "Remove unused code"
# Alternatively:
git rm file1.js
```

### Rename Files

```bash
mv file2.js hello.js
git add file2.js hello.js
git commit -m "Rename file"
# Alternatively:
git mv file2.js hello.js
```

---

## Ignoring Files

Create a `.gitignore` file to specify files or directories for Git to ignore:

```bash
logs/      # Ignore all files in logs/
*.log      # Ignore all .log files
main.log   # Ignore a specific file
```

For previously committed files:

```bash
git rm --cached -r bin/  # Remove from staging area
echo "bin/" >> .gitignore
git add .gitignore
git commit -m "Add bin to .gitignore"
```

---

## Viewing History

```bash
git log               # Full history
git log --oneline     # Concise format
git log --reverse     # Oldest to newest
git log --all --graph # Visualize branch history
```

---

## Unstaging and Discarding Changes

```bash
git restore --staged file.js  # Unstage changes
git restore .                 # Discard all local changes (except untracked)
git clean -fd                 # Remove untracked files
```

---

## Branching and Merging

### Create and Switch Branches

```bash
git branch feature1       # Create a branch
git checkout feature1     # Switch to the branch
git checkout master       # Switch back to master
```

### Merge Branches

```bash
git checkout master
git merge feature1 -m "Merge feature1 into master"
```

### Feature Branch Workflow

1. **Create a branch**:
    
    ```bash
    git branch new-feature
    ```
    
2. **Push to GitHub**:
    
    ```bash
    git remote add origin [link]
    git push origin master       # Push master branch
    git push origin new-feature  # Push feature branch
    ```
    
3. **Pull Request**:
    
    - Create a pull request on GitHub.
    - Add title, description, and submit.
4. **Merge Changes**:
    
    ```bash
    git checkout master
    git pull origin master
    ```
    
5. **Delete Branch**:
    
    ```bash
    git branch -D new-feature
    ```
    

---

## Help Commands

- Detailed help: `git config --help`
- Simple help: `git config -h`
