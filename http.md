## Service Analysis - HTTP (Port 80)
*Section Added: 2026-04-26*

Hypertext Transfer Protocol (HTTP) is a stateless application-layer protocol used for transmitting web content between clients (browsers) and servers, typically over Port 80.

HTTP follows a request-response model:

- A client sends a request (e.g. GET, POST) to the server
- The server processes it and returns a response (HTML, JSON, files, etc.)

Users interact through browsers, but under the surface it's structured text flying back and forth.

### Why HTTP Matters

As the backbone of the internet HTTP is one of the most common and important services.

Its presence indicates:

- A web application or site is hosted
- A primary user-facing interface exists
- A large and complex attack surface is likely present

Unlike many services, HTTP is rarely the system itself, but a gateway into deeper layers including:

- Backend logic
- Databases
- Authentication Systems

### Common Misconfigurations & Vulnerabilities

- Directory listing enabled (exposed files and structure)
- Default or hidden pages (admin panels, backups, test endpoints)
- Weak auth mechanisms
- Input handlings vulnerabilities (e.g. injection flaws)
- Misconfigured file permissions
- Outdatd server software or frameworks
- Exposure of sensitive files (configs, credentials, source code)

HTTP is especially prone to:

- Logic flaws
- Poort input validation
- Accidental exposure of internal functionality

### Attack Prioritisation

- If Port 80 open >> prioritise enumeration of web application
- Identify: pages & endpoints; tech in use; auth mechanisms

HTTP is a **primary entry point** becaise:

- It is designed to be interacted with
- It often exposes complex functionality
- Small mistakes can lead to full compromise
