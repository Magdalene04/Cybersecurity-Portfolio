# OWASP 10 2025: IAAA Failures
**a)** The OWASP Top 10 is a list compiled by the Open Web Application Security Project (OWASP) that outlines the most critical security risks to web applications. <br>
**b)** The list is updated periodically to reflect changes in the security landscape and includes categories that highlight common vulnerabilities. 

In this room, we will cover three topics: <br>
**A01**: *Broken Access Control* <br>
**A07**: *Authentication Failures* <br>
**A09**: *Logging and Alerting Failures*

## What is IAAA?
IAAA is the way where we can verify a users action on an application. Each item in IAAA plays a crucial role, that only if one gets complete, it moves to the next stage. The four items are as follows:

**Identity** - The unique account (e.g., user ID/email) that represents a person or service. <br>
**Authentication** - Proof for that identity (passwords, OTP, passkeys). <br>
**Authorisation** - What that identity is allowed to do. <br>
**Accountability** - Recording and alerting on who did what, when, and from where. <br>

### Questions:
1) What does IAAA stand for? <br>
**Ans:** Identity Authentication Authorization and Accountability

## A01: Broken Access Control
Broken Access Control happens when the server doesn’t properly enforce who can access what on every request. A common occurence of this is **IDOR (Insecure Direct Object Reference)**: if changing an ID like ?id=7 → ?id=6, lets you see or edit someone else’s data, access control is broken here.

### Questions:
1) If you don't get access to more roles but can view the data of another users, what type of privilege escalation is this? <br>
**Ans:** Horizontal

2) What is the note you found when viewing the user's account who had more than $ 1 million?
**Ans:** THM{Found.the.Millionare!}

<img width="910" height="855" alt="image" src="https://github.com/user-attachments/assets/492efb59-08a6-4b92-91e5-d9705ba996ee" />

## A07: Authentication Failures
Authentication Failures happen when an application can’t reliably verify or bind a user’s identity. Common issues include:

**a)** Username Enumeration. <br>
**b)** Weak/Guessable Passwords (no lockout/rate limits). <br>
**c)** Logic flaws in the login/registration flow. <br>
**d)** Insecure Session or Cookie Handling. <br>

If any of these are present, an attacker can often log in as someone else or bind a session to the wrong account.

<img width="921" height="723" alt="image" src="https://github.com/user-attachments/assets/cf2a643c-1d39-4eac-978f-dc986adad56b" />

<img width="914" height="617" alt="image" src="https://github.com/user-attachments/assets/3b73129a-7758-47d9-a8af-be1d63e61a5a" />

<img width="911" height="840" alt="image" src="https://github.com/user-attachments/assets/167d20e3-f3b1-4949-9c8d-8a3263aef730" />

### Questions:
1) What is the flag on the admin user's dashboard? <br>
**Ans:** THM{Account.confusion.FTW!}

## A09: Logging and Alerting Failures
When applications don’t record or alert on security-relevant events, defenders can’t detect or investigate attacks. Good logging underpins accountability (being able to prove who did what, when, and from where). In practice, failures look like missing authentication events, vague error logs, no alerting on brute-force or privilege changes, short retention, or logs stored where attackers can tamper with them.

### Questions:
1) It looks like an attacker tried to perform a brute-force attack, what is the IP of the attacker? <br>
**Ans:** 203.0.113.45

<img width="906" height="811" alt="image" src="https://github.com/user-attachments/assets/c29c1c57-5703-412d-979b-99ae2c15d096" />

2) Looks like they were able to gain access to an account! What is the username associated with that account? <br>
**Ans:** Admin

<img width="886" height="525" alt="image" src="https://github.com/user-attachments/assets/302d8b56-2f4a-4ae5-83de-2331430b1520" />

3) What action did the attacker try to do with the account? List the endpoint the accessed. <br>
**Ans:** /supersecretadminstuff

## Conclusion

**a) A01 Broken Access Control:** Enforce server-side checks on every request. <br>
**b) A07 Authentication Failures:** Enforce unique indexes on the canonical form, rate-limit/lock out brute force, and rotate sessions on password/privilege changes. <br>
**c) A09 Logging & Alerting Failures:** Log the full auth lifecycle (fail/success, password/2FA/role changes, admin actions), centralise logs off-host with retention, and alert on anomalies (e.g., brute-force bursts, privilege elevation).
