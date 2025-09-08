In this room, we learned how to use Nmap to discover live hosts on any network. We also explored the common types of port scans and how we can use Nmap to find service version numbers. We also learned how to control the timing of the scan, and finally, we covered the different formats for saving Nmap scan results.

It is worth noting that it is best to run Nmap with `sudo` privileges so that we can make use of all its features. Running Nmap with local user privileges will still work; however, you should expect many features to be unavailable. You get a minimal portion of Nmap’s power when running it as a local user. For instance, Nmap would automatically use SYN scan (`-sS`) if you are running it with `sudo` privileges and will default to connect scan (`-sT`) if run as a local user. The reason is that crafting certain packets, such as sending a TCP SYN packet, requires root privileges.

Nmap is a very rich tool, and we only covered the most common and essential features in this room. In the [Network Security](https://tryhackme.com/module/network-security) module, four rooms are dedicated exclusively to Nmap. The table below lists most of the options we explained in this room to help you review and remember them.

|Option|Explanation|
|---|---|
|`-sL`|List scan – list targets without scanning|
|**_Host Discovery_**||
|`-sn`|Ping scan – host discovery only|
|**_Port Scanning_**||
|`-sT`|TCP connect scan – complete three-way handshake|
|`-sS`|TCP SYN – only first step of the three-way handshake|
|`-sU`|UDP Scan|
|`-F`|Fast mode – scans the 100 most common ports|
|`-p[range]`|Specifies a range of port numbers – `-p-` scans all the ports|
|`-Pn`|Treat all hosts as online – scan hosts that appear to be down|
|**_Service Detection_**||
|`-O`|OS detection|
|`-sV`|Service version detection|
|`-A`|OS detection, version detection, and other additions|
|**_Timing_**||
|`-T<0-5>`|Timing template – paranoid (0), sneaky (1), polite (2), normal (3), aggressive (4), and insane (5)|
|`--min-parallelism <numprobes>` and `--max-parallelism <numprobes>`|Minimum and maximum number of parallel probes|
|`--min-rate <number>` and `--max-rate <number>`|Minimum and maximum rate (packets/second)|
|`--host-timeout`|Maximum amount of time to wait for a target host|
|**_Real-time output_**||
|`-v`|Verbosity level – for example, `-vv` and `-v4`|
|`-d`|Debugging level – for example `-d` and `-d9`|
|**_Report_**||
|`-oN <filename>`|Normal output|
|`-oX <filename>`|XML output|
|`-oG <filename>`|`grep`-able output|
|`-oA <basename>`|Output in all major formats|
