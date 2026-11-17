# Evidence Index

I have grouped my screenshots and notes by the type of evidence they contain. The dates below are the dates shown in the captures.

## Browser
- [Chrome HTTP homepage and response headers](browser/chrome_2026-10-30%20183814.png) — 30 October 2026; Chrome DevTools shows `GET http://testfire.net/`, `200 OK`, remote address `65.61.137.117:80`.
- [Firefox HTTP browser check](browser/firefox-http-response-2026-11-08.png) — 8 November 2026; Firefox DevTools shows `GET http://testfire.net/`, `200 OK`, remote address `65.61.137.117:80`, and four response headers.
- [HTTPS certificate warning](tls/certificate-warning-2026-10-30.png) — 30 October 2026; Chrome displayed `NET::ERR_CERT_AUTHORITY_INVALID` for `https://testfire.net/`.

## TLS
See [TLS evidence notes](tls/README.md). So far, I have captured the browser trust warning. I have not saved a certificate export, chain validation result or OpenSSL output.

## HTTP headers
See [HTTP header evidence notes](headers/README.md). My screenshots show the response-header fields visible in DevTools; I have not yet completed a full security-header review.

## ZAP
I have not added ZAP evidence yet.

## Evidence handling
The Chrome screenshot includes a Set-Cookie/JSESSIONID response. I am checking that the session value is not readable in the public image. A cookie value is not needed to demonstrate its attributes, so I will keep it redacted.
