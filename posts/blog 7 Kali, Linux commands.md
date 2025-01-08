---
title: 7. Kali, linux Commands
date: 2024-12-05
draft: 
Toc: true
tags:
  - basic
  - tips/tricks
---



---

**Top 60 Linux Commands Cheat Sheet in one line**

---

**A. File and Directory Management Commands**

- `ssh`: Secure Shell, used for secure remote access to a system.
- `ls`: List directory contents.
- `pwd`: Print the current working directory.
- `cd`: Change directory to a different folder.
- `touch`: Create an empty file or update the modified timestamp of an existing file.
- `echo`: Print a message or the value of a variable.
- `nano`: A simple text editor.
- `vim`: A more advanced text editor with many features.
- `cat`: Print the contents of a file to the console.
- `shred`: Securely delete a file by overwriting its contents.
- `mkdir`: Create a new directory.
- `cp`: Copy a file from one location to another.
- `mv`: Move a file from one location to another, or rename a file.
- `rm`: Remove a file.
- `rmdir`: Remove a directory if it is empty.
- `ln`: Create a link to a file or directory.
- `head`: Display the first lines of a file.
- `tail`: Display the last lines of a file.
- `cmp`: Compare two files byte by byte.
- `diff`: Display the differences between two files.
- `sort`: Sort the lines of a file.
- `find`: Search for files in a directory hierarchy.
- `chmod`: Change the permissions of a file or directory.
- `chown`: Change the owner of a file or directory.

---

**B. System Management Commands**

- `clear`: Clear the console.
- `useradd`: Add a new user to the system.
- `sudo`: Run a command with administrative privileges.
- `adduser`: Add a new user to the system with more options than `useradd`.
- `su`: Switch to another user account.
- `exit`: Close the current terminal or log out of the current user account.
- `sudo passwd`: Change the password for the current user.
- `sudo passwd [username]`: Change the password for another user.
- `sudo apt`: A package manager used to install, update, and remove software packages on Debian-based systems.
- `sudo apt update & install`: Update package lists and install packages.
- `finger`: Display information about a user.
- `man`: Display the manual page of a command.
- `whatis`: Display a brief description of a command.
- `which`: Locate a command and display its path.
- `whereis`: Locate the binary, source, and manual page files for a command.
- `wget`: Download files from the web.
- `curl`: Transfer data to or from a server.
- `zip`: Compress files into a zip archive.
- `unzip`: Extract files from a zip archive.
- `less`: View a file one page at a time.

---

**C. File Comparison & Manipulation Commands**

- `ifconfig`: Configure network interfaces.
- `ip address`: Display IP address information.
- `ping`: Test network connectivity by sending packets to a host.
- `resolvectl status`: Display the current DNS resolver configuration.
- `netstat`: Display network connections, routing tables, and interface statistics.
- `iptables`: Configure and administer the netfilter firewall.
- `ufw`: A user-friendly interface to manage iptables firewall rules.

---

**D. Networking Management & Monitoring Commands**

- `uname`: Print system information, including kernel name, network node hostname, kernel release, and kernel version.
- `neofetch`: Display system information in a colorful and visually appealing way.
- `cal`: Display a calendar of the current month or year.
- `free`: Display the amount of free and used system memory.
- `df` and `df -h`: Display disk usage statistics for a file system.
- `ps`: Report a snapshot of current processes.
- `top`: Display dynamic real-time information about running processes.
- `kill`: Send a signal to terminate a process.
- `pkill`: Send a signal to terminate one or more processes based on their name.
- `systemctl`: Control the system and service manager.
- `history`: Display previously executed commands.
- `sudo reboot`: Reboot the system with administrative privileges.
- `shutdown`: Shutdown or reboot the system.

  credits: [NetworkChuck]
---

# Linux Commands Cheat Sheet with Examples :

## 1. **File and Directory Management**

- **`ls`**  
    List files and directories.  
    _Example:_
    
    ```bash
    ls
    ```
    
- **`ls -l`**  
    List files with detailed information.  
    _Example:_
    
    ```bash
    ls -l
    ```
    
- **`mkdir`**  
    Create a new directory.  
    _Example:_
    
    ```bash
    mkdir new_folder
    ```
    
- **`rmdir`**  
    Remove an empty directory.  
    _Example:_
    
    ```bash
    rmdir empty_folder
    ```
    
- **`rm`**  
    Delete files or directories.  
    _Example:_
    
    ```bash
    rm file.txt
    ```
    
- **`cp`**  
    Copy files or directories.  
    _Example:_
    
    ```bash
    cp source.txt destination.txt
    ```
    
- **`mv`**  
    Move or rename files.  
    _Example:_
    
    ```bash
    mv old_name.txt new_name.txt
    ```
    
- **`pwd`**  
    Show the current directory.  
    _Example:_
    
    ```bash
    pwd
    ```
    

## 2. **File Viewing**

