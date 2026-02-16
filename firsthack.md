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
cat ~/Hashing-Basics/Task-6/hash1.txt
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
hashcat -m 3200 -a 0 ~/Hashing-Basics/Task-6/hash1.txt rockyou.txt
```

<img width="937" height="479" alt="image" src="https://github.com/user-attachments/assets/55004d2d-670e-4606-aab2-4bcdfd38162e" />

(Screenshot of the crack process in progress. I am sharing just to demonstrate the view from the Terminal; I will not paste screenshots from the subsequent cracking attempts).

<img width="460" height="164" alt="image" src="https://github.com/user-attachments/assets/221e8774-ac32-4ebf-857a-ee9e25b9458b" />

<img width="804" height="477" alt="image" src="https://github.com/user-attachments/assets/12c87bf7-d400-4598-8635-f1c16d5d7cd6" />

(This screenshot details the successful result of the crack)

With the hashcat command having executed successfully, I now know the hashed password: *85208520*

### Second Password

1. **File Location**

The second target password hash is located in the directory ~/Hashing-Basics/Task-6/hash2.txt

2. **Aquire Hash**

```bash
cat ~/Hashing-Basics/Task-6/hash2.txt
```

I run the same command to procure the hash from the target directory. **N.B.** I will skip these two steps on the subsequent two cracks, as they are identical each time, with the only difference between them being the name of the target file: 'hash1.txt'; 'hash2.txt'; etc.

In this instance, the hash I discover reads: *9eb7ee7f551d2f0ac684981bd1f1e2fa4a37590199636753efe614d4db30e8e1*

3. **Determine Hash Type**

In this particular example, the Hash Type has already been supplied to me - SHA2-256.

<img width="1224" height="167" alt="image" src="https://github.com/user-attachments/assets/d647ca1c-7e33-4807-96e5-63c5962974d9" />

I can therefore refer to the Hashcat depository to determine the Hash Mode ID for SHA2-256, which is 1400, as shown in the above screenshot.

4. **Execute Password Crack**

Armed with the target directory, my word list and the Hash Mode ID, I can execute the crack just the same as before.

```bash
hashcat -m 1400 -a 0 ~/Hashing-Basics/Task-6/hash2.txt rockyou.txt
```

A successful crack returns the password: *halloween* (Which, incidentally, is my favourite holiday!)

### Third Password

1. **Summarising First Two Steps**

As detailed in the first two password cracks, armed with the target directory I can easily pull the hash from the file it is stored in.

```bash
cat ~/Hashing-Basics/Task-6/hash3.txt
```

This command returns the hash I am looking to crack: *$6$GQXVvW4EuM$ehD6jWiMsfNorxy5SINsgdlxmAEl3.yif0/c3NqzGLa0P.S7KRDYjycw5bnYkF5ZtB8wQy8KnskuWQS3Yr1wQ0*

2. **Determine Hash Type**

When a cursory visual scan of the Hashcat depository won't do, I run a simply page search for the "$6" prefix of the hash I've recovered.

<img width="1337" height="516" alt="image" src="https://github.com/user-attachments/assets/04d8f43f-a00e-4900-b0ce-422a4bd06f61" />

(Ignore my bookmarks bar!)

This is mostly an educated guess, but I can already be confident that I've located the correct hash type, as SHA matches the target system (Linux)

3. **Execute Password Crack**

Once again, I am now armed with all I need to attempt a crack.

```bash
hashcat -m 1800 -a 0 ~/Hashing-Basics/Task-6/hash3.txt rockyou.txt
```

Once this crack is successful, it returns the password: *spaceman*

### Fourth Password

1. **Summarising First Two Steps**

A more complete summary of this process is detailed under the First and Second Passwords I cracked. The process is exactly the same here, only I am pulling from the file 'hash4.txt'.

The search returns the target hash with a value of: *b6b0d451bbf6fed658659a9e7e5598fe*

2. **Hash Type**

This challenge is designed on the assumption that the hash type cannot or cannot be easily determined simply by searching through example tables. It therefore encourages the student to acquire the password by means other than a cracking attempt.

3. **Using Hashes.com**

Therefore, I copy/paste the hash I received into hashes.com, for it to run through its own internal Rainbow Tables to find a match:

<img width="1600" height="683" alt="image" src="https://github.com/user-attachments/assets/6e2be62c-b167-4fe1-9258-909e3affc89c" />

4. **Successful Search**

<img width="1590" height="352" alt="image" src="https://github.com/user-attachments/assets/f75fa086-0875-438d-b975-48213f2dd3ef" />

Hashes.com does indeed have the target hash on file, and it returns with the password: *funforyou*

## Result

Following the above steps I was able to determine all four target passwords:

- 85208520
- Halloween
- spaceman
- funforyou

## References

| Hash Type     | Prefix   | hashcat Mode | Example Command                                       |
|---------------|----------|--------------|-------------------------------------------------------|
| bcrypt        | `$2a$`     | 3200         | hashcat -m 3200 hash.txt rockyou.txt                  |
| SHA-256 (raw) | (none)   | 1400         | hashcat -m 1400 hash.txt rockyou.txt                  |
| sha512crypt   | `$6$`      | 1800         | hashcat -m 1800 hash.txt rockyou.txt                  |

## Summary

This is not a real TryHackMe Challenge Room; I am simply documenting a guided password cracking exercise from a learning room *(Cybersecurity 101 -> Cryptography -> Hashing Basics -> Task 6)*. This is both as a way to document and record my first "hack", and also an excuse to set up my GitHub profile and get used to using GitHub to document future CTFs, Challenge Rooms, etc. As a result of this process I have:

- Gotten comfortable with the hashcat command and its arguments;
- Solidifed my knowledge of hashing;
- Became more familiar with common hashing types such as bcrypt and SHA variants;
- Set-up a GitHub account
- Practiced documentation write-ups on GitHub

## Final Thoughts

The one-two punch of executing my first, albeit trivial, hack and taking the time to document it thoroughly has massively boomed my confidence. My plan is to continue on this track, building up a portfolio of documentation that I can both refer back to myself and display as proof of my achievements in this space.

Looking forwards to the next one.
