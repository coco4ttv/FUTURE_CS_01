# Evidence Index

This directory contains browser and OWASP ZAP screenshots and notes. Dates are taken from the captures where visible.

## Browser
- [Chrome HTTP homepage and response headers](browser/chrome_2026-10-30%20183814.png) — 30 October 2026; Chrome DevTools shows `GET http://testfire.net/`, `200 OK`.
- [Firefox HTTP browser check](browser/firefox-http-response-2026-11-08.png) — 8 November 2026; Firefox DevTools shows `GET http://testfire.net/`, `200 OK`.
- [HTTPS certificate warning](tls/certificate-warning-2026-10-30.png) — 30 October 2026; Chrome displayed `NET::ERR_CERT_AUTHORITY_INVALID`. The root cause is unconfirmed and this is not a confirmed certificate vulnerability.

## HTTP headers
See [HTTP header evidence notes](headers/README.md). The captures show selected response headers; they should not be interpreted as proof that every other security header is absent from every route.

## OWASP ZAP
See the [ZAP evidence index](zap/README.md). The 22 November 2026 captures include:
- Sites tree and History of normal browser-generated requests;
- the homepage HTTP response, with the JSESSIONID value redacted;
- the alert overview and selected passive alert details.

ZAP showed 16 alert categories. They are not 16 confirmed vulnerabilities. The findings register distinguishes observed configuration weaknesses from low-confidence or informational alerts.

The nine-page report includes selected browser and ZAP evidence together, plus plain-English business impact and OWASP-aligned remediation recommendations.

## Evidence handling
Session identifiers, cookie values, authentication tokens and personal data must not be readable in screenshots or text files published in this repository. Preserve relevant status codes, URLs, alert titles, confidence and risk details.
