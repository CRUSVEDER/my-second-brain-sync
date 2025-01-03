---
dg-publish:
---

# Git Workflow and Commands Explained

## Introduction
Git is a **distributed version control system** for version tracking and collaboration. This guide covers essential Git commands and workflows, applicable to any project or file.

---

## Interfaces
- **Command Line**: Fastest and most versatile option.
- **GUI Options**:
  - **GitKraken**: Free for open-source projects.
  - **Sourcetree**: Free for Windows and macOS.

---

## Initial Setup

### Check Git Version
Verify the Git installation:
```bash
git --version
````

### Git Bash

Emulates a Linux terminal environment for Windows users, making it easier to use Git commands.

### Git Configuration Levels

1. **System**: Applies to all users on the computer.
2. **Global**: Applies to all repositories of the current user.
3. **Local**: Applies only to the current repository.

Set user details globally:

```bash
git config --global user.name "Your Name"
git config --global user.email your_email@example.com
```

> Quotes are only required if there are spaces in the input.

Edit global configurations:

```bash
git config --global -e
```

### Line Ending Compatibility

Set line-ending conversion for cross-platform compatibility:

- **Windows**: Use `\r\n` (Carriage Return + Line Feed).
- **Linux/macOS**: Use `\n` (Line Feed).

```bash
git config --global core.autocrlf true    # For Windows
git config --global core.autocrlf input   # For Linux/macOS
```

---

## Basic Commands

### Initialize Repository

```bash
mkdir [project_name]
cd [project_name]
git init
ls -a  # Display hidden files (e.g., .git directory)
```

### Staging and Committing Files

1. **Staging Area**: Prepares changes for a snapshot.
2. **Commit**: Saves the snapshot to the repository.

Example:

```bash
echo "Hello World" > file1.txt
git status       # Check current status
git add file1.txt  # Stage file
git commit        # Commit changes
```

### Commit Message Etiquette

- **Be specific**: Separate commits for specific portions of code.
- **Be concise**: Use short, meaningful messages.
- **Tense**: Use present or past tense (e.g., "Add feature" or "Added feature").

---

## File Management

### Remove Files

```bash
rm file1.txt
git add file1.txt
git commit -m "Remove unused file"
# Alternatively:
git rm file1.txt
```

### Rename Files

```bash
mv old_file.txt new_file.txt
git add old_file.txt new_file.txt
git commit -m "Rename file"
# Alternatively:
git mv old_file.txt new_file.txt
```

---

## Ignoring Files

To prevent Git from tracking certain files or directories, create a `.gitignore` file in the project root:

```plaintext
# Example .gitignore rules
logs/         # Ignore all files in the 'logs' directory
*.log         # Ignore all files with a .log extension
config.json   # Ignore specific file
```

For files previously committed:

```bash
git rm --cached -r [file_or_directory]
echo "[file_or_directory]" >> .gitignore
git add .gitignore
git commit -m "Update .gitignore to ignore specific files"
```

---

## Viewing History

```bash
git log               # Full commit history
git log --oneline     # Concise commit history
git log --reverse     # Show commits from oldest to newest
git log --all --graph # Visual representation of branches and commits
```

---

## Unstaging and Discarding Changes

```bash
git restore --staged [file]   # Unstage changes
git restore .                 # Discard all local changes (except untracked files)
git clean -fd                 # Remove untracked files (f: force, d: directories)
```

---

## Branching and Merging

### Create and Switch Branches

```bash
git branch [branch_name]   # Create a branch
git checkout [branch_name] # Switch to the branch
```

### Merge Branches

```bash
git checkout main          # Switch to the main branch
git merge [branch_name] -m "Merge [branch_name] into main"
```

### Feature Branch Workflow

1. **Create a Feature Branch**:
    
    ```bash
    git branch [feature_name]
    ```
    
2. **Push to Remote Repository**:
    
    ```bash
    git remote add origin [repository_url]
    git push origin main          # Push main branch
    git push origin [feature_name] # Push feature branch
    ```
    
3. **Pull Request**:
    
    - Create a pull request on GitHub or your Git hosting platform.
    - Add a title, description, and submit.
4. **Merge Changes**:
    
    ```bash
    git checkout main
    git pull origin main
    ```
    
5. **Delete Feature Branch**:
    
    ```bash
    git branch -D [feature_name]
    ```
    

---

## Help Commands

- Detailed help: `git config --help`
- Simple help: `git config -h`

