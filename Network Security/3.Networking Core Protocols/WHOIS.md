In the previous task, we covered how a domain name is resolved into an IP address. However, for this to happen, someone needs to have the authority to set the A, AAAA, and MX records, among other DNS records for the domain. Whoever registers a domain name is granted this power. Therefore, if you register example.com, you can set any valid DNS records for example.com.

You can register any available domain name for one or more years. You need to pay the annual fee, and you are required to provide [accurate contact information](https://www.icann.org/resources/pages/whois-data-accuracy-2017-06-20-en) as the registrant. This information is part of the data available via WHOIS records and is available publicly. (Although written in uppercase, WHOIS is not an acronym; it is pronounced _who is_.) However, don’t worry if you want to register a domain without revealing your contact information publicly; you can use one of the privacy services that hide all your information from the WHOIS records.

You can look up the WHOIS records of any registered domain name using one of the online services or via the command-line tool `whois`, available on Linux systems, among others. As expected, a WHOIS record provides information about the entity that registered a domain name, including name, phone number, email, and address. In the screenshot shown below, you can see when the record was first created and when it was last updated. Moreover, you can find the registrant’s name, address, phone, and email.

![Example WHOIS record](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1719849535407.png)  

In the terminal output below, we have used the `whois` command to look up a domain whose WHOIS record is protected by privacy protection.

Terminal

```shell-session
user@TryHackMe$ whois [REDACTED].com
[...]
Domain Name: [REDACTED].COM
Registry Domain ID: [REDACTED]
Registrar WHOIS Server: whois.godaddy.com
Registrar URL: https://www.godaddy.com
Updated Date: 2017-07-05T16:02:43Z
Creation Date: 1993-04-02T00:00:00Z
Registrar Registration Expiration Date: 2026-10-20T14:56:17Z
Registrar: GoDaddy.com, LLC
Registrar IANA ID: 146
Registrar Abuse Contact Email: abuse@godaddy.com
Registrar Abuse Contact Phone: +1.4806242505
[...]
Registrant Name: Registration Private
Registrant Organization: Domains By Proxy, LLC
Registrant Street: DomainsByProxy.com
[...]
```