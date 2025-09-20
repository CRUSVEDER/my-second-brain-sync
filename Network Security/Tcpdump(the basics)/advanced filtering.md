There are many more ways to filter packets. After all, in any real-life situation, we would need to filter through thousands or even millions of packets. It is indispensable to be able to express the exact packets to display. For example, we can limit the displayed packets to those smaller or larger than a certain length:

- `greater LENGTH`: Filters packets that have a length greater than or equal to the specified length
- `less LENGTH`: Filters packets that have a length less than or equal to the specified length

We recommend you check the `pcap-filter` manual page by issuing the command `man pcap-filter`; however, for the purposes of this room, we will focus on one advanced option that allows you to filter packets based on the TCP flags. Understanding the TCP flags will make it easy to build on this knowledge and master more advanced filtering techniques.

### Binary Operations

Before proceeding, it is worth visiting binary operations. A binary operation works on bits, i.e., zeroes and ones. An operation takes one or two bits and returns one bit. Let’s explain in more depth and consider the following three binary operations: `&`, `|`, and `!`.

`&` (And) takes two bits and returns 0 unless both inputs are 1, as shown in the table below.

|Input 1|Input 2|Input1 `&` Input 2|
|---|---|---|
|0|0|0|
|0|1|0|
|1|0|0|
|1|1|1|

`|` (Or) takes two bits and returns 1 unless both inputs are 0. This is shown in the table below.

|Input 1|Input 2|Input 1 `\|` Input 2|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|1|

`!` (Not) takes one bit and inverts it; an input of 1 gives 0, and an input of 0 gives 1, as shown in the table below.

|Input 1|`!` Input 1|
|---|---|
|0|1|
|1|0|

### Header Bytes

The purpose of this section is to be able to filter packets based on the contents of a header byte. Consider the following protocols: ARP, Ethernet, ICMP, IP, TCP, and UDP. These are just a few networking protocols we have studied. How can we tell Tcpdump to filter packets based on the contents of protocol header bytes? (We will not go into details about the headers of each protocol as this is beyond the scope of this room; instead, we will focus on TCP flags.)

Using pcap-filter, Tcpdump allows you to refer to the contents of any byte in the header using the following syntax `proto[expr:size]`, where:

- `proto` refers to the protocol. For example, `arp`, `ether`, `icmp`, `ip`, `ip6`, `tcp`, and `udp` refer to ARP, Ethernet, ICMP, IPv4, IPv6, TCP, and UDP respectively.
- `expr` indicates the byte offset, where `0` refers to the first byte.
- `size` indicates the number of bytes that interest us, which can be one, two, or four. It is optional and is one by default.

To better understand this, consider the following two examples from the pcap-filter manual page (and don’t worry if you find them difficult):

- `ether[0] & 1 != 0` takes the first byte in the Ethernet header and the decimal number 1 (i.e., `0000 0001` in binary) and applies the `&` (the And binary operation). It will return true if the result is not equal to the number 0 (i.e., `0000 0000`). The purpose of this filter is to show packets sent to a multicast address. A multicast Ethernet address is a particular address that identifies a group of devices intended to receive the same data.  
    
- `ip[0] & 0xf != 5` takes the first byte in the IP header and compares it with the hexadecimal number F (i.e., `0000 1111` in binary). It will return true if the result is not equal to the (decimal) number 5 (i.e., `0000 0101` in binary). The purpose of this filter is to catch all IP packets with options.

Don’t worry if you find the above two examples complex. We included them so you know what you can achieve with this; however, fully understanding the above examples is not necessary to finish this task. Instead, we will focus on filtering TCP packets based on the set TCP flags.

You can use `tcp[tcpflags]` to refer to the TCP flags field. The following TCP flags are available to compare with:

- `tcp-syn` TCP SYN (Synchronize)
- `tcp-ack` TCP ACK (Acknowledge)
- `tcp-fin` TCP FIN (Finish)
- `tcp-rst` TCP RST (Reset)
- `tcp-push` TCP Push

Based on the above, we can write:

- `tcpdump "tcp[tcpflags] == tcp-syn"` to capture TCP packets with **only** the SYN (Synchronize) flag set, while all the other flags are unset.
- `tcpdump "tcp[tcpflags] & tcp-syn != 0"` to capture TCP packets with **at least** the SYN (Synchronize) flag set.
- `tcpdump "tcp[tcpflags] & (tcp-syn|tcp-ack) != 0"` to capture TCP packets with **at least** the SYN (Synchronize) **or** ACK (Acknowledge) flags set.

You can write your own filter depending on what you are looking for.