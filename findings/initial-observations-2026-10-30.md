# Initial Observations — 30 October 2026

**Status:** Preliminary browser observations. No vulnerability has yet been confirmed.

## 1. HTTP browser baseline

**Evidence:** [HTTP homepage and response headers](<../evidence/HTTP homepage and response headers.jpeg>) — redacted Chrome DevTools screenshot of the Testfire homepage and main document response headers. The screenshot is stored in the repository's evidence folder; the session-cookie value has been redacted.

- Requested URL: http://testfire.net/
- Request method: GET
- HTTP status: 200 OK
- Remote address shown: 65.61.137.117:80
- Referrer-Policy: strict-origin-when-cross-origin
- Content-Type: text/html; charset=ISO-8859-1
- Server header: Apache-Coyote/1.1
- Set-Cookie response shown: JSESSIONID with HttpOnly and Path=/.
- Secure and SameSite attributes were not visible in the supplied screenshot; confirm with a fresh capture before treating this as a finding.

### Interpretation

- 200 OK means the server returned a successful response to that HTTP request. It does not mean the application is secure.
- The browser's "Not secure" indicator is consistent with the page being loaded over unencrypted HTTP.
- Apache-Coyote/1.1 is the exact Server header value observed. Do not infer a specific software release from this string alone.
- HttpOnly is visible for the JSESSIONID cookie. The public evidence screenshot is a redacted replacement; do not publish any unredacted copy containing cookie or session values.
- Do not infer that a header is absent from the entire site based on one response.

## 2. HTTPS browser observation

**Evidence:** [HTTPS certificate warning](../evidence/https-certificate-warning.png).

- Chrome displayed "Your connection is not private".
- Error code shown: NET::ERR_CERT_AUTHORITY_INVALID.
- Chrome's message stated that the certificate was not trusted by the computer's operating system.

### Interpretation

This is evidence that Chrome could not establish trust in the certificate authority/chain in that browsing environment. This error alone does not prove that the certificate has expired. The certificate subject, issuer, validity dates, subject alternative names and chain need to be inspected before classifying the issue.

Do not bypass the browser warning or proceed to the unsafe site.

## 3. Potential checks — not confirmed findings

| Area | Evidence required |
|---|---|
| HTTP transport | Establish whether HTTP redirects to HTTPS. Record the behaviour; do not send credentials or sensitive data. |
| TLS certificate | Inspect subject, issuer, validity period, hostnames and trust-chain result. |
| Security headers | Capture the complete response-header list for relevant public HTML responses. |
| Server banner | Confirm the Server header and determine whether it reveals meaningful version information. |
| Cookie attributes | Capture Set-Cookie attributes with the cookie value redacted; check Secure, HttpOnly and SameSite. |
| Client-side resources | Identify relevant third-party scripts/styles and assess whether Subresource Integrity is applicable. |

## 4. Next steps

1. Inspect the HTTPS certificate details without bypassing browser warnings.
2. Review public pages manually while OWASP ZAP passive scanning observes ordinary browser traffic.
3. Validate each observation and document only evidence-backed findings.

## 5. Scope decisions and limitations

- **Nmap is not authorised for this assessment.** No port or service scanning will be performed against Testfire, and no Nmap results will be included in the report.
- These observations are based on browser evidence supplied by the assessor and have not yet been independently reproduced in this report.
- The HTTPS certificate chain and validity dates have not yet been captured.
- The full set of response headers has not yet been verified.
- No Nmap scan, ZAP active scan, login attempt, form submission, exploitation, brute force or denial-of-service test is recorded here.
- Absence of a finding does not prove the website is secure.
