# Future Interns — Task 1: Vulnerability Assessment Report

## Project status
Planning and scope definition. No security scans have been run yet.

## Objective
Produce a read-only vulnerability assessment of an authorised target, document substantiated findings, classify risks as Low / Medium / High, and provide practical remediation guidance.

## Scope and ethics
- **Target:** To be confirmed.
- **Authorisation:** Must be confirmed before scanning.
- **In scope:** Publicly accessible pages and explicitly authorised passive/read-only checks.
- **Out of scope:** Login bypass, exploitation, brute force, denial-of-service, intrusive testing, and any activity that could harm the site.
- Do not describe an issue as a confirmed vulnerability without reproducible evidence.

## Planned tools
- **Nmap:** Only for a target where scanning is explicitly permitted; keep checks limited and non-intrusive.
- **OWASP ZAP:** Passive scanning only; do not use active scan or attack features.
- **Browser Developer Tools:** Inspect browser-visible response headers, cookies and client-side behaviour.
- **Canva:** Design the final report.

## Planned workflow
1. Confirm the target and written permission / permitted test scope.
2. Record assessment date, target URL, scope, exclusions and methodology.
3. Capture baseline browser observations and relevant response headers.
4. Perform only permitted, low-impact checks.
5. Record each finding with evidence, impact, risk level, confidence and recommended remediation.
6. Review findings and distinguish confirmed observations from items that could not be verified.
7. Design and export the final report as a PDF.
8. Publish the report and sanitised supporting evidence in this repository.

## Findings
No findings have been confirmed yet. This section will be updated after the assessment. Do not treat potential issues as confirmed findings.

## Deliverables
- [ ] Canva-designed report exported to PDF
- [ ] README updated with the actual target, scope, tools, limitations and assessment date
- [ ] Sanitised screenshots and relevant tool outputs
- [ ] Remediation recommendations
- [ ] Final review for accuracy and sensitive information

## Disclaimer
This is an educational, read-only assessment. Results will be limited to the target, date and methods documented in the final report. Absence of a finding does not prove the website is secure.
