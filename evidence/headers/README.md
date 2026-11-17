# HTTP Response Header Evidence

## Existing evidence
- [Chrome HTTP capture](../browser/HTTP%20homepage%20and%20response%20headers.jpeg) — 30 October 2026; response details include Content-Type, Date, Server, Set-Cookie and Transfer-Encoding.
- [Firefox HTTP capture](../browser/firefox_browser_check_2026-11-08%20210612.png) — 8 November 2026; response-header panel shows Content-Type, Date, Server and Transfer-Encoding.

## Important interpretation
The Firefox screenshot's four visible response headers do not prove that every other security header is absent from all responses. The Chrome General panel's Referrer Policy field is not proof that a `Referrer-Policy` response header was sent.

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
