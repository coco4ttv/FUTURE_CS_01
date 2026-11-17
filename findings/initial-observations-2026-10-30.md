# Initial Observations — 30 October 2026

**Status:** Preliminary browser observations. Not independently revalidated. No vulnerability is confirmed by this note alone.

## 1. HTTP homepage response

**Evidence:** [HTTP homepage and response headers](../evidence/browser/HTTP%20homepage%20and%20response%20headers.jpeg)

The supplied Chrome DevTools screenshot records the following for the homepage request:

- Requested URL: `http://testfire.net/`
- Method: `GET`
- Status: `200 OK`
- Remote address shown: `65.61.137.117:80`
- Referrer-Policy: `strict-origin-when-cross-origin`
- Content-Type: `text/html; charset=ISO-8859-1`
- Server header: `Apache-Coyote/1.1`
- A `JSESSIONID` Set-Cookie response was visible with `HttpOnly` and `Path=/`.

The screenshot's cookie value is redacted. The supplied capture does not establish whether `Secure` or `SameSite` was present. Re-capture the full Set-Cookie attributes with the value removed before drawing a conclusion.

### Interpretation and limitations

- `200 OK` confirms only that this particular HTTP request received a successful response at the time of capture.
- The page was requested over HTTP, which is unencrypted in transit. Re-test whether the host redirects HTTP to HTTPS before documenting the site's current behaviour.
- `Apache-Coyote/1.1` is the observed header value; it does not, by itself, identify a specific vulnerable version.
- Do not generalise one response's headers to every route or page.

## 2. HTTPS certificate warning

**Evidence:** [HTTPS certificate warning](../evidence/browser/https-certificate-warning.png)

Chrome displayed “Your connection is not private” with error code `NET::ERR_CERT_AUTHORITY_INVALID`.

### Interpretation and limitations

This records that Chrome did not trust the certificate authority/chain in that browsing environment. It does not, by itself, prove that the certificate was expired. The certificate subject, issuer, validity dates, subject alternative names and chain verification result must be inspected before classifying this as a finding.

Do not bypass the warning or proceed through an unsafe-site interstitial.

## 3. Candidate checks — not confirmed findings

| Area | What must be verified |
|---|---|
| HTTP transport | Current HTTP response and redirect behaviour, without submitting data |
| TLS | Certificate subject, issuer, validity, hostname/SAN match and chain result |
| Security headers | Complete response headers for relevant public HTML responses |
| Server banner | Whether the observed banner is current and whether it discloses meaningful version detail |
| Cookies | Secure, HttpOnly and SameSite attributes, with cookie value redacted |
| Client-side resources | Whether relevant third-party resources are used and whether integrity controls are applicable |

## 4. Next steps

1. Check whether the public demo is reachable and record the exact timestamp, URL and error/status.
2. If reachable, inspect TLS certificate details without bypassing browser warnings.
3. Capture relevant response headers and cookie attributes with secrets redacted.
4. If reachable, browse public pages manually with OWASP ZAP passive mode only.
5. Update the findings register only when evidence supports a conclusion.

## 5. Scope and limitations

- Nmap port/service scanning is excluded and was not performed.
- No ZAP active scan, spider, crawler, API probing, login attempt, form submission, exploitation, brute force or denial-of-service test is documented here.
- These observations are based on the original supplied browser captures and have not been independently reproduced in this note.
- The TLS chain, complete response-header set and cookie attributes require further validation.
- An unavailable target is an assessment limitation, not itself a vulnerability finding.
- Absence of a finding does not prove the website is secure.
