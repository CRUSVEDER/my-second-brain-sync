Press the **Start Machine** button below.

Start Machine

Start the AttackBox by pressing the **Start AttackBox** button at the top of this page. The AttackBox machine will start in Split-Screen view. If it is not visible, use the blue **Show Split View** button at the top of the page.

Give them about 2 minutes each to properly boot up. Once the two machines are ready, we need to start the terminal on the AttackBox to experiment with `telnet`.

The TELNET (Teletype Network) protocol is a network protocol for remote terminal connection. In simpler words, `telnet`, a TELNET client, allows you to connect to and communicate with a remote system and issue text commands. Although initially it was used for remote administration, we can use `telnet` to connect to any server listening on a TCP port number.

On the target virtual machine, different services are running. We will experiment with three of them:

- Echo server: This server echoes everything you send it. By default, it listens on port 7.
- Daytime server: This server listens on port 13 by default and replies with the current day and time.
- Web (HTTP) server: This server listens on TCP port 80 by default and serves web pages.

Before continuing, we should mention that the echo and daytime servers are considered security risks and should not be run; however, we started them explicitly to demonstrate communication with the server using `telnet`. In the terminal below, we connect to the target VM at the echo server’s TCP port number 7. To close the connection, press the `CTRL` + `]` keys simultaneously.

Terminal

```shell-session
user@TryHackMe$ telnet MACHINE_IP 7
telnet MACHINE_IP 7
Trying MACHINE_IP...
Connected to MACHINE_IP.
Escape character is '^]'.
Hi
Hi
How are you?
How are you?
Bye
Bye
^]

telnet> quit
Connection closed.
```

In the terminal below, we use `telnet` to connect to the daytime server listening at port 13. We noticed that the connection closes once the current date and time are returned.

Terminal

```shell-session
user@TryHackMe$ telnet MACHINE_IP 13
Trying MACHINE_IP...
Connected to MACHINE_IP.
Escape character is '^]'.
Thu Jun 20 12:36:32 PM UTC 2024
Connection closed by foreign host.
```

Finally, let’s request a web page using `telnet`. After connecting to port 80, you need to issue the command `GET / HTTP/1.1` and identify the host where anything goes, such as `Host: telnet.thm`. Next, you need to press `Enter` twice so your last input line is a blank line. The output below shows the exchange. (The page has been redacted.)

**Note**: You may have to press `Enter` after sending the information in case you don’t get a response.

Terminal

```shell-session
user@TryHackMe$ telnet MACHINE_IP 80
Trying MACHINE_IP...
Connected to MACHINE_IP.
Escape character is '^]'.
GET / HTTP/1.1
Host: telnet.thm

HTTP/1.1 200 OK
Content-Type: text/html
[...]

Connection closed by foreign host.
```

