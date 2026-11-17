# HTTP Response Header Evidence

## Evidence captured

- [Chrome HTTP capture](../browser/chrome_2026-10-30%20183814.png) — 30 October 2026; response details include Content-Type, Date, Server, Set-Cookie and Transfer-Encoding.
- [Firefox HTTP capture](../browser/firefox-http-response-2026-11-08.png) — 8 November 2026; the response-header panel shows Content-Type, Date, Server and Transfer-Encoding.
- [Raw response-header transcription](raw-response-headers-2026-11-08.txt) — text transcribed from the Firefox raw-header screenshot.

## What I can conclude so far

The Firefox screenshot shows four response headers. It does not establish that every other security header is absent from all responses or routes. The Chrome General panel's Referrer Policy field is not, by itself, proof that a `Referrer-Policy` response header was sent.

## Checks I have not completed

I have not yet captured a complete response-header set to check:
- `Strict-Transport-Security`
- `Content-Security-Policy`
- `X-Content-Type-Options`
- `X-Frame-Options` or an appropriate CSP `frame-ancestors` directive
- `Referrer-Policy`
- `Permissions-Policy`
- `Set-Cookie` attributes: Secure, HttpOnly and SameSite

I will record the exact URL, date/time and status code with any future capture. I will not include cookie values in the evidence.
