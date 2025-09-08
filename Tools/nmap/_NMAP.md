---
dg-publish:
---

---

# 🔍 Nmap Full Command Guide (Detailed)

---

## 📘 1. What is Nmap?

**Nmap (Network Mapper)** is an open-source network scanner used for:

- Discovering hosts
    
- Detecting open ports
    
- Fingerprinting OS and services
    
- Detecting vulnerabilities using NSE (Nmap Scripting Engine)
    

🧪 Used by:

- Network Admins (for auditing)
    
- Ethical Hackers (for reconnaissance)
    
- Security Researchers (for scanning & assessment)
    

---

## 🔧 2. Basic Syntax

```bash
nmap [Scan Type(s)] [Options] <target>
```

Examples:

```bash
nmap 192.168.1.1
nmap -sS -p 1-65535 -T4 192.168.1.1
```

---

## 🧭 3. Host Discovery (Find Live Devices)

### 🔹 Ping Scan (no port scan)

```bash
nmap -sn 192.168.1.0/24
```

- Detects which hosts are up using ICMP Echo
    
- Use-case: Inventory active IPs in a subnet
    

🔹 Example Output:

```
Nmap scan report for 192.168.1.5
Host is up (0.0010s latency).
```

### 🔹 ARP Ping Scan (local network only)

```bash
nmap -PR 192.168.1.0/24
```

- ARP requests are more accurate than ICMP on LANs.
    

---

## 📦 4. Port Scanning

### 🔹 Default Scan (Top 1000 ports)

```bash
nmap 192.168.1.10
```

### 🔹 Scan Specific Ports

```bash
nmap -p 22,80,443 192.168.1.10
```

### 🔹 Full Range (All 65535 ports)

```bash
nmap -p- 192.168.1.10
```

### 🔹 Scan Port Ranges

```bash
nmap -p 1-1000 192.168.1.10
```

🔹 Tip: Combine with `-sV` for service detection.

---

## 🕵️‍♂️ 5. Scan Types (TCP/UDP/Stealth)

### 🔹 TCP SYN Scan (Stealthy)

```bash
nmap -sS 192.168.1.10
```

- Sends SYN packets (half-open scan)
    
- Requires root/admin privileges
    
- Stealthier, often undetected by firewalls
    

### 🔹 TCP Connect Scan

```bash
nmap -sT 192.168.1.10
```

- Completes full TCP handshake
    
- Use when not root
    

### 🔹 UDP Scan

```bash
nmap -sU -p 53,67,161 192.168.1.10
```

- Detects services like DNS, DHCP, SNMP
    
- Slower and less reliable
    

### 🔹 Xmas, FIN, NULL Scans (bypass firewalls)

```bash
nmap -sX 192.168.1.10  # Xmas
nmap -sF 192.168.1.10  # FIN
nmap -sN 192.168.1.10  # NULL
```

- Use in stealth scenarios
    
- Good for testing IDS/IPS
    

---

## 🧠 6. Service and Version Detection

### 🔹 Detect Running Services and Versions

```bash
nmap -sV 192.168.1.10
```

- Tries to identify applications and version numbers (e.g., Apache 2.4.7)
    

### 🔹 Service Intensity

```bash
nmap -sV --version-intensity 9 192.168.1.10
```

- Controls aggressiveness (0–9)
    

---

## 🧪 7. OS Detection

### 🔹 Operating System Detection

```bash
nmap -O 192.168.1.10
```

- Detects OS using TCP/IP stack fingerprinting
    

🔹 Combine with:

```bash
nmap -O --osscan-guess 192.168.1.10
```

- Adds best guess even if accuracy is low
    

---

## 🎯 8. Aggressive Scan

### 🔹 All-in-One Aggressive Scan

```bash
nmap -A 192.168.1.10
```

Includes:

- OS detection
    
- Service version detection
    
- Script scan
    
- Traceroute
    

🔹 Warning: Noisy — easily detected by firewalls

---

## 🧰 9. Nmap Scripting Engine (NSE)

### 🔹 Run Default Scripts

```bash
nmap -sC 192.168.1.10
```

### 🔹 Run Vulnerability Detection Scripts

```bash
nmap --script vuln 192.168.1.10
```

### 🔹 Run Auth or Exploit Scripts

```bash
nmap --script auth 192.168.1.10
nmap --script exploit 192.168.1.10
```

### 🔹 Run Specific Script

```bash
nmap --script http-title 192.168.1.10
```

### 🔹 Combine Scripts

```bash
nmap --script "ftp*,http*" 192.168.1.10
```

---

## 💻 10. Output Formats

### 🔹 Save to File (Normal)

```bash
nmap -oN scan.txt 192.168.1.10
```

### 🔹 Save as XML

```bash
nmap -oX scan.xml 192.168.1.10
```

### 🔹 Save All Formats

```bash
nmap -oA result 192.168.1.10
```

- Produces `result.nmap`, `result.xml`, `result.gnmap`
    

---

## 🚀 11. Performance & Timing

### 🔹 Adjust Speed of Scan

```bash
nmap -T1 192.168.1.10   # Slowest, stealthy
nmap -T4 192.168.1.10   # Faster
nmap -T5 192.168.1.10   # Insane, fast, but detectable
```

---

## 🧱 12. Firewall/IDS Evasion

### 🔹 Fragment Packets

```bash
nmap -f 192.168.1.10
```

### 🔹 Decoy IPs

```bash
nmap -D 192.168.1.1,192.168.1.2,ME 192.168.1.10
```

- Adds fake IPs in the scan traffic
    

### 🔹 Change Source Port

```bash
nmap --source-port 53 192.168.1.10
```

### 🔹 Spoof MAC Address

```bash
nmap --spoof-mac 00:11:22:33:44:55 192.168.1.10
```

---

## 🗂 13. Target Input Types

### 🔹 List of IPs from a File

```bash
nmap -iL targets.txt
```

### 🔹 Exclude Hosts

```bash
nmap 192.168.1.0/24 --exclude 192.168.1.1,192.168.1.5
```

---

## 🧪 14. Real-World Examples

### ✅ Full Port Scan + Aggressive + Save Output

```bash
nmap -p- -A -T4 -oA fullscan 192.168.1.10
```

### ✅ Web Server Detection

```bash
nmap -p 80,443 --script=http-title 192.168.1.10
```

### ✅ Check for Heartbleed

```bash
nmap -p 443 --script ssl-heartbleed 192.168.1.10
```

---

## 🧪 15. Practice Targets

Use these for safe testing:

- `scanme.nmap.org` (Nmap’s official test host)
    
- Local IPs: `127.0.0.1` or `192.168.1.1`
    

---

## 📦 Installation

### Linux

```bash
sudo apt update && sudo apt install nmap  # Debian/Ubuntu
sudo yum install nmap                     # CentOS/RHEL
```

### Windows

- Download: [https://nmap.org/download.html](https://nmap.org/download.html)
    

---

## 📑 Summary Cheatsheet

| Purpose           | Command Example                   |
| ----------------- | --------------------------------- |
| Ping Scan         | `nmap -sn 192.168.1.0/24`         |
| TCP SYN Scan      | `nmap -sS 192.168.1.10`           |
| OS Detection      | `nmap -O 192.168.1.10`            |
| Version Detection | `nmap -sV 192.168.1.10`           |
| Aggressive Scan   | `nmap -A 192.168.1.10`            |
| Run Scripts       | `nmap --script vuln 192.168.1.10` |
| Save Output       | `nmap -oA result 192.168.1.10`    |
| Scan All Ports    | `nmap -p- 192.168.1.10`           |

---

