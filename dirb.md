# A Really Simple Example of Dirb in Action

**Room Link:** https://tryhackme.com/room/offensivesecurityintro |
**Difficulty:** N/A (Guided Learning Room) |
**Date Completed:** 2026/03/17

## Objective
Illicitly transfer money from a bank to a designated account by exploiting a hidden page vulnerability on the bank's website, thus demonstrating both dirb's efficacy and the danger of hidden page vulnerabilities

## Tools Employed
- Windows CLI
- Dirb

## Walkthrough
### Reconnaissance

<img width="1093" height="1049" alt="image" src="https://github.com/user-attachments/assets/e953582c-60db-4571-aa4b-5814a9ed6baa" />

Our target is FakeBank, which runs a browser service for account holders. By typing their URL into our browser we can then input our Username and Password to be taken directly to our account dashboard. Our account in this scenario is No. 8881.

### Find Hidden Pages on fakebank.thm

In order to probe for hidden pages, we run a dirb attack against FakeBank's url. We input the following command into Windows' CLI:

```bash
dirb http://fakebank.thm
```

<img width="763" height="598" alt="image" src="https://github.com/user-attachments/assets/03c64f57-0e70-4d87-8e37-8f9df9819c74" />

Our scan reveals two hidden pages at the target URL: "images" and "bank-transfer".

### Exploit Vulnerable Bank-Transfer Page

Now, from the pages on fakebank.thm we already have access to, we can edit the URL to grant us access to one of the hidden pages of our choosing. As our objective here is to steal money from the bank, we're going to make use of the unprotected bank-transfer page.

<img width="940" height="937" alt="image" src="https://github.com/user-attachments/assets/d33d2173-9336-4945-b441-2531cf4f4316" />

Like so.

<img width="940" height="406" alt="image" src="https://github.com/user-attachments/assets/4e932363-4bb6-4c30-9730-c33489c419d6" />

Just like that, we have access to a hidden page that was improperly secured by FakeBank.

### Transfer Funds

Now we can transfer money to any account we elect. Let's wipe out our overdraft, and give us a little something extra for our troubles.

<img width="940" height="451" alt="image" src="https://github.com/user-attachments/assets/c457b8e9-56c6-4579-8d6a-df67f33a7b16" />

Now we simply execute the transfer, and we are mission accomplished.

## Result

$2,000 successfully transferred from FakeBank to Account Number 8881

## Summary

This barely constitutes a hack, certainly not one worth documenting, but I decided to do so simply as an excuse to continue honing my familiarity with GitHub as well as my own personal documentation process. I feel like I have a bit of refinement still to etch out. Ideally I would want these documents to be so thorough that anybody could emulate the steps I took.

I wrote this quickly, and leaned on my screenshots to do some of the talking for me. I believe that while this is functional, in future my written documentation should be erven more granular and break down every action in text form, using screenshots simply as a visual aid, not a guide.

Conscious of this, I have since gone back to add in a little more detail early on, including providing the exact command line used by me in this attack. Otherwise, I will leave this guide unchanged, and take care to be more thorough in future.

## Final Thoughts

This is really an exercise in my familiarity with GitHub first and foremost, and my etiquette in devising these documentations. From that, it was a good exericse. The hack itself is almost certainly never to work quite this way against any real major target, let alone a financial institution. Nonetheles, it's a fun backdrop to explore the functionality of dirb in very simple terms and served as a great excuse to write another document.
