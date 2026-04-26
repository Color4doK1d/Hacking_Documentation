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
