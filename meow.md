# Meow - First Hack the Box

**Room Link:** https://app.hackthebox.com/machines/Meow?sort_by=created_at&sort_type=desc |
**Difficulty:** Very Easy |
**Date Completed:** 2026-04-22

## Objective
Penetrate the target system and capture the flag.

## Tools Employed
- Nmap
- Telnet

## Walkthrough
### Reconnaissance & Enumeration

- Ran an nmap scan against target IP address

> <img width="1375" height="311" alt="NmapCapture" src="https://github.com/user-attachments/assets/35678888-032d-4ffd-9769-eea71c53860d" />
> <em>Figure 1: Nmap Scan Output</em>

- Identified Port 23 (Telnet) as open. This is more or less expected, given the simplicity of the exposed surface and the absence of additional open ports. While it's the only open port on this target machine, it stands out anyway for being notoriously vulnerable if poorly configured, especially as it is an older service. This makes it a high-priority target for probing.

### Exploit

- Connected to Port 23 on target machine with telnet command

- User credentials were requested; attempted several obvious username/password combinations before I took a step back and reconsidered. Given the limited attack surface and absence of alternative entry points, I probed for misconfiguration by attempting root as a username.

- Used "root" login and was granted immediate root access without any follow-up prompt for a password.

### Privilege Escalation

- The ability to authenticate directly as root without a password results in full system compromise. No further privilege escalation was required, as the highest level of access was obtained immediately upon login.

> <img width="849" height="928" alt="Telnet" src="https://github.com/user-attachments/assets/89b5db30-bb4f-4603-90a0-ff6e84bdc2c3" />
> <em>Figure 2: Gained access to target machine through Port 23 (Telnet) with root privileges</em>

## Flags

> <img width="675" height="134" alt="Flag" src="https://github.com/user-attachments/assets/8dec75fd-2627-495d-ad41-cb8937e44842" />
> <em>Figure 3: First Flag Captured!</em>

## Summary

This is HacktheBox's easiest machine in its Starting Point pathway. This provides a gauntlet of eight target machines, each with lax security features, designed to teach students rudimentary enumeration, how to identify services, and knowing which programs and commands to use to interface with those services when discovered. It also encourages an understanding of admin/root username combinations and weak password practices for both, as demonstrated in this report.

Thus, this box does not offer a challenge so much as a chance to get reps in for beginners to cybersecurity and build their muscle memory in executing commands to connect to services.

In that spirit, I was able to quickly identify Port 23 as running Telnet, and interface with it using telnet from my Linux VM. Attempting to log in with root as a username revealed that there was no password required, giving me full root privileges on the target machine. From there, locating and reading the flag was trivial, but I owe that at least to my own practice over the past few months with Linux Terminal on my laptop. It saved me some time having to learn on the fly from within the target box.

## Service Analysis - Telnet (Port 23)
<em>Section Added 2026-04-26</em>

Telnet is a plaintext remote access protocol that allows users to log into and control systems over TCP, typically on Port 23.

Telnet establishes a direct TCP connection between a client and a remote system, providing an interactive command line interface.

> <img width="1118" height="497" alt="image" src="https://github.com/user-attachments/assets/b7e032a1-5fd7-40c0-b1cc-6f94d947b222" />
> <em>Figure 4: How Port 23 Works</em>

All communication, *including login credentials and commands*, is transmitted in plaintext with no encryption or integrity protection.

### Why Telnet Matters

Telnet is largely obsolete and has been replaced by secure alternatives such as SSH.

Its presence on a modern system usually indicates:

- Legacy infrastructure
- Poor security practice
- Intentional exposure in training environments such as this one

As it lacks encryptian, any intercepted traffic can reveal credentials and session data.

### Common Misconfigurations & Vulnerabilities

- Transmission of credentials in plaintext (susceptible to interception)
- Weak or default credentials
- No account lockout or rat limiting
- Unrestricted remote shell access after authentication
- Exposure to untrusted or public networks

### Attack Prioritisation

- If Telnet exposed >> Prioritise investigation due to inherent insecurity
- If auth. required >> focus on credential-based access (potentially weak)
- If access obtained >> likely provides immediate command execution

## Final Thoughts

Switching into tackling HacktheBox practicals marks a shift in how I have approached by cybersecurity studies to date, from passive learning to learning through active problem-solving. I know from my day job as well as my private programming studies that I learn best through being hands-on, and so I decided that tackling target machines head on offered the best path to building confidence and muscle memory. As with my programming studies, where I have learned the most by setting myself small tasks and attempting to figure out what's required for them as I go, I primarily use outside assistance when I lack the command language or syntax to execute the next step I have already identified.

What surprised me most was how confident I felt in understanding what I had to do. Without any guidance whatsoever on this box I knew, in order:

- To run an nmap scan against the target IP
- To connect to Port 23 with the command telnet
- To test the login gate with the "root" username
- Thereafter, I am already more than comfortable navigating a Linux Terminal, so I felt like I had the run of the place

This was significantly better than I thought I was going to do, and it's proven to me the efficacy of my hands on approach and inspired me to keep cracking on with these boxes and learning as I go.

I thoroughly look forwards to the experience.
