---
dg-publish:
---
---
![](../_attachments/Pasted%20image%2020250619215037.png)
connected to kali via openvpn

![](../_attachments/Pasted%20image%2020250619215120.png)

![](../_attachments/Pasted%20image%2020250619215158.png)
![](../_attachments/Pasted%20image%2020250619215214.png)
![](../_attachments/Pasted%20image%2020250619215227.png)

this reveals:

| Port     | Service          | Purpose                                                   |
| -------- | ---------------- | --------------------------------------------------------- |
| **53**   | domain           | DNS — often used by AD for internal name resolution.      |
| **80**   | http             | Web service — may host admin panels or web interfaces.    |
| **88**   | kerberos-sec     | Kerberos authentication — core part of AD.                |
| **135**  | msrpc            | Microsoft RPC — used for various Windows services.        |
| **139**  | netbios-ssn      | NetBIOS — legacy file/printer sharing.                    |
| **389**  | ldap             | LDAP — directory services, typically AD-related.          |
| **445**  | microsoft-ds     | SMB — file sharing, often exploitable.                    |
| **464**  | kpasswd5         | Kerberos password change service.                         |
| **593**  | http-rpc-epmap   | Remote procedure call over HTTP.                          |
| **636**  | ldapssl          | LDAP over SSL/TLS.                                        |
| **3268** | globalcatLDAP    | Global Catalog service — used for forest-wide AD queries. |
| **3269** | globalcatLDAPssl | Secure Global Catalog.                                    |

