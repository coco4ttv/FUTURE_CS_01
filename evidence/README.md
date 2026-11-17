# Evidence Index

Evidence is grouped by the type of observation. All evidence must be captured within the read-only scope and sanitised before committing.

## Browser
- [HTTP homepage and response headers](browser/HTTP%20homepage%20and%20response%20headers.jpeg) — redacted Chrome screenshot of the homepage request and selected DevTools response headers (30 October 2026).
- [HTTPS certificate warning](browser/https-certificate-warning.png) — Chrome warning for the HTTPS entry point showing NET::ERR_CERT_AUTHORITY_INVALID (30 October 2026).

## TLS, headers and ZAP
The `tls/`, `headers/` and `zap/` directories are reserved for future evidence. No evidence is claimed until it has actually been captured.

## Evidence handling
Never publish passwords, authentication tokens, session-cookie values, personal data or browser storage. Crop screenshots to relevant evidence and redact secrets. Preserve original timestamps and distinguish historical captures from later re-tests.
