# Preignition

**Room Link:** https://app.hackthebox.com/machines/Preignition?sort_by=created_at&sort_type=desc |
**Difficulty:** Very Easy |
**Date Completed:** 2026-04-23

## Objective
Capture the flag on the target machine

## Tools Employed
- nmap
- wget
- curl
- dirb

## Walkthrough
### Reconnaissance & Enumeration

- Ran an nmap scan on target machine

> <img width="951" height="275" alt="nmap" src="https://github.com/user-attachments/assets/307e78ab-5d6f-49d6-a36a-4e6ee54c99a0" />
> <em>Figure 1: Nmap scan output</em>

- Port 80 usually implies a web server, so I decided to connect to confirm.

> <img width="2523" height="1052" alt="wget" src="https://github.com/user-attachments/assets/9850d2a8-2b27-42b0-a180-4aabeb04b9a6" />
> <em>Figure 2: Wget Connection to Port</em>

- The HTML document transferred to my machine confirms that this is indeed a live web server.

- I can start a more targeted enumeration of this web service itself by running dirb against it.

> <img width="811" height="549" alt="dirb" src="https://github.com/user-attachments/assets/02fe59b1-b610-4a4a-8410-505d74a467be" />
> <em>Figure 3: Results of the dirb scan</em>

- The dirb scan turned up the subdomain "admin.php", which hints that this web service may be misconfigured, to my advantage.

### Exploit

- I use curl to reconnect to the web server using the uncovered subdomain.

> <img width="1429" height="813" alt="curl" src="https://github.com/user-attachments/assets/6f496de9-2d8d-4c71-9f3d-220a61669c86" />
> <em>Figure 4: Port 80 HTTP Session</em>

- The HTML for the /admin.php subdomain reveals that I'm looking at a login screen, requesting a username and password.

## Flags

- I had to take a moment to check curl's documentation both in-terminal and online in order to understand how to POST to a webserver using the curl command.

- Once that was established I began to systematically work through obvious username/password combinations to probe for misconfiguration.

> <img width="1798" height="821" alt="flag" src="https://github.com/user-attachments/assets/3a9569ac-bc83-4cac-a628-58f218258f3a" />
> <em>Figure 5: My flag capture. Terminal commands and output truncated for legibility.</em>

- In the end, the system granted me access - and my sixth legitimate flag capture - with the login credentials "admin | admin".

## Summary

This box was designed to train the user on probing web servers for weaknesses. A central pillar in any attack on a web service such as this is DNS brute-forcing, accomplished through commands like dirb or gobuster. This adds a further step in enumerating the target attack surface, but if the target system is misconfigured it means exposing a critical vulnerability. In this case, not only was an admin login subdomain exposed online, but the login credentials themselves were kept in their default - and so easily brute-forced - values.

## Service Analysis - HTTP (Port 80)
*Section Added: 2026-04-26*

Hypertext Transfer Protocol (HTTP) is a stateless application-layer protocol used for transmitting web content between clients (browsers) and servers, typically over Port 80.

> <img width="1060" height="592" alt="image" src="https://github.com/user-attachments/assets/a906b354-77b8-45f3-8a67-32eef720a550" />
> <em>Figure 6: How Port 80 Works</em>

HTTP follows a request-response model:

- A client sends a request (e.g. GET, POST) to the server
- The server processes it and returns a response (HTML, JSON, files, etc.)

Users interact through browsers, but under the surface it's structured text flying back and forth.

### Why HTTP Matters

As the backbone of the internet HTTP is one of the most common and important services.

Its presence indicates:

- A web application or site is hosted
- A primary user-facing interface exists
- A large and complex attack surface is likely present

Unlike many services, HTTP is rarely the system itself, but a gateway into deeper layers including:

- Backend logic
- Databases
- Authentication Systems

### Common Misconfigurations & Vulnerabilities

- Directory listing enabled (exposed files and structure)
- Default or hidden pages (admin panels, backups, test endpoints)
- Weak auth mechanisms
- Input handlings vulnerabilities (e.g. injection flaws)
- Misconfigured file permissions
- Outdatd server software or frameworks
- Exposure of sensitive files (configs, credentials, source code)

HTTP is especially prone to:

- Logic flaws
- Poort input validation
- Accidental exposure of internal functionality

### Attack Prioritisation

- If Port 80 open >> prioritise enumeration of web application
- Identify: pages & endpoints; tech in use; auth mechanisms

HTTP is a **primary entry point** becaise:

- It is designed to be interacted with
- It often exposes complex functionality
- Small mistakes can lead to full compromise

## Final Thoughts

As silly as it sounds I chewed through this box because I have encountered exactly this set-up when playing hacking videogames. Identify a target website, bruteforce subdomains to reveal vulnerabilities, exploit from there. I actually found it quite satisfying to realise I already knew the attack pattern here, because I'd engaged it in endlessly in games like NITE Team 4 on Steam.

That is, ultimately, where I think my enjoyment of this is stemming from: my gamer's brain recognises the patterns and the progression that HacktheBox in particular is built upon. Namely:

- Meet new challenge
- Discover tool for dealing with challenge
- Overcome challenge
- Repeat pattern

This is fundamentally how gameplay progression loops are designed and it is exactly how HTB has treated their box progression.
