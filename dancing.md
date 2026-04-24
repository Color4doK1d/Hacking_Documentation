# Dancing

**Room Link:** https://app.hackthebox.com/machines/Dancing?sort_by=created_at&sort_type=desc |
**Difficulty:** Very Easy |
**Date Completed:** 2026-04-23

## Objective
Capture the flag on the target machine

## Tools Employed
- nmap
- smbclient

## Walkthrough
### Reconnaissance & Enumeration

- Ran an nmap scan on the target machine

> <img width="949" height="547" alt="nmap" src="https://github.com/user-attachments/assets/d85970d4-fb5f-4a72-840d-db71cd27b56b" />
> <em>Figure 1: Nmap Scan Results</em>

- A laundry list of open ports emerges from the scan, but Port 445 - reserved for SMB services - draws my eye. Misconfigured SMB services can expose shared files on the network as well as network controls. Conscious of the nature of these early HTB boxes I anticipate that this (the first Windows target) is attempting to teach something about Microsoft Windows services. That may not be the most live-fire thought process, but I'm making a note of it anyway: if the objective here is to treat this like a live target and exploit it accordingly then the fact that it is configured as a practice box to teach specific lessons is exploitable intelligence.

- I connect to the SMB service using the command smbclient.

### Exploit

> <img width="2433" height="951" alt="smb" src="https://github.com/user-attachments/assets/57a4e19a-382d-4fdc-a9c7-5ca1a6c239f0" />
> <em>Figure 2: Commands used to figure out how to connect to Port 445 using smbclient</em>

- This is my first time interfacing with an SMB service so there is a lot of fumbling around once I've identified the correct program to use to interface with Port 445.

- I made ample use of smbclient's documentation to help me understand how to deploy it, but for my screenshot ran the commands again in order to take a cleaner capture.

- (The cleaner screenshot also omits my probing of the first three workshares, all of which I found to be password protected).

- Once I tried the WorkShares group, however, I attempted to bypass it by not submitting a password and - sure enough - gained access to the system.

> <img width="1164" height="1009" alt="session" src="https://github.com/user-attachments/assets/0617cc81-4f97-4697-8f6a-278692576b3f" />
> <em>Figure 3: My SMB session</em>

- I was able to use the service's internal help function to help me navigate. From there locating the flag was trivial.

## Flags

> <img width="1173" height="188" alt="flag" src="https://github.com/user-attachments/assets/c40d8258-6834-47ac-96a8-aa5350938016" />
> <em>Figure 4: My third legitimate flag capture</em>

## Summary

This was the first of HTB's boxes that showcased numerous ports. When redoing this hack over for the purposes of writing this report I took some time to probe the other services, but found them to be password protected. This challenge is designed to draw the student towards Port 445 as a potential vulnerability to exploit.

Once I had identified the workgroups running on the SMB service, most of my time was taken with trying to figure out the syntax for smbclient on the fly. Once I'd gained access navigation was somewhat easier, as the service mostly adopts Linux commands for navigation, which I am much more comfortable with.

## Final Thoughts

Again, this early on in HTB's boxes they seem to be trying to build in repetition and muscle memory, rather than serious exploitation. Nonetheless the different services exposed by each challenge is forcing me to build a program/command bible, so that when faced with an open port I have documentation on how to interface with it. This is proving invaluable and this knowledge is only being copperfastened by the writing of these reports. I tend to run each hack twice before finalising a report, and the extra repetition is igniting my self-confidence faster than I dared anticipate at the outset.

It's safe to say I really enjoy this routine and can't wait to advance to the next Tier - but, thorough reporting of the Tier 0 boxes will take priority for now.
