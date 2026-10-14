# Setup and Testing Guide (DVWA + Burp + ZAP)

Only test on DVWA, your own machine, or sites made for practice (like testphp.vulnweb.com). Testing real sites without permission is illegal.

## Part A: Install the tools

### 1. DVWA with Docker (fastest, about 5 minutes)
- Install Docker Desktop.
- Run in a terminal:
  - `docker run --rm -it -p 8080:80 vulnerables/web-dvwa`
- Open `http://localhost:8080`
- Login: `admin` / `password`
- Click **Create / Reset Database**, then log in again.
- Go to **DVWA Security** and set level to **Low**.

### DVWA with XAMPP (if no Docker)
- Install XAMPP. Start Apache and MySQL.
- Download DVWA from GitHub (digininja/DVWA). Put the folder in `htdocs`.
- Copy `config/config.inc.php.dist` to `config.inc.php`.
- Set DB user `root` and an empty password (or whatever yours is).
- Open `http://localhost/DVWA/setup.php` and click Create Database.

### 2. Burp Suite Community
- Download from portswigger.net.
- Open Burp, choose Temporary project, then Start Burp.
- Go to **Proxy > Open Browser** (built-in browser, no setup needed).
- Turn **Intercept on** to catch requests.

### 3. OWASP ZAP
- Download from zaproxy.org. Needs Java (the installer bundles it).
- Open ZAP and choose the "persist session: No" option for a quick run.

## Part B: Tests on DVWA (security level LOW)

### SQL Injection (menu: SQL Injection)
- Test 1: type `'` and submit. You get a SQL error.
- Test 2: type `1' OR '1'='1` . It shows all users.
- Test 3: type `1' UNION SELECT user, password FROM users -- ` . It shows usernames and password hashes.
- Screenshot: payload typed, and the result page.

### Reflected XSS (menu: XSS (Reflected))
- Type `<script>alert('Reflected XSS')</script>` in the name box.
- An alert pops up. Screenshot it, and the URL.

### Stored XSS (menu: XSS (Stored))
- Name: `test` (if the box limits length, edit the maxlength in browser Inspect).
- Message: `<script>alert('Stored XSS')</script>`
- Reload the page. The alert pops up again. That proves it is stored.
- Screenshot it.
- Reset with the "Clear Guestbook" option afterwards if needed.

### Burp capture
- With Intercept ON in Burp's browser, submit any test above.
- In Burp, screenshot the **request** (Raw tab).
- Click **Forward**, then open **HTTP history**, select the request, screenshot the **Response** tab.
- Bonus: right-click the request, **Send to Repeater**, change the payload, click Send, and screenshot.

### Optional: Brute Force (menu: Brute Force)
- Capture the login request, send it to Intruder, mark the password value, load a small wordlist.
- Sort by response length and screenshot the different one.

## Part C: ZAP automated scan
- In ZAP click **Automated Scan**.
- URL to attack: `http://localhost:8080` (DVWA).
- Click Attack. Wait for the Spider and the Active Scan to finish (10 to 30 minutes).
- Note: ZAP is not logged in, so it may miss pages behind login. For a better scan, log in through ZAP's browser first and add the site to Context.
- Open the **Alerts** tab. Screenshot the list.
- Export: **Report > Generate Report**, choose HTML (and PDF if offered). Save it.

## Screenshot checklist (name the files like this)
- 01_dvwa_login_security_low.png
- 02_sqli_payload.png
- 03_sqli_result.png
- 04_xss_reflected_payload.png
- 05_xss_reflected_result.png
- 06_xss_stored_payload.png
- 07_xss_stored_result.png
- 08_burp_request.png
- 09_burp_response.png
- 10_zap_scan_running.png
- 11_zap_alerts.png
- 12_zap_report.png

## Bonus: testphp.vulnweb.com
- It is a public practice site by Acunetix. Run a ZAP scan or try `http://testphp.vulnweb.com/listproducts.php?cat=1'` to see the SQL error.
