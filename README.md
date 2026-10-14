# Web Security & Vulnerability Testing (VAPT Basics) - Week 6

Hands-on VAPT practice on **DVWA** (Damn Vulnerable Web Application) running in Docker, using **Burp Suite Community** and **OWASP ZAP**.
All testing was done on my own local lab at security level **Low**. Educational use only.

## What I tested
- SQL Injection (payload `1' OR '1'='1` dumped all users) - High
- Reflected XSS - Medium
- Stored XSS - High
- Automated ZAP scan: 9 alerts (0 High, 2 Medium, 5 Low, 2 Info)

## Folder structure
| Folder | Contents |
|---|---|
| `report/` | Full project report (PDF + DOCX, 14 pages) |
| `presentation/` | 9-slide PPT |
| `screenshots/` | Payloads, results, Burp request/response, ZAP alerts |
| `notes/` | OWASP notes: SQLi, XSS, Broken Authentication, Security Misconfiguration, plus setup guide |

## Run the lab
```bash
docker run --rm -it -p 8080:80 vulnerables/web-dvwa
# open http://localhost:8080  (admin / password), create DB, set security to Low
```

## Tools
Burp Suite Community, OWASP ZAP, DVWA, Docker

## Author
Kritika Rai
