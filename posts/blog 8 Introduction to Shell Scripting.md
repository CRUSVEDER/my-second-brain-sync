---
title: 8. Introduction to Shell Scripting
date: 2024-12-06
draft: 
Toc: true
tags:
  - basic
---


---

# Introduction to Shell Scripting: Automating Daily Tasks (Bash and PowerShell Edition)

Alright, imagine this: you wake up, fire up your computer, and instead of wasting time organizing files or backing up data, you just hit a button, and boom—your computer does all that boring stuff for you. That’s the magic of shell scripting. It’s not just for Linux nerds; even Windows folks can automate tasks like a pro using PowerShell.

Let’s break this down step-by-step, keeping things chill and beginner-friendly. We'll cover **Bash** for Linux/macOS and **PowerShell** for Windows. No rocket science, just automation magic.

---

### Part 1: What’s a Shell Script?

A shell script is a set of instructions you write in a text file, and the computer runs them, just like how a playlist makes Spotify play the songs you want.

For **Linux/macOS**, we use **Bash** (Bourne Again Shell). For **Windows**, we have **PowerShell**. Both are built-in tools that make automation super easy once you know the basics.

---

### Part 2: Getting Started with Bash (Linux/macOS)

#### Step 1: Open the Terminal

Hit `CTRL+ALT+T` (Linux) or search for **Terminal** (macOS).

#### Step 2: Create Your First Script

In your terminal, type:

```bash
nano hello.sh
```

This opens a text editor. Inside, write:

```bash
#!/bin/bash
echo "Hello from Bash!"
```

#### Step 3: Save and Exit

Press `CTRL+O` to save, `ENTER` to confirm, then `CTRL+X` to exit.

#### Step 4: Make It Executable

Run this to give your script permission to run:

```bash
chmod +x hello.sh
```

#### Step 5: Execute the Script

Run your script by typing:

```bash
./hello.sh
```

You should see:

```
Hello from Bash!
```

---

### Part 3: Getting Started with PowerShell (Windows)

#### Step 1: Open PowerShell

Search for **PowerShell** in the Start menu and open it.

#### Step 2: Create Your First Script

Open Notepad (yes, Notepad), and type:

```powershell
Write-Output "Hello from PowerShell!"
```

#### Step 3: Save as a `.ps1` File

Go to **File > Save As**, name it `hello.ps1`, and choose "All Files" in the save dialog. Make sure it ends with `.ps1`, like this:

```
hello.ps1
```

#### Step 4: Run the Script

Back in PowerShell, navigate to where you saved the file (use `cd` to change directories). Then, run:

```powershell
./hello.ps1
```

You should see:

```
Hello from PowerShell!
```

---

### Part 4: Real-Life Automation with Shell Scripts

Now that you know the basics, let’s tackle some useful scripts.

#### **1. Organize Files**

**Bash (Linux/macOS):**

```bash
#!/bin/bash
mkdir -p Pictures
mv *.jpg Pictures/
echo "JPG files moved to Pictures!"
```

**PowerShell (Windows):**

```powershell
New-Item -ItemType Directory -Path . -Name "Pictures"
Move-Item *.jpg Pictures/
Write-Output "JPG files moved to Pictures!"
```

#### **2. Automate Backups**

**Bash (Linux/macOS):**

```bash
#!/bin/bash
rsync -av ~/Documents ~/Backup
echo "Backup complete!"
```

**PowerShell (Windows):**

```powershell
Copy-Item -Path C:\Users\YourName\Documents -Destination D:\Backup -Recurse
Write-Output "Backup complete!"
```

#### **3. Monitor System Performance**

**Bash (Linux/macOS):**

```bash
#!/bin/bash
while true; do
  echo "$(date): $(top -b -n1 | head -5)" >> system.log
  sleep 3600
done
```

**PowerShell (Windows):**

```powershell
while ($true) {
  Get-Date | Out-File -Append -FilePath system.log
  Get-Process | Sort-Object CPU -Descending | Select-Object -First 5 | Out-File -Append -FilePath system.log
  Start-Sleep -Seconds 3600
}
```

---

### Part 5: Scheduling Scripts

#### **On Linux/macOS:**

Use **crontab** to run scripts at specific times:

1. Open crontab:
    
    ```bash
    crontab -e
    ```
    
2. Add a line to run your script every day at 8 AM:
    
    ```bash
    0 8 * * * /path/to/your/script.sh
    ```
    

#### **On Windows:**

Use **Task Scheduler**:

1. Open Task Scheduler (search for it in Start).
2. Create a new task.
3. Set a trigger (e.g., daily at 8 AM).
4. Set an action to run your `.ps1` script using PowerShell.

---

### Part 6: Tips for Success

1. **Test Small:** Start with tiny scripts and gradually add more features.
2. **Use Comments:** Add `#` in Bash or `#` in PowerShell to explain what each part does.
3. **Handle Errors:** Check if files exist before moving them to avoid errors.
4. **Experiment:** Don’t be afraid to break things (in a safe environment).

---

### Wrapping Up

Whether you’re using Bash or PowerShell, shell scripting is your ticket to automating the boring stuff. It saves time, reduces errors, and makes you look like a tech wizard to your friends.

Start small, stay curious, and soon you’ll be automating tasks you never thought possible. Now, go script something awesome!

[Crusveder]


---