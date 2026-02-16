# Baby's First Hack - Password Cracking with TryHackMe

**Room Link:** https://tryhackme.com/room/hashingbasics |
**Difficulty:** N/A (Guided Learning Room) |
**Date Completed:** 2026/02/16

## Objective
Crack four passwords whose hashes' storage directories are known and accessible to the user.

## Tools Employed
- Hashcat
- RockYou.txt
- Hashes.com

## Walkthrough
### First Password

1. **File Location**
The target password hash is stored in file location ~/Hashing-Basics/Task-6/hash1.txt

2. **Acquire Hash**
<div style="background: #0d1117; border-radius: 8px; padding: 16px; margin: 20px 0; border: 1px solid #30363d; box-shadow: 0 4px 12px rgba(0,0,0,0.4); font-family: 'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, monospace; font-size: 13px; color: #c9d1d9; line-height: 1.5; overflow-x: auto;">
  <div style="border-bottom: 1px solid #21262d; padding-bottom: 8px; margin-bottom: 8px; color: #8b949e; font-size: 0.9em;">
    ~/Hashing-Basics/Task-6
  </div>
user@ip-10-80-175-45:~$ cat ~/Hashing-Basics/Task-6/hash1.txt<br>
$2a$06$7yoU3Ng8dHTXphAg913cyO6Bjs3K5lBnwq5FJyA6d01pMSrddr1ZG<br>
user@ip-10-80-175-45:~$
</div>
