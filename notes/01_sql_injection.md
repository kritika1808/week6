# Notes: SQL Injection (SQLi)

## What it is
- SQL Injection happens when an app puts user input straight into a database query.
- The attacker types SQL code instead of normal data. The database runs it.
- OWASP lists this under **A03: Injection** (2021 list).

## Simple example
- Login code: `SELECT * FROM users WHERE user='$u' AND pass='$p'`
- Attacker types `admin' --` as the username.
- Query becomes: `SELECT * FROM users WHERE user='admin' -- ' AND pass=''`
- `--` makes the rest a comment. The password check is skipped.

## Types
- **In-band (classic):** you see the result on the page.
  - Error-based: the database error leaks info.
  - UNION-based: attacker joins extra data to the normal result.
- **Blind:** the page shows no data, but behaves differently.
  - Boolean-based: page changes for true/false.
  - Time-based: attacker uses `SLEEP(5)` to see if the query ran.
- **Out-of-band:** data is sent via DNS/HTTP to the attacker (rare).

## Common test payloads (use ONLY on DVWA or labs you own)
- `'` (single quote) - checks if the app breaks.
- `1' OR '1'='1` - always true, dumps all rows.
- `1' UNION SELECT user, password FROM users -- ` - pulls usernames and password hashes.
- `1' AND SLEEP(5) -- ` - time-based test.

## Impact
- Read all data in the database (users, emails, hashes).
- Change or delete data.
- Bypass login.
- Sometimes run commands on the server.

## How to fix
- **Prepared statements / parameterized queries** (best fix).
- Use an ORM properly (do not build raw strings).
- Validate input (allow-list), but do not rely on this alone.
- Give the database account least privilege (no DROP, no admin).
- Hide detailed error messages from users.
- Use a WAF as an extra layer, not the main defense.

## Risk level
- **Critical / High.** Easy to exploit, huge damage.

## Honest note
- SQLi is old but still shows up. Many small business and student-built sites still have it.
