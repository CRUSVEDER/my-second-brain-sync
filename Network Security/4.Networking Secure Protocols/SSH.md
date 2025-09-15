We have used the TELNET protocol in the [Networking Concepts](https://tryhackme.com/r/room/networkingconcepts) room. Although it is very convenient to log in and administer remote systems, it is risky when all the traffic is sent in cleartext. It is easy for anyone monitoring the network traffic to get hold of your login credentials once you use `telnet`. This problem necessitated a solution. Tatu Ylönen developed the Secure Shell (SSH) protocol and released SSH-1 in **1995** as freeware. (Interestingly, it was the same year that Netscape Communications released the SSL 2.0 protocol.) A more secure version, SSH-2, was defined in 1996. In **1999**, the OpenBSD developers released OpenSSH, an open-source implementation of SSH. Nowadays, when you use an SSH client, it is most likely based on OpenSSH libraries and source code.

OpenSSH offers several benefits. We will list a few key points:

- **Secure authentication**: Besides password-based authentication, SSH supports public key and two-factor authentication.
- **Confidentiality**: OpenSSH provides end-to-end encryption, protecting against eavesdropping. Furthermore, it notifies you of new server keys to protect against man-in-the-middle attacks.
- **Integrity**: In addition to protecting the confidentiality of the exchanged data, cryptography also protects the integrity of the traffic.
- **Tunneling**: SSH can create a secure “tunnel” to route other protocols through SSH. This setup leads to a VPN-like connection.
- **X11 Forwarding**: If you connect to a Unix-like system with a graphical user interface, SSH allows you to use the graphical application over the network.

You would issue the command `ssh username@hostname` to connect to an SSH server. If the username is the same as your logged-in username, you only need `ssh hostname`. Then, you will be asked for a password; however, if public-key authentication is used, you will be logged in immediately.

The screenshot below shows an example of running Wireshark on a remote Kali Linux system. The argument `-X` is required to support running graphical interfaces, for example, `ssh 192.168.124.148 -X`. (The local system needs to have a suitable graphical system installed.)

![After establishing an SSH connection to a remote server, we successfully started Wireshark, an application with a graphical user interface.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1721903514417.png)

While the TELNET server listens on port 23, the SSH server listens on port 22.