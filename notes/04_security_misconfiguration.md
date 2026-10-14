# Notes: Security Misconfiguration

## What it is
- The software is fine, but it is set up in an unsafe way.
- OWASP calls it **A05: Security Misconfiguration** (2021 list).

## Common problems
- Default usernames and passwords left unchanged.
- Debug mode ON in production.
- Detailed error messages and stack traces shown to users.
- Directory listing enabled (anyone can browse folders).
- Unneeded services, sample apps, or ports left open.
- Missing security headers: `Content-Security-Policy`, `X-Frame-Options`, `X-Content-Type-Options`, `Strict-Transport-Security`.
- Cloud storage (S3 buckets) set to public.
- Old, unpatched software and servers.
- Server banners that reveal exact version numbers.

## How it is found
- OWASP ZAP and Burp Suite scanners flag missing headers and exposed files.
- Manual check: look at response headers, try `/admin`, `/backup`, `/.git`, `/phpinfo.php`.
- DVWA itself is a good example: default login `admin / password`, security level can be set to "low".

## Impact
- Information leaks that help the attacker plan.
- Full system access in bad cases (default admin panel).
- Makes other attacks (XSS, clickjacking) easier.

## How to fix
- Harden every environment. Use a repeatable checklist.
- Change all default credentials.
- Turn off debug and show generic error pages.
- Disable directory listing.
- Remove unused features, ports, and sample files.
- Add all key security headers.
- Patch and update regularly.
- Review cloud permissions often.

## Risk level
- **Low to High**, depending on what is exposed.

## Honest note
- Easy to find, easy to fix, and still very common. Good place for beginners to get quick wins.
