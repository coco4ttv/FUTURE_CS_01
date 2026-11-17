# Evidence Index

Evidence is grouped by the type of check. Record the exact hostname, scheme and capture time for every item. Sanitise screenshots before committing them.

## Browser
- [Chrome HTTP homepage and response headers](browser/HTTP%20homepage%20and%20response%20headers.jpeg) — 30 October 2026; `GET http://testfire.net/`, `200 OK`, remote address `65.61.137.117:80`.
- [Firefox HTTP browser check](browser/firefox_browser_check_2026-11-08%20210612.png) — 8 November 2026; Firefox DevTools shows `GET http://testfire.net/`, `200 OK`, remote address `65.61.137.117:80`, and four response headers.
- [HTTPS certificate warning](browser/https-certificate-warning.png) — 30 October 2026; Chrome displayed `NET::ERR_CERT_AUTHORITY_INVALID` for `https://testfire.net/`.

## TLS
See [TLS evidence notes](tls/README.md). The current evidence is a browser trust warning only; no certificate export, chain validation or OpenSSL output has been captured.

## HTTP headers
See [HTTP header evidence notes](headers/README.md). The browser captures show selected response headers, not a complete audit of every route or header.

## ZAP
The `zap/` directory is reserved for passive-mode evidence. No ZAP evidence is currently recorded.

## Evidence handling
Never publish passwords, authentication tokens, session-cookie values, personal data or browser storage. Check the 30 October Chrome screenshot for visible session-cookie material before public reuse; if the JSESSIONID value is readable, replace it with a redacted copy.
