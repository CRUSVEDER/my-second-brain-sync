---
dg-publish:
---
---
# Connect

![](../../_attachments/Pasted%20image%2020250619215037.png)
connected to kali via 'openvpn'

![](../../_attachments/Pasted%20image%2020250619215120.png)

# verify 
using ping

![](../../_attachments/Pasted%20image%2020250619215158.png)

---
# Scanning

## command i used:
`nmap -p 1-5000 -sC -sV -T4 -oN scan_result_tombwatcher.txt 10.10.11.72`

![](../../_attachments/Pasted%20image%2020250619215214.png)
![](../../_attachments/Pasted%20image%2020250619215227.png)

this reveals:

## outputs:


````
# Nmap 7.94SVN scan initiated Sun Aug 17 05:36:27 2025 as: /usr/lib/nmap/nmap -p 1-5000 -sC -sV -T4 -oN scan_result_tombwatcher.txt 10.10.11.72
Nmap scan report for 10.10.11.72
Host is up (0.22s latency).
Not shown: 4988 filtered tcp ports (no-response)
PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
80/tcp   open  http          Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: IIS Windows Server
|_http-server-header: Microsoft-IIS/10.0
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2025-08-17 13:37:07Z)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: tombwatcher.htb0., Site: Default-First-Site-Name)
|_ssl-date: 2025-08-17T13:38:31+00:00; +4h00m04s from scanner time.
| ssl-cert: Subject: commonName=DC01.tombwatcher.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:DC01.tombwatcher.htb
| Not valid before: 2024-11-16T00:47:59
|_Not valid after:  2025-11-16T00:47:59
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp  open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: tombwatcher.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC01.tombwatcher.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:DC01.tombwatcher.htb
| Not valid before: 2024-11-16T00:47:59
|_Not valid after:  2025-11-16T00:47:59
|_ssl-date: 2025-08-17T13:38:32+00:00; +4h00m04s from scanner time.
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: tombwatcher.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC01.tombwatcher.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:DC01.tombwatcher.htb
| Not valid before: 2024-11-16T00:47:59
|_Not valid after:  2025-11-16T00:47:59
|_ssl-date: 2025-08-17T13:38:31+00:00; +4h00m04s from scanner time.
3269/tcp open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: tombwatcher.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC01.tombwatcher.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:DC01.tombwatcher.htb
| Not valid before: 2024-11-16T00:47:59
|_Not valid after:  2025-11-16T00:47:59
|_ssl-date: 2025-08-17T13:38:32+00:00; +4h00m04s from scanner time.
Service Info: Host: DC01; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2025-08-17T13:37:53
|_  start_date: N/A
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
|_clock-skew: mean: 4h00m03s, deviation: 0s, median: 4h00m03s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sun Aug 17 05:38:29 2025 -- 1 IP address (1 host up) scanned in 122.41 seconds
````


### ports & sv explained:

| Port     | Service          | Purpose                                                   |
| -------- | ---------------- | --------------------------------------------------------- |
| **53**   | domain           | DNS — often used by AD for internal name resolution.      |
| **80**   | http             | Web service — may host admin panels or web interfaces.    |
| **88**   | kerberos-sec     | Kerberos authentication — core part of AD.                |
| **135**  | msrpc            | Microsoft RPC — used for various Windows services.        |
| **139**  | netbios-ssn      | NetBIOS — legacy file/printer sharing.                    |
| **389**  | ldap             | LDAP — directory services, typically AD-related.          |
| **445**  | microsoft-ds     | SMB — file sharing, often exploitable.                    |
| **464**  | kpasswd5         | Kerberos password change service.                         |
| **593**  | http-rpc-epmap   | Remote procedure call over HTTP.                          |
| **636**  | ldapssl          | LDAP over SSL/TLS.                                        |
| **3268** | globalcatLDAP    | Global Catalog service — used for forest-wide AD queries. |
| **3269** | globalcatLDAPssl | Secure Global Catalog.                                    |

# command
`echo '10.10.11.72 DC01.tombwatcher.htb tombwatcher.htb' | sudo tee -a /etc/hosts`

# ![](../../_attachments/Pasted%20image%2020250817152620.png)