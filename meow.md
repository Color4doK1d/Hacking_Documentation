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

## Final Thoughts

I have realised in my nascent cybersecurity studies that I've been simply passively absorbing information, but lacked any of confidence in what I was learning once I closed my laptop lid for the day. I decided to take a step back and reconsider my approach. I'd been coding on my new laptop recently, teaching myself bash scripting by writing new commands for Linux Terminal to make navigating my Linux Mint OS easier, as well as doing silly things like triggering scripted text chains, and I was conscious that I seemed to be learning a lot about programming just by setting myself a small task, and figuring it out as I go. I used search engines and AI tools to assist me when I hit a brick wall but I did not rely on them; I made sure I understood the logical function I was trying to achieve before asking for the missing language or syntax that would help me achieve it.

My working method therefore is to ensure I fully understand the logical next step in what I am attempting to do, and if what I lack is simply the right command to execute that step, then I look it up. This way I am not outsourcing my thinking but simply arming myself with the tools to create the effect I already know I need.

This is the approach I've elected to now take with cybersecurity. I know from my day job as with privately practicing coding that I learn best by doing, and I was neglecting this insight in how I'd approached cybersecurity to date. I have covered enough of the first principles already through lessons on TryHackMe to have an understanding of the fundamentals, so I decided to take my hands-on approach into an attack box for the first time.

What surprised me most was how confident I felt in understanding what I had to do. Without any guidance whatsoever on this box I knew, in order:

- To run an nmap scan against the target IP
- To connect to Port 23 with the command telnet
- To test the login gate with the "root" username
- Thereafter, I am already more than comfortable navigating a Linux Terminal, so I felt like I had the run of the place

This was significantly better than I thought I was going to do, and it's proven to me the efficacy of my hands on approach and inspired me to keep cracking on with these boxes and learning as I go.

I thoroughly look forwards to the experience.
