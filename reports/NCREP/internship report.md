## Introduction

This report describes the work completed during my internship. The internship focused on Capture the Flag (CTF) problem solving and penetration testing. I carried out practical tasks that involved cryptography, binary analysis, and Active Directory exploitation. Each task was documented and analyzed to improve my technical ability and reporting skills.

## Background

The internship was conducted with **NullClass**, where the focus was on learning cybersecurity through structured tasks. The program emphasized two areas: solving CTF problems and working on penetration testing labs.

Before starting, I had some experience with **Nmap**, Linux tools, and basic CTF practice on platforms such as HackTheBox. This gave me an entry point into service enumeration and exploitation.

The tasks were designed to reflect real-world security scenarios. CTF problems helped me practice cryptography and reverse engineering in controlled challenges. The penetration testing labs mirrored enterprise environments, with Active Directory, SMB, and Kerberos services. Together, these tasks provided an applied learning environment for improving practical security skills.

## Learning Objectives

- Learn how to break weak cryptographic systems.
    
- Apply reverse engineering to find hidden keys and flags.
    
- Perform enumeration of Windows services, including SMB.
    
- Test and validate credentials on a domain environment.
    
- Improve technical reporting and structured write-ups.
    

## Activities and Tasks

### Task 1: Capture the Flag (BMCTF)

- **RSA Challenge**: Factored a small RSA modulus, computed the private key, and decrypted the ciphertext.
    
- **XOR Challenge**: Used static analysis with `strings` to extract the embedded flag.
    
- **Binary Reversing**: Applied `radare2` to analyze binary functions and identify hidden logic.
    
- **File Analysis**: Used `exiftool` and `xxd` to detect hidden or unusual content in files.


**Outcome**: Multiple flags were recovered using cryptography, binary analysis, and file inspection techniques.

🔗 medium link: https://medium.com/@yashgholap/task-1-ba21fedd9bd8

---

### Task 2: medium difficulty Penetration Testing Lab (Tomb Watcher)

- **Scanning**: Ran Nmap to identify open ports and services including DNS, HTTP, Kerberos, and SMB.
    
- **Host Setup**: Added target entries to `/etc/hosts` for domain resolution.
    
- **Credential Testing**: Verified provided credentials with CrackMapExec against SMB. Authentication was successful.
    
- **SMB Enumeration**: Listed available shares using `smbclient`, which revealed ADMIN$, C$, IPC$, NETLOGON, and SYSVOL.
    
- **Web Enumeration**: Used Gobuster for directory brute forcing on the IIS server.


**Outcome**: Gained valid access through SMB, enumerated shares, and confirmed the environment as a Windows Server domain controller.

🔗 medium link: https://yashgholap.medium.com/task-2-be5ec9cf1a68


---

## Skills and Competencies

- **Cryptography**: RSA factorization and decryption.
    
- **Reverse Engineering**: Static analysis with `strings` and `radare2`.
    
- **Pentesting Tools**: Nmap, CrackMapExec, smbclient, Gobuster.
    
- **Active Directory Security**: Enumeration of LDAP, Kerberos, and SMB services.
    
- **Documentation**: Clear and structured technical write-ups.
    

## Feedback and Evidence

- Screenshots :

Task 1:

![](https://miro.medium.com/v2/resize:fit:700/0*NEXfSJdFyYl7wPMC.png)
*i took this before ctf started.*

![](../../_attachments/Pasted%20image%2020250629112800.png)

Task 2:

![](../../_attachments/Pasted%20image%2020250619215120.png)

![](../../_attachments/Pasted%20image%2020250619215158.png)

- Medium write-ups of selected tasks.  
    🔗 medium link task 1: https://medium.com/@yashgholap/task-1-ba21fedd9bd8
    🔗 medium link task 1: https://yashgholap.medium.com/task-2-be5ec9cf1a68

## Challenges and Solutions

- **RSA Output Not Readable**  
    _Solution_: Converted the decimal plaintext to hexadecimal and used it as the flag.
    
- **Binary Without Clear Output**  
    _Solution_: Applied static analysis to extract embedded strings.
    
- **Too Many Open Ports in Pentest Lab**  
    _Solution_: Focused on the core Active Directory services first before moving to web enumeration.

## Outcomes and Impact

The internship improved my ability to analyze and exploit systems in practice. I learned how to move from theory to hands-on problem solving. I became confident in cryptography attacks, binary analysis, and service enumeration in Windows environments. The structured documentation reinforced the value of clear reporting.

## Conclusion

The internship provided practical exposure to both CTF problem solving and enterprise penetration testing. It built my skills in cryptography, reverse engineering, and Active Directory security. The experience prepared me for more advanced cybersecurity challenges and future professional roles.
