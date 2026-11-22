# HTTP Response Header Evidence

## Evidence captured

- [Firefox HTTP capture](../browser/firefox-http-response-2026-11-08.png) — 8 November 2026; the response-header panel shows Content-Type, Date, Server and Transfer-Encoding.
- [Raw response-header transcription](raw-response-headers-2026-11-08.txt) — the four headers transcribed from the Firefox raw-header screenshot.
- [ZAP homepage HTTP response](../zap/04-homepage-http-response.png) — 22 November 2026; shows the homepage `200 OK` response, server banner, content type and a redacted JSESSIONID value with Path and HttpOnly attributes.

The original Chrome DevTools screenshot from 30 October 2026 was removed from the current public file tree because its session identifier was readable. The final report contains a separate cropped homepage image on page 4; the removed DevTools capture should not be re-uploaded.

## What the evidence supports

The Firefox raw response capture shows:
- `HTTP/1.1 200 OK`
- `Server: Apache-Coyote/1.1`
- `Content-Type: text/html;charset=ISO-8859-1`
- `Transfer-Encoding: chunked`
- `Date: Sun, 08 Nov 2026 21:17:02 GMT`

The separate ZAP response capture from 22 November shows a JSESSIONID cookie with `Path=/` and `HttpOnly`; the value is redacted. ZAP's passive alert review also identified missing CSP, anti-clickjacking protection and X-Content-Type-Options on sampled responses, plus a SameSite cookie attribute observation. See the [findings register](../../findings/findings-register.md) for confidence, risk and limitations.

A response-header capture only describes the response shown. It does not establish that every header is absent from every route or response. HSTS is not assessed from an HTTP response; it requires an appropriate HTTPS response.

## Interpretation limits

The Firefox header capture is historical and was made over HTTP, not HTTPS. It does not show every common security header. The Chrome General panel's Referrer Policy field is not, by itself, proof that a `Referrer-Policy` response header was sent.

Cookie values and session identifiers must not be published. Keep the JSESSIONID value redacted in all evidence.
