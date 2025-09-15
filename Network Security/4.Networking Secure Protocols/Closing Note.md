In this room, we covered three main approaches to secure network traffic.

The first approach is to use TLS, which provides a convenient way to secure many protocols, such as HTTP, SMTP, and POP3. Protocols secured with TLS usually get an S, for _Secure_, added to their names, such as HTTPS, SMTPS, and POP3S.

The second approach to secure network traffic is to use SSH. Although SSH is mainly used for remote access, it can also transfer files securely and establish secure tunnels. Creating an SSH tunnel is a solid choice if you want to pass the traffic of a plaintext protocol, such as VNC.

The last approach we covered to secure network traffic is using VPN connections. A VPN connection is usually the perfect option for connecting two company branches.

We will finish this room with a hands-on challenge.

## Challenge

Press the **Start Machine** button below.

Start Machine

The machine will start in Split-Screen view. If it is not visible, use the blue **Show Split View** button at the top of the page.

We have set the browser to log the session’s TLS keys so we can take a closer look at the traffic using Wireshark. This logging was achieved by adding an extra option to the browser shortcut. Executing `chromium --ssl-key-log-file=~/ssl-key.log` dumps the TLS keys to the `ssl-key.log` file.

The packet capture file is called `randy-chromium.pcapng` and is saved in the `Documents` folder. When you open the packet capture file in Wireshark, you can configure Wireshark to use the `ssl-key.log` file so that all the TLS traffic gets decrypted. You can see the five steps to achieve this in the two screenshots below.

First, after right-clicking anywhere, choose “Protocol Preferences.” From the submenu, select “Transport Layer Security.” Thirdly, click on “Open Transport Layer Security preferences.”

![Click on Protocol Preferences, then click on Transport Layer Security, and finally click on Open Transport Layer Security preferences.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1726165322572.png)  

Clicking “Open Transport Layer Security preferences” will show a dialog box. You must click the “Browse” button marked with four to locate the `ssl-key.log`. You can find it in the `Documents` directory. Finally, click OK, and Wireshark will show all the TLS decrypted. One of these packets contains login credentials.

![Click on Browse, then select the ssl-key.log file, and finally click OK.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1726165340490.png)