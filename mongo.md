
## Service Analysis - MongoDB (Port 27017)
<em>Section Added 1016-04-26</em>

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
