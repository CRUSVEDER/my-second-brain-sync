---
title: 3. cybersec tips & tricks
date: 2024-12-01
draft: 
Toc: true
tags:
  - cybersec
  - tips/tricks
---


---
# **Cybersecurity Tips and Tools for Beginners: Hackers Hate These Simple Tricks**

So, you’ve stumbled into the world of cybersecurity, huh? Good choice! Whether you're here to keep your personal data safe or dreaming of becoming the internet's Batman, you're in the right place. This blog is your crash course—no fluff, just actionable tips and beginner-friendly tools. Let’s jump in!

---

## **Step 1: Know Your Enemies (Yes, There Are Many)**

Cyber threats come in all shapes and sizes, from sneaky scammers to sophisticated hacking groups. Here are the main culprits you’ll face:

- **Phishing**: These scammers pretend to be your bank, Netflix, or even a Nigerian prince to steal your info. Look out for weird URLs and typos.
- **Ransomware**: A digital hostage situation where your files get locked, and you’re asked to pay in Bitcoin.
- **Man-in-the-Middle Attacks**: This happens when a hacker intercepts your communication (like your email or bank logins) over unsecured networks.

### **How to Protect Yourself**:

- Never trust unsolicited emails. If it’s too good to be true, it probably is.
- Use VPNs like **ProtonVPN** to encrypt your internet connection on public Wi-Fi.
- Get in the habit of checking URLs and sender addresses for red flags.

---

## **Step 2: Tools You Need to Level Up**

Let’s talk tools. These aren’t just for geeks in dark rooms—they’re essential for anyone serious about cybersecurity.

### **1. Wireshark: Analyze Your Network Like a Pro**

Wireshark is like Google Maps for your internet traffic. It lets you see everything happening on your network. Here’s how to get started:

- **Step 1**: Install Wireshark on your system (free and open-source).
- **Step 2**: Choose a network interface (Wi-Fi or Ethernet) and click "Start."
- **Step 3**: Apply filters (e.g., `http` or `tcp.port==443`) to focus on specific traffic types.
- **Step 4**: Look for anomalies, like traffic to unknown IPs or repeated failed login attempts.

**Pro Tip**: Use Wireshark’s color coding to quickly identify different types of traffic—green for TCP, blue for DNS, etc. It’s like having a cheat sheet built right in.

![[wireshark-live-capture.png]]


---

### **2. Nmap: The Network Scanner Everyone Loves**

Nmap is a command-line tool that scans networks to identify devices, open ports, and potential vulnerabilities. It’s a must-have for beginners learning about penetration testing.

Here’s how to use it:

- **Basic Network Scan**:
    
    ```
    nmap -sn 192.168.1.0/24  
    ```
    
    This scans all devices on your local network.
- **Detailed Scan**:
    
    ```
    nmap -sS -p 1-1000 192.168.1.10  
    ```
    
    This checks the first 1,000 ports on a specific device for open or vulnerable services.

**Pro Tip**: Pair Nmap with **Zenmap** (a graphical interface) if you’re still warming up to command lines.

![[1_eju_tKQSYYL5MDk0BtWBLg.png]]


---
### **3. Password Managers: The Easiest Security Boost Ever**

Let’s face it, remembering passwords is the worst. A password manager like **Bitwarden** or **Dashlane** stores all your login info securely.

- **Step 1**: Create a strong master password (at least 12 characters with letters, numbers, and symbols).
- **Step 2**: Let the manager generate unique passwords for each account.
- **Step 3**: Sync across your devices so you’re always covered.

**Why It’s Essential**:  
Password reuse is like leaving your front door key under the mat—it’s an open invite for hackers.

---

## **Step 3: Protect Yourself with Good Habits**

Even the best tools won’t help if you ignore basic cybersecurity practices. Here are the must-dos:

### **1. Enable Two-Factor Authentication (2FA)**

Adding 2FA to your accounts is like putting a deadbolt on your digital doors. Use apps like **Authy** or **Google Authenticator** instead of SMS for added security.

### **2. Keep Your Software Updated**

Outdated apps and operating systems are hacker bait. Enable auto-updates for your phone, laptop, and browser extensions.

### **3. Don’t Click Random Links**

It doesn’t matter how tempting it looks—"FREE iPhone 15!" links lead to scams, not Apple’s generosity.

### **4. Backup Your Data**

Use cloud services like Google Drive or OneDrive alongside an external hard drive. Set up automatic backups so you never lose anything to ransomware or hardware failures.

---

## **Step 4: Practice Your Skills (Legally, Please)**

The best way to learn cybersecurity is by doing. Luckily, there are platforms designed for beginners:

- **TryHackMe**: Step-by-step labs that teach you hacking and defensive techniques.
- **OverTheWire**: Fun games that help you master Linux commands and networking basics.
- **Hack The Box (Beginner Track)**: Once you’re feeling confident, test your skills on live machines.

**Pro Tip**: Don’t be afraid to fail—it’s all part of learning. Just don’t mess with systems you don’t own. (Seriously, that’s a crime!)

---
### **Serious Caution: The Dark Web Isn’t a Playground**

The dark web might seem intriguing, but it’s a risky space for beginners. While it can be used for legitimate purposes (like protecting privacy via Tor), it’s also a hub for illegal activities—stolen data, malware, and hacking tools.

Here’s why you should be cautious:

- **Legal Risks**: Just accessing certain dark web marketplaces or forums can get you in trouble with the law. Tools like Tor may anonymize your traffic, but they don’t make illegal activity any less illegal.
- **Cybersecurity Risks**: The dark web is a hotbed for malware. Downloading files from unknown sources, even seemingly harmless ones, could expose your system to trojans, ransomware, or keyloggers.
- **Data Exposure**: Hackers frequently exchange stolen credentials and personal data. If you visit the wrong site, your personal information could be at risk, or worse, you could become a target for attacks.

If you’re curious about the technology, like Tor or encryption, stick to safe, legal environments for learning. Avoid accessing the dark web without a clear, informed purpose. The risks outweigh any potential gain for beginners.

---

## **Final Thoughts: Start Small, Aim Big**

Cybersecurity isn’t a sprint; it’s a marathon. Start with simple tools like Wireshark and Nmap, build good habits, and practice consistently. Before you know it, you’ll be the go-to person for all things cyber (and maybe even impress your crush with your “hacker skills”).

If you’re ready to dive deeper, check out platforms like **TryHackMe** or certifications like **CompTIA Security+** to get serious street cred in the cyber world.

---
 [Crusveder]