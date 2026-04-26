## Service Analysis - FTP (Port 21)
<em>Section Added 2026-04-26</em>

File Transfer Protocol (FTP) is a standard protocol used to transfer files between a client and a server over a network, typically operating on Port 21.

FTP uses two separate channels:
- Control channel (Port 21) for handling commands and authentication
- Data channel (dynamic ports) for handling file transfer and directory listings

FTP can operate in:
- Active mode: Server conncets back to the client
- Passive mode: Client initiates both connections (more common today)

### Why FTP Matters

FTP is widely utilised but often poorly secure. Note that like Telnet, it transmits data and credentials in plaintext.

Its presence can indicate:

- File sharing functionality
- Backup storage or web content hosting
- Legacy systems or weak security posture

Because it frequently exposes system files directly, it can revela sensitive data or provide a path to further compromise.

### Common Misconfigurations & Vulnerabilities

- Anonymous login enabled (anonymous:anonyomous or similar)
- Weak or reused credentials
- Sensitive files exposed
- Write permissions allowing file upload
- Plaintext transmission of credentials (sniffing risk)
- Misconfigured directory permissions

### Attack Prioritisation
- If FTP open >> check for anonymous access immediately
- If login required >> attempt credential-based access
- If access gained >> enumerate directories and files for sensitive data
- If upload allowed >> assess potential for file-based exploitation
