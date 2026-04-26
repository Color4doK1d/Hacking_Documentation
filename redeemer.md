# Redeemer

**Room Link:** https://app.hackthebox.com/machines/Redeemer?sort_by=created_at&sort_type=desc |
**Difficulty:** Very Easy |
**Date Completed:** 2026-04-23

## Objective
Capture the flag on the target machine

## Tools Employed
- nmap
- redis-cli
- redis.io documentation

## Walkthrough
### Reconnaissance & Enumeration

- Ran nmap scan on the target IP address

> <img width="947" height="306" alt="nmap 1" src="https://github.com/user-attachments/assets/1d8a681f-2c2a-4cbb-bd3c-d42558c8e158" />
> <em>Figure 1: Initial nmap scan</em>

- Initial scan of the most common 1,000 ports shows all ports closed. Although this could be a firewall blocking an nmap TCP SYN probe, I try to get a better idea of the lay of the land before jumping to conclusions.

> <img width="946" height="338" alt="nmap 2" src="https://github.com/user-attachments/assets/9a3c3ed2-dfc5-4423-ab55-479c9c8e5ed2" />
> <em>Figure 2: Second nmap scan run against all target system's ports</em>

- A scan of all ports reveals that one port is open, running a Redis service. This is interesting, as Redis services tend to lack authentication checks, and makes this system acutely vulnerable if misconfigured.

### Exploit

- I admit at this point I had to step out of the terminal to do a little bit of research. I am unfamiliar with Redis beyond the basic concept, and so had no idea how to interface with the open port once I'd identified it. Through my Google searches however I identified redis-cli as the program I needed to connect to a live Redis service.

- From there, I simply had to work out on the fly how to use redis-cli.

> <img width="818" height="301" alt="redis help" src="https://github.com/user-attachments/assets/b6045e4a-b7d4-498a-bde0-735816664aff" />
> <em>Figure 3: redis-cli command documentation; highlight my own</em>

- Notably, unlike the tools I've been deploying so far, there's a quirk in redis-cli's syntax that requires a Host switch (-h) to be called before a target IP address can be passed to it. I made note of this in my field notes.

- Once I'd successfully connected with the service (it required no login credentials) I found myself stuck. I was entirely unfamiliar with redis' command structure and syntax and so went onto redis.io and looked up their documentation on Redis commands. Even this, I'll admit, took me a couple of moments to wrap my head around, as the language and syntax was entirely alien to anything I've worked with through a CLI to date.

- ([See documentation here](https://redis.io/docs/latest/commands/redis-8-6-commands/))

> <img width="814" height="765" alt="help 2" src="https://github.com/user-attachments/assets/f38411d6-eba1-4fd4-9ee7-3fdbc309bbaa" />
> <em>Figure 4: Redis service help documentation</em>

- Nonetheless with the help of both the online documentation and the in-service documentation I managed to experiment and fumble and, through trial and error, ascertain how to acquire the flag.

## Flags

> <img width="358" height="146" alt="flag" src="https://github.com/user-attachments/assets/6e03a556-c27d-493e-ac22-936f481f69d6" />
> <em>Figure 5: My fourth legitimate flag capture</em>

## Summary

This required some active problem solving, as it required a somewhat deeper understanding of nmap and how it works, as well as interfacing with a very different system, at least to what I'm used to. This box required me to factfind on my feet while in the middle of the exploitation, in order to take advantage of what proved to be a completely undefended system.

Maybe the best defence is an arcane and archaic attack surface... (Okay, maybe not).

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


## Final Thoughts

This challenge seemed designed to encourage students to think on their feet, and problem-solve on the fly. It required some amount of research from me to understand what I was looking at and then how to navigate; I satisfied myself that I am growing confident enough with the fundamentals of this process that I do not immediately balk when faced with a twist or complications.

I don't know if this is a strong testament to how I'm performing so far or to the ingenuity of HacktheBox's sysadmins but either way, I feel extremely confident in this and eager to move forwards
