# Notes: Broken Authentication

## What it is
- Weak or wrong login and session handling lets attackers become other users.
- OWASP calls it **A07: Identification and Authentication Failures** (2021 list). Before 2021 it was "Broken Authentication".

## Common problems
- Weak or default passwords (`admin/admin`, `admin/password`).
- No limit on login tries, so **brute force** and **credential stuffing** work.
- Session ID in the URL, or session ID that is easy to guess.
- Session does not expire, or is not destroyed on logout.
- Weak "forgot password" flow (easy security questions, guessable reset links).
- No multi-factor authentication (MFA).
- Passwords stored in plain text or with weak hashing (MD5).

## How it is tested (DVWA Brute Force module)
- Capture the login request in Burp Suite.
- Send it to **Intruder** and try a list of common passwords.
- Look at response length. A different length often means success.

## Impact
- Account takeover.
- Data theft.
- Admin access in the worst case.

## How to fix
- Strong password rules + check against leaked-password lists.
- **Rate limiting** and account lockout (or CAPTCHA).
- Turn on **MFA**.
- Generate long random session IDs. Regenerate after login.
- Session timeout and proper logout.
- Hash passwords with **bcrypt / Argon2**, never MD5 or plain text.
- No default accounts in production.

## Risk level
- **High**

## Honest note
- This is one of the most common real-world causes of breaches. It is boring, but it works for attackers.
