# OWASP ZAP Evidence

**Capture date:** 22 November 2026  
**Target:** `http://testfire.net/`  
**ZAP mode:** Safe Mode; passive observation only

I used OWASP ZAP while manually browsing publicly accessible Testfire pages. The screenshots document the Sites tree, browser-generated History entries, an HTTP response and selected passive alerts.

## Screenshot index

| File | What it shows |
|---|---|
| [01-alert-overview.png](01-alert-overview.png) | ZAP alert tree showing 16 alert categories |
| [02-sites-tree.png](02-sites-tree.png) | Testfire host and paths observed by ZAP; other hosts appear where pages referenced external resources |
| [03-http-history.png](03-http-history.png) | Normal browser-generated requests, including the Testfire homepage returning `200 OK` |
| [04-homepage-http-response.png](04-homepage-http-response.png) | Homepage HTTP response; the JSESSIONID value is redacted |
| [05-anti-csrf-token-alert.png](05-anti-csrf-token-alert.png) | Passive alert for forms where no recognised anti-CSRF token was identified; no form was submitted |
| [06-content-security-policy-alert.png](06-content-security-policy-alert.png) | CSP response-header alert |
| [07-anti-clickjacking-header-alert.png](07-anti-clickjacking-header-alert.png) | Missing anti-clickjacking protection alert |
| [08-subresource-integrity-alert.png](08-subresource-integrity-alert.png) | External script reference without an integrity attribute |
| [09-samesite-cookie-alert.png](09-samesite-cookie-alert.png) | JSESSIONID cookie reported without a SameSite attribute |
| [10-cross-domain-javascript-alert.png](10-cross-domain-javascript-alert.png) | Cross-domain JavaScript source reference; related to the external-script/SRI observation |
| [11-debug-error-message-alert.png](11-debug-error-message-alert.png) | Full ZAP alert view for a generic `Internal server error` response |
| [12-debug-error-message-detail.png](12-debug-error-message-detail.png) | Closer detail view of the same generic error alert |
| [13-server-header-disclosure-alert.png](13-server-header-disclosure-alert.png) | `Server: Apache-Coyote/1.1` response header |
| [14-x-content-type-options-alert.png](14-x-content-type-options-alert.png) | Missing `X-Content-Type-Options: nosniff` alert |

## What the captures establish

- The ZAP interface shows **Safe Mode** selected.
- The History capture shows a normal `GET http://testfire.net/` request with a `200 OK` response and other requests generated during manual browsing.
- The homepage response shows `HTTP/1.1 200 OK`, `Server: Apache-Coyote/1.1`, `Content-Type: text/html; charset=ISO-8859-1` and a redacted `Set-Cookie` value with `Path=/` and `HttpOnly`.
- The alert overview contains 16 categories. Technology detections and informational alerts are not automatically vulnerabilities.
- The external JavaScript evidence references `http://demo-analytics.testfire.net/urchin.js`. ZAP History shows a failed response for that external request in this capture, so successful script delivery was not established.
- The debug-error screenshots show only the generic text `Internal server error`; they do not show a stack trace, file path, database details or other sensitive diagnostic data.

## Interpretation limits

ZAP's alert risk and confidence are recorded in the screenshots. A passive alert is not proof of exploitability. The anti-CSRF alert has low confidence and is treated as an unverified observation because no form submission or request-behaviour test was performed. The debug-error alert is also treated as unconfirmed because the visible evidence is generic.

The HSTS alert is not treated as a finding on the basis of an HTTP response alone. Suspicious-comment and technology-detection alerts are not included as security findings without relevant supporting detail.

## Ethical boundaries

Only public-facing pages and browser-generated requests were observed. No login bypass, exploitation, brute force, DoS, active scanning, spidering, fuzzing or form submission was performed. The third-party hosts visible in the Sites tree were not independently tested.
