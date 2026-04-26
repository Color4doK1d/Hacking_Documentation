## Service Analysis - Redis (Port 6379)
<em>Section Added 2026-04-26</em>

Redis is an in-memory key-value data store used for caching, message brokering, and fast data retrieval, typically running on Port 6379.

Redis stores data in memory as key-value pairs, allowing extremely fast read and write operations.

Clients connect to the Redis server and issue commands via a simple text-based interface.

By default, Redis historically trusted the environment it ran in and often did not enforce authentication.

### Why Redis Matters

Redis is typically intended for internal use only.

If exposed externally, it often indicates:

- Misconfiguration
- Lack of network segmentation
- Absense of authentication controls

Expore of Redis can lead to:

- Full data access
- Data manipulation
- In some cases, system-level compromise

### Common Misconfigurations & Vulnerabilities

- Unauthenticated access
- Bound to all interfaces instead of localhost
- Exposure to public networks
- Ability to write arbitrary files to disk
- Misuse of persistence features
- Weak or absent access controls

### Attack Prioritisation

- If Redis exposed >> prioritise immediate interaction
- If no auth required >> enumerate keys and configuration
- If access available >> assess ability to read/write data and interact wtih filesystem

**NOTE** that Redis is a **High-Value Target** for the reasons listed above.
