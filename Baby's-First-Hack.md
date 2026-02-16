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

3. **Acquire Hash**
   
```bash
user@ip-10-80-175-45:~$ cat ~/Hashing-Basics/Task-6/hash1.txt
```

With the target directory known, the hash can be retrieved for review.

Running the above command returns a hash value of: *$2a$06$7yoU3Ng8dHTXphAg913cyO6Bjs3K5lBnwq5FJyA6d01pMSrddr1ZG*

3. **Determine Hash Type**
   
Now with the hash known to me, I can cross-reference it as best as possible with, in this case, the Hashcat depository of hash examples to discover its type.

<img width="1176" height="901" alt="image" src="https://github.com/user-attachments/assets/7446d9a5-a73d-4645-b719-717d40aea612" />

Having identified the hash type as bcrypt, I now have the Hash-Mode ID that I can feed into the hashcat command for my cracking attempt.

4. **Execute Password Crack**

I will be using the rockyou.txt password leak as my wordlist for the attack.

```bash
user@ip-10-80-175-45:~$ hashcat -m 3200 -a 0 ~/Hashing-Basics/Task-6/hash1.txt rockyou.txt
```

Test Text
