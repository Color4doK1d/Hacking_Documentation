# Baby's First Hack - Password Cracking with TryHackMe

**Room Link:** https://tryhackme.com/room/hashingbasics |
**Difficulty:** N/A (Guided Learning Room) |
**Date Completed:** 2026/02/16

## Objective
Crack four passwords whose hashes' storage directories are known and accessible to the user.

## Tools Employed
- Linux Terminal
- Hashcat
- RockYou.txt
- Hashes.com

## Walkthrough
### First Password

1. **File Location**
   
The target password hash is stored in file location ~/Hashing-Basics/Task-6/hash1.txt

2. **Acquire Hash**
   
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

<img width="937" height="479" alt="image" src="https://github.com/user-attachments/assets/55004d2d-670e-4606-aab2-4bcdfd38162e" />

(Screenshot of the crack process in progress. I am sharing just to demonstrate the view from the Terminal; I will not paste screenshots from the subsequent cracking attempts).

<img width="460" height="164" alt="image" src="https://github.com/user-attachments/assets/221e8774-ac32-4ebf-857a-ee9e25b9458b" />

<img width="804" height="477" alt="image" src="https://github.com/user-attachments/assets/12c87bf7-d400-4598-8635-f1c16d5d7cd6" />

(This screenshot details the successful result of the crack)

With the hashcat command having executed successfully, I now know the hashed password: *85208520*

###Second Password

1. **File Location**

The second target password hash is located in the directory ~/Hashing-Basics/Task-6/hash2.txt

2. **Aquire Hash**

```bash
user@ip-10-80-175-45:~$ cat ~/Hashing-Basics/Task-6/hash2.txt
```

I run the same command to procure the hash from the target directory. **N.B.** I will skip these two steps on the subsequent two cracks, as they are identical each time, with the only difference between them being the name of the target file: 'hash1.txt'; 'hash2.txt'; etc.

