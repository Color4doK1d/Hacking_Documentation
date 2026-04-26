# Fawn

**Room Link:** https://app.hackthebox.com/machines/Fawn?sort_by=created_at&sort_type=desc |
**Difficulty:** Very Easy |
**Date Completed:** 2026-04-22

## Objective
Capture the flag on the target machine

## Tools Employed
- nmap
- ftp

## Walkthrough
### Reconnaissance & Enumeration

- As usual, ran an nmap scan against target machine's IP address

> <img width="1303" height="300" alt="nmap" src="https://github.com/user-attachments/assets/38078209-6ad2-49f9-8821-5e2fe794d2b9" />
> <em>Figure 1: Nmap Scan Output</em>

- Detected that Port 21 (File Transfer Protocol) was open. FTP allows for anonymous access, which combined with poor network configuration could reveal a catastrophic vulnerability.

### Exploit

- With this in mind, I attempted connection to the target machine's FTP service using "anonymous" as my username. Sure enough, it granted me access without requiring a password.

- The target flag was easily available once a connection was established; this represents less a vulnerability and more simply "Connect to a public access point and download a public file". As this was enough to satisfy my objective, I had no cause to pursue privilege escalation on the target.

> <img width="1898" height="601" alt="ftp" src="https://github.com/user-attachments/assets/398c9158-b5e9-43b1-9e33-01555bcd65ec" />
> <em>Figure 2: Access to Port 21 (FTP) and my actions while inside</em>

## Flags

> <img width="1163" height="184" alt="flag" src="https://github.com/user-attachments/assets/d2d404a7-01cb-41e7-b0f6-daa2bb0f0c23" />
> <em>Figure 3: My second ever legitimately captured flag</em>


## Summary

My initial enumeration revealed an open FTP port (21) on the target machine. From here it was a trivial maatter to connect to the port leveraging ftp's anonymous access protocols in order to acquire the flag that represents the box's objective.

It's worth commenting that this required no privilege escalation and no real exploitative mindset beyond a rudimentary understanding of how FTP works. As outlined in my report for the "Meow" box, this is in keeping with what I feel HacktheBox is attempting to teach on these Tier 0 boxes. Namely, a familiarity with various services and repetition of the basic steps in targeting a machine.

## Service Analysis - FTP (Port 21)
<em>Section Added 2026-04-26</em>

File Transfer Protocol (FTP) is a standard protocol used to transfer files between a client and a server over a network, typically operating on Port 21.

> <img width="1200" height="675" alt="image" src="https://github.com/user-attachments/assets/e9a57036-ba04-4a3f-956a-73f71a3a7014" />
> <em>Figure 4: How Port 21 Works</em>

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

## Final Thoughts

This was mostly an exercise in muscle-memory and understanding what I was looking at. I'm glad of the opportunity to repeat these basic one-step penetrations to exercise that muscle memory, and to take notes (which in turn spawn these reports) which deepen my understanding of the services I am connecting to.
