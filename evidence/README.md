# Evidence Index

I have grouped the screenshots and notes by the type of evidence they contain. The dates below are the dates shown in the captures.

## Browser
- [Chrome HTTP homepage and response headers](browser/chrome_2026-10-30%20183814.png) — 30 October 2026; Chrome DevTools shows `GET http://testfire.net/`, `200 OK`, remote address `65.61.137.117:80`.
- [Firefox HTTP browser check](browser/firefox-http-response-2026-11-08.png) — 8 November 2026; Firefox DevTools shows `GET http://testfire.net/`, `200 OK`, remote address `65.61.137.117:80`, and four response headers.
- [HTTPS certificate warning](tls/certificate-warning-2026-10-30.png) — 30 October 2026; Chrome displayed `NET::ERR_CERT_AUTHORITY_INVALID` for `https://testfire.net/`.

## TLS
See [TLS evidence notes](tls/README.md). So far, I have captured the browser trust warning. I have not saved a certificate export, chain validation result or OpenSSL output.

## HTTP headers
See [HTTP header evidence notes](headers/README.md). The screenshots show the response-header fields visible in DevTools; I have not yet completed a full security-header review.

## ZAP
I have not added ZAP evidence yet. I will add it here if I complete passive observation during manual browsing.

## Evidence handling
Before sharing screenshots publicly, I check that session identifiers, cookie values, authentication tokens and personal data are not readable. The Chrome capture includes a Set-Cookie/JSESSIONID response; I need to ensure its value is redacted in the public image.
