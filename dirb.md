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

In order to probe for hidden pages, we run a dirb attack against FakeBank's url.

<img width="763" height="598" alt="image" src="https://github.com/user-attachments/assets/03c64f57-0e70-4d87-8e37-8f9df9819c74" />

Our scan reveals two hidden pages at the target URL: "images" and "bank-transfer".

### Exploit Vulnerable Bank-Transfer Page

Now, from the pages on fakebank.thm we already have access to, we can edit the URL to grant us access to one of the hidden pages of our choosing. As our objective here is to steal money from the bank, we're going to make use of the unprotected bank-transfer page.

<img width="940" height="937" alt="image" src="https://github.com/user-attachments/assets/d33d2173-9336-4945-b441-2531cf4f4316" />

Like so.

<img width="940" height="406" alt="image" src="https://github.com/user-attachments/assets/4e932363-4bb6-4c30-9730-c33489c419d6" />

Just like that, we have access a hidden page that was improperly secured by FakeBank.

### Transfer Funds

