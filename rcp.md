## Service Analysis - MS RPC (Port 135)
<em>Section Added 2026-04-26</em>

Microsoft Remote Procedure Call (RPC) is a protocol used by Windows systems to allow programs to request services from other systems or processes over a network, typically via Port 135.

MS RPC operates through an endpoint mapper on Port 135, which acts like a directory service.

#### Process:

- Client connets to Port 135
- Endpoint Mapper provides information about available RPC services and their ports
- The client then connects to those specific services on dynamic ports

RPC underpins many core Windows functions, including authentication, service control, and system mamagement.

### Why RPC Matters

MS RPC is normal in Windows environments, especially internally.

However, its exposure can:

- Reveal detailed information about the system
- Enable enumeration of users, services, and network structure
- Indicate a broader Windows attack surface

NOTE that on its own, RPC is rarely the direct entry point. It nonetheless serves as a useful roadmap to understanding the target system environment.

### Common Misconfigurations & Vulnerabilities

- Excessive information disclosure via enumeration
- Weak access controls allowing unauthenticated queries
- Exposure to untrusted networks
- Poorly secured dependent services (e.g. SMB, WinRM)
- Legacy or unpatched RPC-related vulnerabilities

RPC is often less about direct exploitation and mmore about:

- Gathering intelligence
- Identifying valid users
- Mapping services and dependencies

### Attack Prioritisation

- If RPC is open - prioritise enumeration, not exploitation
- Use to identify usernames; available services; system roles
- Use gathered information to inform attacks on other services

RPC is a **supporting actor**, not the primary point of attack, but it can dramatically improve the effectiveness of other attacks.
