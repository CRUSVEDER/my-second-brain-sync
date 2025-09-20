You can run `tcpdump` without providing any arguments; however, this is only useful to test that you have it installed! In any real scenario, we must be specific about what to listen to, where to write, and how to display the packets.

### Specify the Network Interface

The first thing to decide is which network interface to listen to using `-i INTERFACE`. You can choose to listen on all available interfaces using `-i any`; alternatively, you can specify an interface you want to listen on, such as `-i eth0`.

A command such as `ip address show` (or merely `ip a s`) would list the available network interfaces. In the terminal below, we see one network card, `ens5`, in addition to the loopback address.

Terminal

```shell-session
user@TryHackMe$ ip a s
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
[...]
2: ens5: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc mq state UP group default qlen 1000
[...]
```

### Save the Captured Packets

In many cases, you should check the captured packets again later. This can be achieved by saving to a file using `-w FILE`. The file extension is most commonly set to `.pcap`. The saved packets can be inspected later using another program, such as Wireshark. You won’t see the packets scrolling when you choose the `-w` option.

#### Read Captured Packets from a File

You can use Tcpdump to read packets from a file by using `-r FILE`. This is very useful for learning about protocol behaviour. You can capture network traffic over a suitable time frame to inspect a specific protocol, then read the captured file while applying filters to display the packets you are interested in. Furthermore, it might be a packet capture file that contains a network attack that took place, and you inspect it to analyze the attack.

### Limit the Number of Captured Packets

You can specify the number of packets to capture by specifying the count using `-c COUNT`. Without specifying a count, the packet capture will continue till you interrupt it, for example, by pressing CTRL-C. Depending on your goal, you only need a limited number of packets.

### Don’t Resolve IP Addresses and Port Numbers

Tcpdump will resolve IP addresses and print friendly domain names where possible. To avoid making such DNS lookups, you can use the `-n` argument. Similarly, if you don’t want port numbers to be resolved, such as `80` being resolved to `http`, you can use the `-nn` to stop both DNS and port number lookups. Consider the following example shown in the terminal below. We captured and displayed five packets without resolving the IP addresses.

Terminal

```shell-session
user@TryHackMe$ sudo tcpdump -i ens5 -c 5 -n
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on ens5, link-type EN10MB (Ethernet), capture size 262144 bytes
08:55:18.989213 IP 10.10.117.2.22 > 10.11.81.126.53378: Flags [P.], seq 2888580014:2888580210, ack 771262362, win 922, options [nop,nop,TS val 3216251159 ecr 33295823], length 196
08:55:18.989446 IP 10.10.117.2.22 > 10.11.81.126.53378: Flags [P.], seq 196:424, ack 1, win 922, options [nop,nop,TS val 3216251159 ecr 33295823], length 228
08:55:18.989576 IP 10.10.117.2.22 > 10.11.81.126.53378: Flags [P.], seq 424:620, ack 1, win 922, options [nop,nop,TS val 3216251159 ecr 33295823], length 196
08:55:18.989839 IP 10.10.117.2.22 > 10.11.81.126.53378: Flags [P.], seq 620:816, ack 1, win 922, options [nop,nop,TS val 3216251159 ecr 33295823], length 196
08:55:18.989958 IP 10.10.117.2.22 > 10.11.81.126.53378: Flags [P.], seq 816:1012, ack 1, win 922, options [nop,nop,TS val 3216251159 ecr 33295823], length 196
5 packets captured
6 packets received by filter
0 packets dropped by kernel
```

### Produce (More) Verbose Output

If you want to print more details about the packets, you can use `-v` to produce a slightly more verbose output. According to the Tcpdump manual page (`man tcpdump`), the addition of `-v` will print “the time to live, identification, total length and options in an IP packet” among other checks. The `-vv` will produce more verbose output; the `-vvv` will provide even more verbosity; check the manual page for details.

### Summary and Examples

The table below provides a summary of the command line options that we covered.

|Command|Explanation|
|---|---|
|`tcpdump -i INTERFACE`|Captures packets on a specific network interface|
|`tcpdump -w FILE`|Writes captured packets to a file|
|`tcpdump -r FILE`|Reads captured packets from a file|
|`tcpdump -c COUNT`|Captures a specific number of packets|
|`tcpdump -n`|Don’t resolve IP addresses|
|`tcpdump -nn`|Don’t resolve IP addresses and don’t resolve protocol numbers|
|`tcpdump -v`|Verbose display; verbosity can be increased with `-vv` and `-vvv`|

Consider the following examples:

- `tcpdump -i eth0 -c 50 -v` captures and displays 50 packets by listening on the `eth0` interface, which is a wired Ethernet, and displays them verbosely.
- `tcpdump -i wlo1 -w data.pcap` captures packets by listening on the `wlo1` interface (the WiFi interface) and writes the packets to `data.pcap`. It will continue till the user interrupts the capture by pressing CTRL-C.
- `tcpdump -i any -nn` captures packets on all interfaces and displays them on screen without domain name or protocol resolution.