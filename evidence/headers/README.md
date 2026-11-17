# HTTP Response Header Evidence

## Existing evidence
- [Chrome HTTP capture — 30 October](../browser/http-response-headers-2026-10-30.jpeg) — selected response details include Content-Type, Date, Server, Set-Cookie and Transfer-Encoding.
- [Firefox HTTP capture — 8 November](../browser/firefox-http-response-2026-11-08.png) — DevTools shows Content-Type, Date, Server and Transfer-Encoding.
- [Raw header transcription — 8 November](raw-response-headers-2026-11-08.txt) — transcribed from the supplied raw response-header screenshot.

## Important interpretation
The four headers visible in the Firefox capture do not prove every other security header is absent from all responses. The Chrome General panel's Referrer Policy field is not proof that a `Referrer-Policy` response header was sent.

## Checks to complete
For a reachable public page, capture the complete raw response headers and check:
- `Strict-Transport-Security`
- `Content-Security-Policy`
- `X-Content-Type-Options`
- `X-Frame-Options` (or an appropriate CSP frame-ancestors directive)
- `Referrer-Policy`
- `Permissions-Policy`
- `Set-Cookie` attributes: Secure, HttpOnly and SameSite

Record each as Present, Absent in this response, or Not assessed. Do not record cookie values. Include the exact URL, date/time and status code.
