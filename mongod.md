# Mongod

**Room Link:** https://app.hackthebox.com/machines/Mongod?sort_by=created_at&sort_type=desc |
**Difficulty:** Very Easy |
**Date Completed:** 2026-04-24

## Objective
Capture the flag on the target machine

## Tools Employed
- nmap
- mongosh

## Walkthrough
### Reconnaissance & Enumeration

- I began my enumeration of the target attack surface as ever by running an nmap scan

> <img width="961" height="322" alt="nmap" src="https://github.com/user-attachments/assets/5c0402c0-0266-41ce-8b82-8424827230e5" />
> <em>Figure 1: Nmap Scan Output</em>

- Nmap revealed two ports open; an SSH service on Port 22 and a MongoDB service on Port 27017.

- I was utterly unfamiliar with Mongo as a service so at this point I took some time to look it up online. What I found led me to believe that older versions of MongoDB - and the version running on this system is certainly outdated - are infamously susceptible to exploitation. Older deployments notoriously lacked authentication and meant that exposed services, such as this one, were vulnerable to hostile actors. As a result I looked up the command I required to attempt a connection, to probe for exposed data.

> <img width="1608" height="182" alt="wrong version" src="https://github.com/user-attachments/assets/7892b550-3103-4e16-a91b-d88346fbdad0" />
> <em>Figure 2: Failed to connect to an older Mongo version</em>

- The target system's version of Mongo (3.6.8) was too old to interface with my VM's version of mongosh.

- This required another round of googling to understand exactly what I was dealing with and how to proceed, but I eventually elected on downgrading my VM's mongosh to a comensurate version with the version I was attempting access to.

> <img width="2518" height="602" alt="downgrade" src="https://github.com/user-attachments/assets/08402e36-68e6-4697-bf93-3da7e731cf7c" />
> <em>Figure 3: Downgrading mongosh</em>

- With a compatible version now installed, I re-attempted my connection to Port 27017 on the target machine.

### Exploit

> <img width="1471" height="664" alt="mongo" src="https://github.com/user-attachments/assets/3e6e4c31-b9eb-4ad2-aec9-5f3ccc1c1438" />
> <em>Figure 4: Mongo Session</em>

- Access to the target system was achieved without credentials due to poor configuration of the outdated MongoDB version running on Port 27017.

- I took a moment to familiarise myself with Mongo's commands through its internal documentation and online.

> <img width="1671" height="976" alt="navigation" src="https://github.com/user-attachments/assets/53a326b7-c0cc-4809-8fad-dbad29174ea1" />
> <em>Figure 5: Navigating Mongo with Documentation</em>

- The lack of proper configuration left the "sensitive_information" database exposed and vulnerable to reading.

## Flags

> <img width="469" height="456" alt="flag" src="https://github.com/user-attachments/assets/6d25622f-ad73-4422-b716-025d642a47df" />
> <em>Figure 6: Claiming my seventh flag</em>

## Summary

The biggest challenge here was neither determining the attack vector, not even in figuring out on the fly how to navigate an unfamiliar command line interface such as Mongo. It proved to be having to reconfigure my tools to interface with an out of date, but thus vulnerable, service version. Once this had been achieved I was able to take advantage of a lax security environment to gain unfettered access to the target system and locate the flag.

## Service Analysis - MongoDB (Port 27017)

MongoDB is a NoSQL database that stores data as flexible, JSON-like documents within collections. It typically runs on Port 27017.

MongoDB organises data into:

- Databases - Contains collections
- Collections - Contain documents
- Documents - Key-value data structures (similar to JSON)

Unlike relational databases, MongoDB does not enforce strict schemas, allowing flexible data storage.

Historically, MongoDB often assumed it was running in a trusted environment and did not enforce authentication by default, as in this report's documented walkthrough.

### Why MongoDB Matters

MongoDB is intended for internal use, not public exposure.

If accessible externally, it often indicates:

- Misconfiguration
- Lack of authentication
- Poor network isolation

Because it directly stores application data, exposure can lead to:

- Full data disclosure
- Data manipulation
- Credential harvesting

### Common Misconfigurations & Vulnerabilities

- Unauthenticated access
- Database bound to all interfaces
- Exposure to public networks
- Weak or absent access controls
- Sensitive data stored in plaintext within collections
- Outdated versions with known security issues

MongoDB is particularly risky when exposed because:

- Access often grants full visibility into stored data
- There is minimal separation between user and database logic

### Attack Prioritisation

- If MongoDB exposed >> prioritise immediate access attempts
- Check for: unauth'd access; accessible databases and collections
- If access available >> enumerate data for sensitive information

MongoDB is a **high-value target** because:

- It often lacks authentication in misconfigured environments
- It provides direct access to application data
- It can reveal credentials, tokens and internal logic

## Final Thoughts

I probably had to do the most research of all the boxes so far on this one, and it's gradually moulding my approach both to learning on the go and to how I frame these reports. I'm starting to understand that these reports hold the most value for myself (and presumably others) the more I use them to showcase reasoning and deduction, beyond just the pure investigative process. I'll keep that in mind moving forwards.
