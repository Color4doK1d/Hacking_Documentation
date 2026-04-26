# Synced

**Room Link:** https://app.hackthebox.com/machines/Synced?sort_by=created_at&sort_type=desc |
**Difficulty:** Very Easy |
**Date Completed:** 2026-04-23

## Objective
Capture the flag

## Tools Employed
- nmap
- rsync

## Walkthrough
### Reconnaissance & Enumeration

- Enumerated target attack surface with an nmap scan

> <img width="928" height="281" alt="nmap" src="https://github.com/user-attachments/assets/67f93b44-a19b-459d-af3b-ad19b3e59d0a" />
> <em>Figure 1: Nmap scan Output</em>

- With only one port exposed I took this to be my attack vector. I had to look up how to connect to an rsync service in order to learn the command, and then it took some trial-and-error to work out the exact syntax to connect and navigate to the port.

### Exploit

- Connected to the target system with the rsync command. Full access was granted without the need for authentication

## Flags

> <img width="1149" height="429" alt="flag" src="https://github.com/user-attachments/assets/a74e99f0-52dc-4b55-b7d7-ad0d41ef8903" />
> <em>Figure 2: My eighth legitmate flag capture, and the final one for Tier 0 boxes</em>

## Summary

Enumeration revealed the sole open port on the target system, and no authentication was required to breach. This made for a simple one-step hack.

## Service Analysis - Rsync (Port 873)
<em>See **Final Thoughts** section below for rationale on Service Analyses</em>

Rsync is a file synchronisation protocol and tool used to efficiently transfer and mirror files between systems, typically operating over Port 873.

Rsync synchronises files by transferring only the differences between source and destination, making it highlt efficient.

When running as a daemon, access control depends on configuration, which may or may not require authentication.

### Why Rsync Matters

Rsync is commonly used for:

- Backups
- File replication
- System synchronisation

If exposed externally, it may indicate:

- Backup data accessible over the network
- Misconfigured file-sharing services
- Weak or absent access controls

Because it often handles entire directory structures, exposure can lead to:

- Large-scale data disclosure
- Access to sensitive backups and configurations

### Common Misconfigurations & Vulnerabilities

- Anonymous access to modules
- No auth required
- Overly permissive module configurations
- Exposure of sensitive directories (backups, configs, user data)
- Write permissions enabled (potential for file upload)
- Service exposed to public networks

Rsync is particularly risky when exposed because:

- It can expose entire file systems or backup sets
- Backups often contain sensitive or forgotten data

### Attack Prioritisation

- If Rsync open >> prioritise enumeration of available modules
- If modules are accessible >> inspect contents for sensitive data
- If auth not required >> treat as immediate data exposure
- If write access permitted >> assess potential for file-based exploitation

Rsync is a **high value target** because:

- It often exposes large volumes of data
- It may contain backups with credentials or system information
- It provides structured access to file systems

## Final Thoughts

The final box in HacktheBox's Tier 0 is a perfect summation of the approach taken by this Tier. It is not so much testing ability to breach defended systems as it is building up muscle memory for enumeration; recognising services; connecting with and navigating services. This is that concept stripped down to the bare essentials.


<em>One Last Personal Note:</em>

In spite of the above, I think I will be doing myself a better favour if I go back over each of these reports and study each service in depth a little more. I believe I have understood the learning objectives at this tier and that I have hit each one, but I could better equip myself for what's to come by understanding each service in this Tier better. In future, rather than seeing an open port and thinking "I know which command to use", I would like to have the confidence to instead think "I understand how this service works and what its vulnerabilities are."

Therefore, before I embark upon Tier 1, I am going to update the format of these reports to include a section on the service being probed in each hack, which will aim to accomplish the following:

- An understanding of what the service is and how it works.
- An understanding of how the tools used to connect with that service do so.
- An understanding of the service's common misconfigurations and vulnerabilities.
- And as such, an understanding of how to prioritise that service for attack during enumeration.
