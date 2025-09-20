Tcpdump is a rich program with many options to customize how the packets are printed and displayed. We have selected to cover the following five options:

- `-q`: Quick output; print brief packet information
- `-e`: Print the link-level header
- `-A`: Show packet data in ASCII
- `-xx`: Show packet data in hexadecimal format, referred to as hex
- `-X`: Show packet headers and data in hex and ASCII

To demonstrate how the above options manipulate the output, we will first display two captured packets without using any additional arguments.

Terminal

```shell-session
user@TryHackMe$ tcpdump -r TwoPackets.pcap
reading from file TwoPackets.pcap, link-type EN10MB (Ethernet), snapshot length 262144
18:59:59.979771 IP 104.18.12.149.https > g5000.45248: Flags [P.], seq 2695955324:2695955349, ack 2856007037, win 16, options [nop,nop,TS val 412758285 ecr 3959057198], length 25
18:59:59.980574 IP g5000.45248 > 104.18.12.149.https: Flags [P.], seq 1:30, ack 25, win 2175, options [nop,nop,TS val 3959057384 ecr 412758285], length 29
```

### Brief Packet Information

If you prefer shorter output lines, you can opt for “quick” output with `-q`. The following example shows the timestamp, along with the source and destination IP addresses and source and destination port numbers.

Terminal

```shell-session
user@TryHackMe$ tcpdump -r TwoPackets.pcap -q
reading from file TwoPackets.pcap, link-type EN10MB (Ethernet), snapshot length 262144
18:59:59.979771 IP 104.18.12.149.https > g5000.45248: tcp 25
18:59:59.980574 IP g5000.45248 > 104.18.12.149.https: tcp 29
```

### Displaying Link-Level Header

If you are on an Ethernet or WiFi network and want to include the MAC addresses in Tcpdump output, all you need to do is to add `-e`. This is convenient when you are learning how specific protocols, such as ARP and DHCP function. It can also help you track the source of any unusual packets on your network.

Terminal

```shell-session
user@TryHackMe$ tcpdump -r TwoPackets.pcap -e
reading from file TwoPackets.pcap, link-type EN10MB (Ethernet), snapshot length 262144
18:59:59.979771 44:df:65:d8:fe:6c (oui Unknown) > 02:83:1e:40:5d:17 (oui Unknown), ethertype IPv4 (0x0800), length 91: 104.18.12.149.https > g5000.45248: Flags [P.], seq 2695955324:2695955349, ack 2856007037, win 16, options [nop,nop,TS val 412758285 ecr 3959057198], length 25
18:59:59.980574 02:83:1e:40:5d:17 (oui Unknown) > 44:df:65:d8:fe:6c (oui Unknown), ethertype IPv4 (0x0800), length 95: g5000.45248 > 104.18.12.149.https: Flags [P.], seq 1:30, ack 25, win 2175, options [nop,nop,TS val 3959057384 ecr 412758285], length 29
```

### Displaying Packets as ASCII

ASCII stands for American Standard Code for Information Interchange; ASCII codes represent text. In other words, you can expect `-A` to display all the bytes mapped to English letters, numbers, and symbols.

Terminal

```shell-session
user@TryHackMe$ tcpdump -r TwoPackets.pcap -A
reading from file TwoPackets.pcap, link-type EN10MB (Ethernet), snapshot length 262144
18:59:59.979771 IP 104.18.12.149.https > g5000.45248: Flags [P.], seq 2695955324:2695955349, ack 2856007037, win 16, options [nop,nop,TS val 412758285 ecr 3959057198], length 25
E..M..@.5..)h.....BY.......|.;5}...........
..1...k......j.3.2.....&9a.....-L
18:59:59.980574 IP g5000.45248 > 104.18.12.149.https: Flags [P.], seq 1:30, ack 25, win 2175, options [nop,nop,TS val 3959057384 ecr 412758285], length 29
E..Ql.@.@.VV..BYh........;5}...............
..k...1.......1.y.&VC<#._J$..z...D#.`
```

### Displaying Packets in Hexadecimal Format

ASCII format works well when the packet contents are plain-text English. It won’t work if the contents have undergone encryption or even compression. Furthermore, it won’t work for languages that don’t use the English alphabet. Hence, we need another way to display the packet contents regardless of format. Being 8 bits, any octet can be displayed as two hexadecimal digits. (Each hexadecimal digit represents 4 bits.) To display the packets in hexadecimal format, we must add `-xx` as shown in the terminal below.

Terminal

```shell-session
user@TryHackMe$ tcpdump -r TwoPackets.pcap -xx
reading from file TwoPackets.pcap, link-type EN10MB (Ethernet), snapshot length 262144
18:59:59.979771 IP 104.18.12.149.https > g5000.45248: Flags [P.], seq 2695955324:2695955349, ack 2856007037, win 16, options [nop,nop,TS val 412758285 ecr 3959057198], length 25
        0x0000:  0283 1e40 5d17 44df 65d8 fe6c 0800 4500
        0x0010:  004d fbd8 4000 3506 d229 6812 0c95 c0a8
        0x0020:  4259 01bb b0c0 a0b1 037c aa3b 357d 8018
        0x0030:  0010 f905 0000 0101 080a 189a 310d ebfa
        0x0040:  6b2e 1703 0300 146a 8f33 1832 e6a2 fb99
        0x0050:  eb26 3961 dad4 1611 152d 4c
