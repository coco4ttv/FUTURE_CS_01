# Initial Observations — 30 October and 8 November 2026

**Status:** Historical browser observations. They are not a current availability test and do not establish confirmed vulnerabilities.

## 1. HTTP homepage response — 30 October 2026

**Evidence:** The original Chrome DevTools capture recorded `GET http://testfire.net/` with `200 OK`. It also showed `Apache-Coyote/1.1`, the HTML content type and a JSESSIONID cookie. The original screenshot has been removed from the current public file tree because its session identifier was readable. Do not re-upload that unredacted screenshot. A cropped public homepage image is included on page 4 of the [final assessment report](../report/FUTURE_CS_01_Vulnerability_Assessment_Report.pdf).

The historical capture recorded:
- Requested URL: `http://testfire.net/`
- Method: `GET`
- Status: `200 OK`
- Remote address: `65.61.137.117:80`
- Response Content-Type: `text/html; charset=ISO-8859-1`
- Server: `Apache-Coyote/1.1`
- Transfer-Encoding: `chunked`
- A JSESSIONID cookie with `HttpOnly` and `Path=/` visible.

The Chrome General panel also showed a Referrer Policy value. That panel value is not, by itself, proof that a `Referrer-Policy` response header was sent. It is not recorded as a confirmed response header.

## 2. HTTPS certificate warning — 30 October 2026

**Evidence:** [Chrome HTTPS certificate warning](../evidence/tls/certificate-warning-2026-10-30.png)

Chrome displayed “Your connection is not private” and `NET::ERR_CERT_AUTHORITY_INVALID` for `https://testfire.net/`. The page stated that the certificate was not trusted by the computer's operating system.

This supports the observation that Chrome did not trust the certificate authority/chain in that browser environment at that time. It does **not** prove that the certificate was expired. The certificate subject, issuer, validity dates, SANs and chain verification result have not been captured.

The warning was not bypassed.

## 3. HTTP response — 8 November 2026

**Evidence:** [Firefox HTTP response capture](../evidence/browser/firefox-http-response-2026-11-08.png) and [raw response-header transcription](../evidence/headers/raw-response-headers-2026-11-08.txt).

The Firefox DevTools screenshot records:
- Host: `testfire.net`
- Filename: `/`
- Address: `65.61.137.117:80`
- Status: `200 OK`
- Protocol: `HTTP/1.1`
- Response headers shown: `Content-Type`, `Date`, `Server`, `Transfer-Encoding`.

The raw response-header transcription records those same four headers. It does not show CSP, X-Frame-Options, X-Content-Type-Options, HSTS or other common security headers. Because the capture is historical and does not show every response or route, treat those headers as **not evidenced in this capture**, not as proven absent from the whole site.

## 4. What can and cannot be concluded

- The hosted HTTP page responded with `200 OK` on 30 October and again on 8 November 2026.
- The supplied HTTPS attempt produced a certificate-authority trust warning on 30 October.
- These screenshots do not tell us whether the site is reachable today.
- A certificate warning alone does not establish expiry, hostname mismatch or a specific certificate misconfiguration.
- A generic `Apache-Coyote/1.1` banner does not prove a vulnerable server version.
- A header not visible in a partial screenshot is not automatically proven absent.
- An unavailable target is an assessment limitation, not a vulnerability.

## 5. Related passive evidence

The 22 November 2026 ZAP response and alert screenshots are indexed in [OWASP ZAP evidence](../evidence/zap/README.md). That review was performed in Safe Mode and is described in the [findings register](findings-register.md).
