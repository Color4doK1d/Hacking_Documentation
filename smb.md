## Service Analysis - SMB (Port 445)
<em>Section Added 2026-04-26</em>

Server Message Block (SMB) is a network file-sharing protocol used primarily by Windows systems to provide shared access to files, directories, printers, and other resources over a network.

SMB allows a client to connect to a server and interact with shared resources as if they were local.

SMB is deeply integrated into Windows environments, particularly in domain networks.

### Why SMB Matters

SMB is extremely common in internal networks but highly sensitive when exposed.

Its presence can indicate:

- Windows-based systems or infrastructure
- File sharing or domain services
- Potential access to internal data or credentials

Its exposure can reveal:

- Usernames
- File structure
- Sensitive documents
- Pathways to lateral movement

### Common Misconfigurations & Vulnerabilities

- Anonymous access enabled
- Weak or reused credentials
- Open or overly permissive shares
- Sensitive files exposed (passwords, configs, backups)
- SMBv1 enabled (associated with major vulnerabilities)
- Poor access control on critical directories
- Information leakage through share and user enumeration

### Attack Prioritisation

- If SMB open >> prioritise enumeration of shares and access permissions
- If anonymous access is possible >> immediately inspect available data
- If authentication is required >> attempt credential-based access
- If access is gained >> search for sensitive files and escalation paths
