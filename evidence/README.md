# Evidence Index

This directory contains the supporting browser and OWASP ZAP evidence. Capture dates are taken from the screenshots and tool records where visible.

## Browser and HTTP response evidence
- [Firefox HTTP response capture](browser/firefox-http-response-2026-11-08.png) — 8 November 2026; Firefox Developer Tools records a normal `GET /` request to `testfire.net` returning `200 OK`.
- [Raw response headers](headers/raw-response-headers-2026-11-08.txt) — 8 November 2026; records the visible HTTP response headers. The captured response is HTTP, not HTTPS.
- [HTTP header evidence notes](headers/README.md) — describes which response fields are visible and the limits of that capture.
- [HTTPS certificate trust warning](tls/certificate-warning-2026-10-30.png) — 30 October 2026; Chrome displayed `NET::ERR_CERT_AUTHORITY_INVALID`. The cause is unconfirmed and is not a confirmed certificate vulnerability. See [TLS evidence notes](tls/README.md).

The final PDF report also contains a cropped public homepage image on page 4. The original Chrome DevTools screenshot containing a readable session identifier has been removed from the current public file tree. Do not re-upload it; use cropped or redacted evidence only.

## OWASP ZAP
See the [ZAP evidence index](zap/README.md). The 22 November 2026 captures include:
- Sites tree and History of normal browser-generated requests;
- the homepage HTTP response, with the JSESSIONID value redacted;
- the alert overview and selected passive alert details.

ZAP showed 16 alert categories. They are not 16 confirmed vulnerabilities. The findings register distinguishes observed configuration weaknesses from low-confidence or informational alerts. Related alerts have been grouped where they refer to the same script reference.

## Report
The nine-page report combines selected browser and ZAP evidence, explains the potential business impact of each candidate finding in plain English, and provides proposed risk priorities and OWASP/MDN-aligned remediation recommendations. The final PDF is stored in [report](../report/FUTURE_CS_01_Vulnerability_Assessment_Report.pdf).

## Evidence handling
Never publish session identifiers, cookie values, authentication tokens or personal data. Preserve relevant status codes, URLs, alert titles, confidence and risk details while redacting secrets.
