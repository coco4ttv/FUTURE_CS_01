# Testing Methodology

## Work completed

The assessment used normal browser navigation to publicly accessible Testfire pages and passive observation through OWASP ZAP.

### Historical browser checks
- On 30 October 2026, Chrome showed a `200 OK` response for `GET http://testfire.net/`.
- On 30 October 2026, Chrome displayed `NET::ERR_CERT_AUTHORITY_INVALID` for `https://testfire.net/`. The warning was recorded and not bypassed.
- On 8 November 2026, Firefox showed another `200 OK` response for `GET http://testfire.net/`.

### OWASP ZAP passive review — 22 November 2026
- ZAP was set to **Safe Mode**.
- Firefox was launched through ZAP and used to browse public-facing Testfire pages.
- The Sites tree was reviewed to identify the host and paths observed by the browser.
- The History panel was reviewed for normal browser-generated requests and response codes.
- The homepage response was inspected for status, server banner, content type and cookie attributes. The session cookie value was redacted in the saved screenshot.
- The Alerts panel was reviewed for passive observations and their ZAP risk/confidence values.

The History screenshot shows the homepage request returning `200 OK` and other browser-generated requests. It also contains some `404` and third-party `502` responses; these were not treated as vulnerabilities.

## Checks used

1. Open publicly accessible pages using normal browser navigation.
2. Record the requested hostname, URL, method, status and date where visible.
3. Inspect response headers and cookie attributes.
4. Observe browser-generated requests with ZAP Safe Mode enabled.
5. Review ZAP passive alert details and confidence.
6. Record evidence, limitations and remediation recommendations.

## Actions not performed

No login bypass, credential use, form submission, transaction, exploitation, attack payload, brute-force attempt, DoS testing, ZAP Active Scan, automated attack scan, spidering, crawling, fuzzing or Nmap port/service scan was performed.

## Scope limitations

The third-party hostnames appearing in ZAP were loaded or referenced during normal page browsing; they were not independently assessed. A passive alert is an indicator, not proof of exploitability. Where evidence or confidence was insufficient, the item was recorded as unconfirmed or excluded.

The local AltoroJ Docker practice instance was kept separate from the hosted Testfire target and was not used as evidence for this assessment.