- **`cat`**  
    Display file contents.  
    _Example:_
    
    ```bash
    cat file.txt
    ```
    
- **`less`**  
    View file with pagination.  
    _Example:_
    
    ```bash
    less file.txt
    ```
    
- **`head`**  
    Display the first 10 lines of a file.  
    _Example:_
    
    ```bash
    head file.txt
    ```
    
- **`tail`**  
    Display the last 10 lines of a file.  
    _Example:_
    
    ```bash
    tail file.txt
    ```
    
- **`tail -f`**  
    Follow updates to a file (e.g., log file).  
    _Example:_
    
    ```bash
    tail -f log.txt
    ```
    

## 3. **File Permissions and Ownership**

- **`chmod`**  
    Change file permissions.  
    _Example:_
    
    ```bash
    chmod 755 script.sh
    ```
    
- **`chown`**  
    Change file ownership.  
    _Example:_
    
    ```bash
    chown user:group file.txt
    ```
    
- **`ls -l`**  
    View file permissions and ownership.  
    _Example:_
    
    ```bash
    ls -l
    ```
    

## 4. **Searching**

- **`grep`**  
    Search for a pattern in a file.  
    _Example:_
    
    ```bash
    grep "search_term" file.txt
    ```
    
- **`grep -r`**  
    Search recursively in directories.  
    _Example:_
    
    ```bash
    grep -r "search_term" directory/
    ```
    
- **`find`**  
    Locate files by name or criteria.  
    _Example:_
    
    ```bash
    find /path -name "file.txt"
    ```
    
- **`locate`**  
    Search files quickly using a pre-built database.  
    _Example:_
    
    ```bash
    locate file.txt
    ```
    
- **`updatedb`**  
    Update the database for `locate`.  
    _Example:_
    
    ```bash
    sudo updatedb
    ```
    

## 5. **Disk Usage**

- **`df -h`**  
    Show free disk space in human-readable format.  
    _Example:_
    
    ```bash
    df -h
    ```
    
- **`du -h`**  
    Show disk usage of files/directories.  
    _Example:_
    
    ```bash
    du -h directory/
    ```
    

## 6. **Networking**

- **`ip addr`**  
    Display network interfaces and IP addresses.  
    _Example:_
    
    ```bash
    ip addr
    ```
    
- **`ping`**  
    Test connectivity to a host.  
    _Example:_
    
    ```bash
    ping google.com
    ```
    
- **`netstat`**  
    View network connections.  
    _Example:_
    
    ```bash
    netstat -tuln
    ```
    
- **`nslookup`**  
    Query DNS records for a domain.  
    _Example:_
    
    ```bash
    nslookup example.com
    ```
    
- **`traceroute`**  
    Trace the route to a host.  
    _Example:_
    
    ```bash
    traceroute google.com
    ```
    

## 7. **User Management**

- **`adduser`**  
    Add a new user.  
    _Example:_
    
    ```bash
    sudo adduser username
    ```
    
- **`deluser`**  
    Remove a user.  
    _Example:_
    
    ```bash
    sudo deluser username
    ```
    
- **`whoami`**  
    Show the current logged-in user.  
    _Example:_
    
    ```bash
    whoami
    ```
    
- **`who`**  
    Show logged-in users.  
    _Example:_
    
    ```bash
    who
    ```
    

## 8. **Process Management**

- **`ps aux`**  
    List all running processes.  
    _Example:_
    
    ```bash
    ps aux
    ```
    
- **`top`**  
    Display real-time process usage.  
    _Example:_
    
    ```bash
    top
    ```
    
- **`kill`**  
    Terminate a process by PID.  
    _Example:_
    
    ```bash
    kill 1234
    ```
    
- **`killall`**  
    Terminate processes by name.  
    _Example:_
    
    ```bash
    killall firefox
    ```
    

## 9. **Package Management (Debian-based Systems)**

- **`apt update`**  
    Update package lists.  
    _Example:_
    
    ```bash
    sudo apt update
    ```
    
- **`apt upgrade`**  
    Upgrade installed packages.  
    _Example:_
    
    ```bash
    sudo apt upgrade
    ```
    
- **`apt install`**  
    Install a package.  
    _Example:_
    
    ```bash
    sudo apt install curl
    ```
    
- **`apt remove`**  
    Remove a package.  
    _Example:_
    
    ```bash
    sudo apt remove package_name
    ```
    
- **`apt search`**  
    Search for a package.  
    _Example:_
    
    ```bash
    apt search package_name
    ```
    

## 10. **System Monitoring**

- **`uname -a`**  
    Display system information.  
    _Example:_
    
    ```bash
    uname -a
    ```
    
- **`free -h`**  
    Show memory usage in human-readable format.  
    _Example:_
    
    ```bash
    free -h
    ```
    
- **`uptime`**  
    Show system uptime.  
    _Example:_
    
    ```bash
    uptime
    ```
    


---
[Crusveder]