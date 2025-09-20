  
![Basic filtering in a chemistry lab](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1723125963214.svg)  

Although you can run `tcpdump` without providing any filtering expressions, this won’t be useful. Just like in a social gathering, you don’t try to listen to everyone at the same time; you would rather give your attention to a specific person or conversation. Considering the number of packets seen by our network card, it is impossible to see everything at once; we need to be specific and capture what we are interested in inspecting.

### Filtering by Host

Let’s say you are only interested in IP packets exchanged with your network printer or a specific game server. You can easily limit the captured packets to this host using `host IP` or `host HOSTNAME`. In the terminal below, we capture all the packets exchanged with `example.com` and save them to `http.pcap`. It is important to note that capturing packets requires you to be logged-in as `root` or to use `sudo`.

Terminal

```shell-session
user@TryHackMe$ sudo tcpdump host example.com -w http.pcap
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
16:49:02.482295 IP 192.168.139.132.49480 > 93.184.215.14.http: Flags [S], seq 3330895816, win 32120, options [mss 1460,sackOK,TS val 621343956 ecr 0,nop,wscale 7], length 0
16:49:02.635087 IP 93.184.215.14.http > 192.168.139.132.49480: Flags [S.], seq 2231582859, ack 3330895817, win 64240, options [mss 1460], length 0
16:49:02.635125 IP 192.168.139.132.49480 > 93.184.215.14.http: Flags [.], ack 1, win 32120, length 0
16:49:02.635491 IP 192.168.139.132.49480 > 93.184.215.14.http: Flags [P.], seq 1:131, ack 1, win 32120, length 130: HTTP: GET / HTTP/1.1
16:49:02.635580 IP 93.184.215.14.http > 192.168.139.132.49480: Flags [.], ack 131, win 64240, length 0
[...]
^C
13 packets captured
25 packets received by filter
0 packets dropped by kernel
```

If you want to limit the packets to those from a particular source IP address or hostname, you must use `src host IP` or `src host HOSTNAME`. Similarly, you can limit packets to those sent to a specific destination using `dst host IP` or `dst host HOSTNAME`.

### Filtering by Port

If you want to capture all DNS traffic, you can limit the captured packets to those on `port 53`. Remember that DNS uses UDP and TCP ports 53 by default. In the following example, we can see all the DNS queries read by our network card. The terminal below shows two DNS queries: the first query requests the IPv4 address used by example.org, while the second requests the IPv6 address associated with example.org.  

Terminal

```shell-session
user@TryHackMe$ sudo tcpdump -i ens5 port 53 -n
[sudo] password for strategos: 
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
17:26:33.591670 IP 192.168.139.132.47902 > 192.168.139.2.53: 47108+ A? example.org. (29)
17:26:33.591717 IP 192.168.139.132.47902 > 192.168.139.2.53: 5+ AAAA? example.org. (29)
17:26:33.593324 IP 192.168.139.2.53 > 192.168.139.132.47902: 47108 1/0/0 A 93.184.215.14 (45)
17:26:33.593325 IP 192.168.139.2.53 > 192.168.139.132.47902: 5 1/0/0 AAAA 2606:2800:21f:cb07:6820:80da:af6b:8b2c (57)
[...]
^C
12 packets captured
12 packets received by filter
0 packets dropped by kernel
```

In the above example, we captured all the packets sent to or from a specific port number. You can limit the packets to those from a particular source port number or to a particular destination port number using `src port PORT_NUMBER` and `dst port PORT_NUMBER`, respectively.

### Filtering by Protocol

The final type of filtering we will cover is filtering by protocol. You can limit your packet capture to a specific protocol; examples include: `ip`, `ip6`, `udp`, `tcp`, and `icmp`. In the example below, we limit our packet capture to ICMP packets. We can see an ICMP echo request and reply, which is a possible indication that someone is running the `ping` command. There is also an ICMP time exceeded; this might be due to running the `traceroute` command (as explained in the [Networking Essentials](https://tryhackme.com/r/room/networkingessentials) room).

Terminal

```shell-session
user@TryHackMe$ sudo tcpdump -i ens5 icmp -n
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
18:11:00.624681 IP 192.168.139.132 > 93.184.215.14: ICMP echo request, id 47038, seq 1, length 64
18:11:00.781482 IP 93.184.215.14 > 192.168.139.132: ICMP echo reply, id 47038, seq 1, length 64
18:11:04.168792 IP 192.168.139.2 > 192.168.139.132: ICMP time exceeded in-transit, length 68
18:11:04.168815 IP 192.168.139.2 > 192.168.139.132: ICMP time exceeded in-transit, length 68
[...]
18:11:14.857188 IP 93.184.215.14 > 192.168.139.132: ICMP 93.184.215.14 udp port 33495 unreachable, length 68
^C
52 packets captured
52 packets received by filter
0 packets dropped by kernel
```

### Logical Operators

Three logical operators that can be handy:

- `and`: Captures packets where both conditions are true. For example, `tcpdump host 1.1.1.1 and tcp` captures `tcp` traffic with `host 1.1.1.1`.
- `or`: Captures packets when either one of the conditions is true. For instance, `tcpdump udp or icmp` captures UDP or ICMP traffic.
- `not`: Captures packets when the condition is not true. For example, `tcpdump not tcp` captures all packets except TCP segments; we expect to find UDP, ICMP, and ARP packets among the results.

### Summary and Examples

The table below offers a summary of the command line options that we covered.

|Command|Explanation|
|---|---|
|`tcpdump host IP` or `tcpdump host HOSTNAME`|Filters packets by IP address or hostname|
|`tcpdump src host IP` or|Filters packets by a specific source host|
|`tcpdump dst host IP`|Filters packets by a specific destination host|
|`tcpdump port PORT_NUMBER`|Filters packets by port number|
|`tcpdump src port PORT_NUMBER`|Filters packets by the specified source port number|
|`tcpdump dst port PORT_NUMBER`|Filters packets by the specified destination port number|
|`tcpdump PROTOCOL`|Filters packets by protocol; examples include `ip`, `ip6`, and `icmp`|

Consider the following examples:

- `tcpdump -i any tcp port 22` listens on all interfaces and captures `tcp` packets to or from `port 22`, i.e., SSH traffic.
- `tcpdump -i wlo1 udp port 123` listens on the WiFi network card and filters `udp` traffic to `port 123`, the Network Time Protocol (NTP).
- `tcpdump -i eth0 host example.com and tcp port 443 -w https.pcap` will listen on `eth0`, the wired Ethernet interface and filter traffic exchanged with `example.com` that uses `tcp` and `port 443`. In other words, this command is filtering HTTPS traffic related to `example.com`.

For the questions from this task, we will read captured packets from the `traffic.pcap` file. As mentioned earlier, we use `-r FILE` to read from a packet capture file. To test this, try `tcpdump -r traffic.pcap -c 5 -n`; it should display the first five packets in the file without looking up the IP addresses.

Remember that you can count the lines by piping the output via the `wc` command. In the terminal below, we can see that we have 910 packets with the source IP address set to `192.168.124.1`. Please note that we add `-n` to avoid unnecessary delays in attempting to resolve IP addresses. In the example below, we didn’t use `sudo` as reading from a packet capture file does not require `root` privileges.

Terminal

```shell-session
user@TryHackMe$ tcpdump -r traffic.pcap src host 192.168.124.1 -n | wc
reading from file traffic.pcap, link-type EN10MB (Ethernet)
    910   17415  140616
```