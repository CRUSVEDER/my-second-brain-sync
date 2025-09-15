Now that we have covered the conceptual ISO OSI model, it is time to study an implemented model, the TCP/IP model. TCP/IP stands for Transmission Control Protocol/Internet Protocol and was developed in the 1970s by the Department of Defense (DoD). I hear you ask why DoD would create such a model. One of the strengths of this model is that it allows a network to continue to function as parts of it are out of service, for instance, due to a military attack. This capability is possible in part due to the design of the routing protocols to adapt as the network topology changes.

In our presentation of the ISO OSI model, we went from bottom to top, from layer 1 to layer 7. In this task, let’s look at things from a different perspective, from top to bottom. From top to bottom, we have:

- **Application Layer**: The OSI model application, presentation and session layers, i.e., layers 5, 6, and 7, are grouped into the application layer in the TCP/IP model.
- **Transport Layer**: This is layer 4.
- **Internet Layer**: This is layer 3. The OSI model’s network layer is called the Internet layer in the TCP/IP model.
- **Link Layer**: This is layer 2.

The table below shows how the TCP/IP model layers map to the ISO/OSI model layers.

|Layer Number|ISO OSI Model|TCP/IP Model (RFC 1122)|Protocols|
|---|---|---|---|
|7|Application Layer|Application Layer|HTTP, HTTPS, FTP, POP3, SMTP, IMAP, Telnet, SSH,|
|6|Presentation Layer|
|5|Session Layer|
|4|Transport Layer|Transport Layer|TCP, UDP|
|3|Network Layer|Internet Layer|IP, ICMP, IPSec|
|2|Data Link Layer|Link Layer|Ethernet 802.3, WiFi 802.11|
|1|Physical Layer|||

Many modern networking textbooks show the TCP/IP model as five layers instead of four. For example, in Computer Networking: A Top-Down Approach 8th Edition, [Kurose and Ross](http://gaia.cs.umass.edu/kurose_ross/index.php) describe the following five-layer Internet protocol stack by including the physical layer:

- Application
- Transport
- Network
- Link
- Physical

In the following tasks, we will cover the IP protocol from the Internet layer and the UDP and TCP protocols from the transport layer.