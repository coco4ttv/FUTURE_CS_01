# Testing Methodology

This is a constrained, read-only review. The order below is designed to avoid unnecessary requests and stop safely when the hosted demo is unavailable.

1. **Reachability check:** Visit the documented public entry point once. Record timestamp, URL, final URL, HTTP status or exact browser/network error. Do not repeatedly retry a failing host.
2. **HTTP behaviour:** If reachable, observe ordinary HTTP-to-HTTPS redirect behaviour using a browser or a single normal GET request. Do not submit data.
3. **TLS review:** If HTTPS is reachable without bypassing warnings, inspect certificate subject, issuer, validity period, subject alternative names and trust-chain result. If the browser reports an error, record it and stop before proceeding through the interstitial.
4. **Response headers:** Capture relevant headers from ordinary public page responses. Record the exact page and timestamp; do not assume one page represents the whole site.
5. **Cookie attributes:** Record whether Secure, HttpOnly and SameSite are present. Never record cookie values.
6. **Passive observation:** Only if the site is reachable, browse public pages manually while OWASP ZAP is configured for passive observation. Do not spider, crawl, fuzz or active scan.
7. **Validation and reporting:** Reproduce a candidate observation safely, assess impact, assign confidence and record remediation. Mark unverified items as pending rather than confirmed.

## Unavailability procedure
If the site does not respond, record the error, date/time, URL and whether DNS resolution succeeded (using ordinary system diagnostics only). Pause testing. Do not infer a vulnerability from downtime and do not substitute another host without documenting a revised scope and obtaining approval.