18:59:59.980574 IP g5000.45248 > 104.18.12.149.https: Flags [P.], seq 1:30, ack 25, win 2175, options [nop,nop,TS val 3959057384 ecr 412758285], length 29
        0x0000:  44df 65d8 fe6c 0283 1e40 5d17 0800 4500
        0x0010:  0051 6ca8 4000 4006 5656 c0a8 4259 6812
        0x0020:  0c95 b0c0 01bb aa3b 357d a0b1 0395 8018
        0x0030:  087f 17e0 0000 0101 080a ebfa 6be8 189a
        0x0040:  310d 1703 0300 18f4 31fa 798d 2656 433c
        0x0050:  2389 5f4a 24c2 fa7a 1496 8444 238e 60
```

Adding `-xx` lets us see the packet octet by octet. In the example above, we can closely inspect the IP and TCP headers in addition to the packet contents.

### Best of Both Worlds

If you would like to display the captured packets in hexadecimal and ASCII formats, Tcpdump makes it easy with the `-X` option.

Terminal

```shell-session
user@TryHackMe$ tcpdump -r TwoPackets.pcap -X
reading from file TwoPackets.pcap, link-type EN10MB (Ethernet), snapshot length 262144
18:59:59.979771 IP 104.18.12.149.https > g5000.45248: Flags [P.], seq 2695955324:2695955349, ack 2856007037, win 16, options [nop,nop,TS val 412758285 ecr 3959057198], length 25
        0x0000:  4500 004d fbd8 4000 3506 d229 6812 0c95  E..M..@.5..)h...
        0x0010:  c0a8 4259 01bb b0c0 a0b1 037c aa3b 357d  ..BY.......|.;5}
        0x0020:  8018 0010 f905 0000 0101 080a 189a 310d  ..............1.
        0x0030:  ebfa 6b2e 1703 0300 146a 8f33 1832 e6a2  ..k......j.3.2..
        0x0040:  fb99 eb26 3961 dad4 1611 152d 4c         ...&9a.....-L
18:59:59.980574 IP g5000.45248 > 104.18.12.149.https: Flags [P.], seq 1:30, ack 25, win 2175, options [nop,nop,TS val 3959057384 ecr 412758285], length 29
        0x0000:  4500 0051 6ca8 4000 4006 5656 c0a8 4259  E..Ql.@.@.VV..BY
        0x0010:  6812 0c95 b0c0 01bb aa3b 357d a0b1 0395  h........;5}....
        0x0020:  8018 087f 17e0 0000 0101 080a ebfa 6be8  ..............k.
        0x0030:  189a 310d 1703 0300 18f4 31fa 798d 2656  ..1.......1.y.&V
        0x0040:  433c 2389 5f4a 24c2 fa7a 1496 8444 238e  C<#._J$..z...D#.
        0x0050:  60
```

### Summary and Examples

The table below provides a summary of the command line options that we covered.

|Command|Explanation|
|---|---|
|`tcpdump -q`|Quick and quite: brief packet information|
|`tcpdump -e`|Include MAC addresses|
|`tcpdump -A`|Print packets as ASCII encoding|
|`tcpdump -xx`|Display packets in hexadecimal format|
|`tcpdump -X`|Show packets in both hexadecimal and ASCII formats|
