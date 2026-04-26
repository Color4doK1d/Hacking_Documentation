## Service Analysis - Telnet (Port 23)
<em>Section Added 2026-04-26</em>

Telnet is a plaintext remote access protocol that allows users to log into and control systems over TCP, typically on Port 23.

Telnet establishes a direct TCP connection between a client and a remote system, providing an interactive command line interface.

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
