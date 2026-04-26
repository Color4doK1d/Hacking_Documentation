# Explosion

**Room Link:** https://app.hackthebox.com/machines/Explosion?sort_by=created_at&sort_type=desc |
**Difficulty:** Very Easy |
**Date Completed:** 2026-04-23

## Objective
Capture the flag on the target machine

## Tools Employed
- nmap
- rcpclient
- smbclient
- curl
- evil-winrm

## Walkthrough
### Reconnaissance & Enumeration

- Ran an nmap scan on target machine

> <img width="945" height="622" alt="nmap" src="https://github.com/user-attachments/assets/2d91906c-d960-43f0-87c5-5d7bb77a79d1" />
> <em>Figure 1: Nmap Scan</em>

- The number of open RPC ports revealed that Windows RPC services were active and accessible on the target.

| Port | Service |
|------|---------|
| 135  | MSRPC   |
| 445  | SMB     |
| 3389 | RDP     |
| 5985 | HTTP (WinRM) |
| 47001 | HTTP (WinRM) |

- I probed Port 135 hoping to further enumerate RPC services on the target machine and identify RPC endpoints.

> <img width="832" height="526" alt="rpc" src="https://github.com/user-attachments/assets/eab3e941-5687-4ceb-a671-f9fd379842e9" />
> <em>Figure 2: Connection Attempts with rpcclient</em>

- This only confirmed what I already took to be a given, that this system is operating within a Windows networking context.

- Without any obvious means of access I turned my attention to connecting wtih Port 445, as that has borne fruit for me previously (see my report "Dancer").

> <img width="890" height="654" alt="smb" src="https://github.com/user-attachments/assets/6b3595cf-d30d-42dd-ad3e-470d7e6cc317" />
> <em>Figure 3: Connection Attempts with smbclient</em>

- This, too, proved to be a dead end, as my usual attempts to take advantage of poor configuration met with resistance.

- With RCP and SMB probes yielding no results and precious little usable intel I turned my focus to the two HTTP ports. This was driven largely by my level of understanding and comfort with the programs at my disposal to date; I recognised HTTP services and knew how to test them, which I proceeded to do using curl.

> <img width="950" height="276" alt="curl" src="https://github.com/user-attachments/assets/a1a851d5-e49a-4f1d-b82f-9c8d04d8a061" />
> <em>Figure 4: Connection Attempts on HTTP Ports with curl</em>

- The feedback from curl led me to believe that the ports were not running a web service and instead employing HTTP as a medium for other protocols.

- At this point I took a moment to check online for the commmon usages of Ports 5958 and 47001.

- Port 5958 is the commonly employed by Windows Remote Management, and Port 47001 is commonly used by other Windows RM services. This chimes with what the rest of my enumeration has turned up.

### Exploit

- This required me to discover another tool in the penetration arsenal; evil-winrm. With this I could successfully connect to both ports and begin to test default login credentials, probing for misconfiguration, as I had done on the ports above.

> <img width="1391" height="680" alt="5985" src="https://github.com/user-attachments/assets/31c19b33-14f7-4d3d-8824-63ad7d224951" />
> <em>Figure 5: Connection Attempts on Port 5958 with evil-winrm</em>

- Passing the username "administrator" to Port 5958 granted me full, unfettered admin access to the machine in a Powershell terminal. As Powershell largely works off Linux Terminal commands it was trivial from there to navigate through the environment to capture the flag.

## Flags

> <img width="663" height="902" alt="flag" src="https://github.com/user-attachments/assets/98e9d324-924f-44bc-bc44-c1c185cc7444" />
> <em>Figure 6: The captured flag</em>

## Summary

This enumeration process required multiple attempts to get a lay of the land. In subsequent do-overs I tested each port in turn thoroughly to confirm that each port is password protected and not immediately accessible to the student. The box is designed to push the user into attempting access through the two HTTP ports running WinRM services with admin credentials.

## Service Analysis - WinRM (Ports 5985 - 5986)
<em>Section Added 2026-04-26</em>

Windows Remote Management (WinRM) is a Microsoft protocol that allows remote administration of Windows systems over HTTP (Port 5985) or HTTPS (Port 5986).

WinRM enables remote command execution and system management, typically via PowerShell.

It is the backbone of Powershell Remoting and is commonly used by administrators to manage systems at scale.

### Why WinRM Matters

WinRM is legitimate and common in Windows environments, especially in enterprise settings.

However, when exposed, it signals:

- Remote administration is enabled
- Authentication-based access is possible
- A stable, interactive shell may be available if credentials are obtained

Unlike services that require exploitation, WinRM often becomes valuable once valid credentials are known.

### Common Misconfigurations & Vulnerabilities

- Weak or reused credentials
- Exposure to untrusted or public networks
- Overly permissive access controls
- Lack of network restrictions on administrative interfaces
- Misconfigured authentication settings

Note that while WinRM is not inherently vulnerable, its security depends upon:

- Credential strength
- Access control
- Network exposure

### Attack Prioritisation

- If WinRM open >> note it as a high-priority post-credential target
- Prioritise obtaining valid credentials via other services (e.g. SMB, FTP)
- If credentials are availables >> attempt authenticated access for remote command execution

## Final Thoughts

As far as enumeration goes this represents the most hands-on box I've hacked so far. It relied on me recognising a system configuration from what services were running, something I admit I had to fumble around a little to get to grips with. This report will hopefully stand as a useful touchstone for me for future reference.
