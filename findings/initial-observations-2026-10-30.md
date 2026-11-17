# Initial Observations — 30 October and 8 November 2026

**Status:** Historical browser observations. They are not a current availability test and do not establish confirmed vulnerabilities.

## 1. HTTP homepage response — 30 October 2026

**Evidence:** [Chrome HTTP homepage and response headers](../evidence/browser/http-response-headers-2026-10-30.jpeg)

The supplied Chrome DevTools screenshot records:
- Requested URL: `http://testfire.net/`
- Method: `GET`
- Status: `200 OK`
- Remote address: `65.61.137.117:80`
- Response Content-Type: `text/html; charset=ISO-8859-1`
- Server: `Apache-Coyote/1.1`
- Transfer-Encoding: `chunked`
- A `JSESSIONID` cookie with `HttpOnly` and `Path=/` visible.

The Chrome General panel also shows a Referrer Policy value. That panel value is not, by itself, proof that a `Referrer-Policy` response header was sent.

**Privacy:** Check the screenshot before public reuse. If the JSESSIONID value is readable, redact it and replace the public copy. Never publish a live session identifier.

## 2. HTTPS certificate warning — 30 October 2026

**Evidence:** [Chrome HTTPS certificate warning](../evidence/tls/certificate-warning-2026-10-30.png)

Chrome displayed “Your connection is not private” and `NET::ERR_CERT_AUTHORITY_INVALID` for `https://testfire.net/`. The page states that the certificate was not trusted by the computer's operating system.

This supports the observation that Chrome did not trust the certificate authority/chain in that browser environment at that time. It does **not** prove that the certificate was expired. The certificate subject, issuer, validity dates, SANs and chain verification result have not been captured.

Do not bypass the warning or proceed through the unsafe-site interstitial.

## 3. HTTP response — 8 November 2026

**Evidence:** [Firefox browser check](../evidence/browser/firefox-http-response-2026-11-08.png) and [raw response-header transcription](../evidence/headers/raw-response-headers-2026-11-08.txt).

The Firefox DevTools screenshot records:
- Host: `testfire.net`
- Filename: `/`
- Address: `65.61.137.117:80`
- Status: `200 OK`
- Protocol: `HTTP/1.1`
- Response headers shown: `Content-Type`, `Date`, `Server`, `Transfer-Encoding`.

The raw screenshot shows:
```http
HTTP/1.1 200 OK
Server: Apache-Coyote/1.1
Content-Type: text/html;charset=ISO-8859-1
Transfer-Encoding: chunked
Date: Sun, 08 Nov 2026 21:17:02 GMT
```

Only the four visible response headers have been transcribed. This is not proof that other headers are absent from every response or route.

## 4. What can and cannot be concluded
- The hosted HTTP page responded with `200 OK` on 30 October and again on 8 November 2026.
- The supplied HTTPS attempt produced a certificate-authority trust warning on 30 October.
- These screenshots do not tell us whether the site is reachable today.
- A certificate warning alone does not establish expiry, hostname mismatch or a specific certificate misconfiguration.
- A generic `Apache-Coyote/1.1` banner does not prove a vulnerable server version.
- A header not visible in a partial screenshot is not automatically proven absent.
- An unavailable target is an assessment limitation, not a vulnerability.

## 5. Next steps
1. Check `testfire.net` and `demo.testfire.net` separately; record exact host, scheme, timestamp and result.
2. If HTTP responds, capture redirect behaviour and complete response headers from one normal public GET.
3. If HTTPS is safely inspectable, record certificate subject, issuer, validity, SANs and chain result. Do not bypass browser warnings.
4. Redact session identifiers from all screenshots and text files.
5. Update the findings register only when evidence supports a conclusion.
