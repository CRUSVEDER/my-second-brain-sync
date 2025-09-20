  
The main challenge when studying networking protocols is that we don’t get a chance to see the protocol “conversations” taking place. All the technical complexities are hidden behind friendly and elegant user interfaces. You access resources on your local network without ever seeing an ARP query. Similarly, you would access Internet services for years without seeing a single three-way handshake till you check a networking book or inspect a network traffic capture. The best study aid would be capturing network traffic and taking a closer look at the various protocols; this helps us better understand how networks work.

This room introduces some basic command-line arguments for using Tcpdump. The Tcpdump tool and its `libpcap` library are written in C and C++ and were released for Unix-like systems in the late 1980s or early 1990s. Consequently, they are very stable and offer optimal speed. The `libpcap` library is the foundation for various other networking tools today. Moreover, it was ported to MS Windows as `winpcap`.

### Learning Objectives

This room aims to provide you with the basics necessary to use `tcpdump`. In particular, you will learn how to:

- Capture packets and save them to a file
- Set filters on captured packets
- Control how captured packets are displayed

### Room Prerequisites

We recommend the user be familiar with the TCP/IP model, its related concepts, and its various protocols. The following rooms provide the necessary knowledge to make the best use of this room:

- [Networking Concepts](https://tryhackme.com/r/room/networkingconcepts)
- [Networking Essentials](https://tryhackme.com/r/room/networkingessentials)
- [Networking Core Protocols](https://tryhackme.com/r/room/networkingcoreprotocols)
- [Networking Secure Protocols](https://tryhackme.com/r/room/networkingsecureprotocols)