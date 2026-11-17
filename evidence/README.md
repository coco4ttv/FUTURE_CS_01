# Evidence Index

Evidence is grouped by assessment area. Record the exact hostname, scheme and capture time for every item.

## Browser — HTTP
- [Chrome HTTP homepage and response headers — 30 October](browser/http-response-headers-2026-10-30.jpeg) — `GET http://testfire.net/`, `200 OK`, remote address `65.61.137.117:80`.
- [Firefox HTTP browser check — 8 November](browser/firefox-http-response-2026-11-08.png) — `GET http://testfire.net/`, `200 OK`, remote address `65.61.137.117:80`.

## TLS
- [Chrome certificate warning — 30 October](tls/certificate-warning-2026-10-30.png) — Chrome displayed `NET::ERR_CERT_AUTHORITY_INVALID` for `https://testfire.net/`.
- No certificate export, chain validation or OpenSSL output has been captured.

## HTTP headers
- [Raw response-header transcription — 8 November](headers/raw-response-headers-2026-11-08.txt) — transcribed from the supplied Firefox DevTools raw-header screenshot.
- The browser captures show selected headers, not a complete audit of every route or response.

## ZAP
The `zap/` directory is reserved for passive-mode evidence. No ZAP evidence is currently recorded.

## Evidence handling
Never publish passwords, authentication tokens, session-cookie values, personal data or browser storage. Check the 30 October Chrome screenshot for readable JSESSIONID material before public reuse; if visible, redact the image and replace the public copy.
