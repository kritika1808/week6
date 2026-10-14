# Notes: Cross-Site Scripting (XSS)

## What it is
- XSS happens when a site shows user input on a page without cleaning it.
- The attacker's JavaScript then runs in the victim's browser.
- OWASP lists this under **A03: Injection** (2021 list).

## Types
- **Reflected XSS**
  - Payload is in the URL or form and is reflected back right away.
  - Victim must click a crafted link.
  - Not saved on the server.
- **Stored XSS**
  - Payload is saved in the database (comment, guestbook, profile).
  - Runs for EVERY user who views that page.
  - More dangerous than reflected.
- **DOM-based XSS**
  - Bug is in the browser-side JavaScript, not the server.
  - Page code reads from the URL and writes it into the page unsafely.

## Test payloads (only on DVWA or labs you own)
- `<script>alert('XSS')</script>` - basic test.
- `<img src=x onerror=alert(1)>` - works when `<script>` is blocked.
- `<svg onload=alert(1)>` - another bypass.

## Impact
- Steal session cookies and hijack accounts.
- Show fake login forms (phishing inside a real site).
- Redirect users to bad sites.
- Do actions as the victim.

## How to fix
- **Output encoding:** turn `<` into `&lt;` before showing user data.
- Use frameworks that auto-escape (React, Angular, Jinja2).
- Set a **Content-Security-Policy (CSP)** header.
- Mark cookies `HttpOnly` and `Secure` so JavaScript cannot read them.
- Sanitize HTML with a trusted library (e.g., DOMPurify) if you must allow HTML.

## Risk level
- Reflected: **Medium**
- Stored: **High**

## Honest note
- `alert(1)` looks harmless, but it only proves that JavaScript runs. Real attacks steal sessions.
