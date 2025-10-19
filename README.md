
🛡️ Web Application Security Testing
# Readme — How to run the Web Application Security Assessment on Windows 10

Prepared by: Mrshaukeen46  
Date: 2025-10-19

This README is a step-by-step runbook for executing the assessment described in `Security_Assessment_Report.md` on a Windows 10 machine. Follow these steps and collect the artifacts named in the report.

1) Prerequisites (Windows 10)
   - Admin access
   - Docker Desktop installed (with WSL2 backend recommended)
   - WSL2 (Ubuntu) installed (recommended for sqlmap/nikto)
   - OWASP ZAP (Windows installer)
   - Burp Suite Community (Windows)
   - Firefox browser (use a separate profile for testing)
   - Pandoc / VSCode (optional) for PDF export

2) Start Juice Shop (locally)
   - Open PowerShell:
     `docker run --rm -p 3000:3000 bkimminich/juice-shop`
   - Confirm: open http://localhost:3000

3) Configure Proxy (ZAP or Burp)
   - ZAP default port: 8080 or 8081 depending on install — confirm in ZAP Options.
   - Set Firefox proxy to 127.0.0.1:8080 (or 8081).
   - Import ZAP/Burp CA certificate into Firefox (Options -> Privacy & Security -> Certificates).

4) Crawl & Scan
   - Start ZAP -> Quick Start -> Attack -> `http://localhost:3000`
   - Let ZAP crawl and run Passive scan; after crawl, start Active Scan on the context.
   - Inspect Alerts tab, mark high-confidence items to reproduce manually.

5) Manual Verification
   - Switch browser to Burp (127.0.0.1:8080) if using Burp.
   - Use Burp Repeater to send XSS payloads; use sqlmap from WSL to confirm SQLi.

6) sqlmap example (in WSL2)
   - Identify suspicious request/parameter from Burp/ZAP.
   - Run:
     `sqlmap -u "http://localhost:3000/rest/products?q=test" -p q --batch --level=2 --risk=1 --threads=2 > sqlmap_output.log`

7) Nikto example (in WSL2)
   - `nikto -h http://localhost:3000 -output nikto_report.txt`

8) Capture Evidence
   - Use Snipping Tool to capture:
     - ZAP alerts screen -> save `screenshots/zap_scan_summary.png`
     - Browser showing XSS alert -> save `screenshots/finding1_stored_xss.png`
     - sqlmap console output -> save `screenshots/finding2_sqli_sqlmap.png`
     - Burp request/response showing IDOR -> save `screenshots/finding3_idor.png`
     - curl or DevTools headers -> save `screenshots/finding4_headers.png`
     - DevTools showing secret -> save `screenshots/finding5_secret_exposure.png`

9) Export Scanner Reports
   - ZAP: Reports -> Generate HTML -> `zaproxy_report.html`
   - Burp: Save project or export issues if possible.

10) Populate Report
   - Replace example findings in `Security_Assessment_Report.md` with your captured screenshots and log filenames.
   - Ensure `OWASP_Top10_Checklist.md` is updated with statuses and evidence.

11) Convert to PDF
   - Use VSCode or Pandoc as described in the report.

12) Package Deliverable
   - `Security_Assessment_Report.pdf`
   - `OWASP_Top10_Checklist.md`
   - `zaproxy_report.html`, `sqlmap_output.log`, `nikto_report.txt`
   - `screenshots/` folder with images

13) Ethics Reminder
   - Only run on authorized targets. Do not scan production or third-party sites without explicit permission.

