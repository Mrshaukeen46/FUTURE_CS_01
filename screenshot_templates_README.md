# Screenshot Templates & Runbook — Web App Security Assessment (Windows 10)

WARNING: The HTML pages in this folder are SIMULATED TEMPLATES for training and screenshot composition only. They are NOT real scanner outputs. Do NOT present them as real evidence. Replace them with screenshots from your own lab scans before submission.

What these files are:
- Zap and scanner visual templates (HTML) to help you compose screenshots.
- Simple stylized console/text pages for sqlmap/nikto example output.
- A README with exact instructions for capturing original screenshots on Windows 10.

Goal:
- Help you produce consistent screenshots that show the correct elements (alert titles, severity, request/response text, payloads, header output, IP changes, etc.) while you run the real scans against your local Juice Shop / DVWA instance.

How to use
1. Start your target app locally (e.g., OWASP Juice Shop):
   - PowerShell: `docker run --rm -p 3000:3000 bkimminich/juice-shop`
   - Visit http://localhost:3000 to confirm.

2. Run OWASP ZAP / Burp Suite as described in the main runbook.

3. When you have a real finding:
   - Open the relevant HTML template to see which elements to capture (for example: product review showing the XSS payload or the ZAP alerts summary).
   - Take a real screenshot from the actual tool/browser or — if you need a placeholder in a draft report — take a screenshot of the corresponding simulated template. Make sure to clearly label simulated screenshots as "SIMULATED" if used in drafts.

How to capture screenshots on Windows 10
- Recommended tool: Snip & Sketch (Press Windows + Shift + S).
- For full-window capture: use Print Screen (PrtScn), then paste into Paint and save.
- Save screenshots with exact filenames below (so they match the report template):
  - screenshots/finding1_stored_xss.png
  - screenshots/finding2_sqli_sqlmap.png
  - screenshots/finding3_idor.png
  - screenshots/finding4_headers.png
  - screenshots/finding5_secret_exposure.png
  - screenshots/zap_scan_summary.png

Tips: what to include in each screenshot
- finding1_stored_xss.png
  - Browser window showing the XSS payload rendered / an active alert box triggered by the payload. Include the address bar showing the local URL (http://localhost:3000/...).

- finding2_sqli_sqlmap.png
  - Console output or Burp showing the injection attempt; if using sqlmap, capture the console panel showing evidence (database names, injection type). Save sqlmap output to `sqlmap_output.log` and include that file in the artifacts.

- finding3_idor.png
  - Burp/DevTools request and response where you changed an ID and received another user’s data. Ensure request/response and the modified parameter are visible.

- finding4_headers.png
  - Terminal or DevTools showing HTTP response headers (curl -I output), highlighting missing security headers.

- finding5_secret_exposure.png
  - Browser DevTools Sources or Network showing a visible API key or secret in a JS bundle or a static file. If a real secret is exposed, rotate it immediately.

- zap_scan_summary.png
  - ZAP Alerts tab or summary with a list of alerts and severities (High/Medium/Low) clearly visible.

Replacing simulated files with real evidence
- After you capture real screenshots, overwrite the simulated images or place the real ones into the `screenshots/` folder and update the Markdown report to reference the real files.
- Keep the scanner logs: `zaproxy_report.html`, `zaproxy_report.xml`, `sqlmap_output.log`, `nikto_report.txt`. Include them in your deliverable ZIP.

Ethics reminder
- Only run these tests on systems you own or have explicit authorization to test. Do not scan production or third-party systems.

If you want, I can:
- Produce a pre-configured ZAP context file for Juice Shop you can import, or
- Parse your real ZAP XML / sqlmap logs and automatically populate the report with findings and screenshots.