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
