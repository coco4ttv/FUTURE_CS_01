# Initial Observations — 30 October 2026

**Status:** Preliminary observations only. None of the items below is yet a confirmed vulnerability finding.

## A. Browser baseline — HTTP

Source: assessor-provided Chrome DevTools screenshot of the main document request.

- Requested URL: http://testfire.net/
- Request method: GET
- HTTP status: 200 OK
- Referrer-Policy: strict-origin-when-cross-origin
- Content-Type: text/html; charset=ISO-8859-1
- Server header: Apache-Coyote/1.1
- Set-Cookie response shown: JSESSIONID with HttpOnly and Path=/.
- The screenshot did not show Secure or SameSite attributes for that cookie. Confirm with a fresh, sanitised capture before treating this as a finding.
- No conclusion should be drawn about the entire site from this single main-document response.

**Evidence handling:** The original screenshot visibly contains a session-cookie value. Do not publish that original image. Capture a new screenshot with the cookie value redacted; only the attributes are relevant.

## B. Browser baseline — HTTPS certificate warning

Source: assessor-provided Chrome screenshot after navigating to https://testfire.net/.

- Chrome displayed “Your connection is not private”.
- Error code shown: NET::ERR_CERT_AUTHORITY_INVALID.
- Chrome's message states that the certificate is not trusted by the computer's operating system.

**Interpretation:** This is evidence that the browser could not validate the certificate's trust chain in that browsing environment. This error alone does not establish that the certificate has expired. Possible causes include an untrusted issuer or incomplete certificate chain, and environment-specific trust/interception issues. Record the certificate's subject, issuer, validity dates and chain before assigning a certificate finding.

**Safety:** Do not bypass the warning or proceed through the unsafe interstitial for this assessment.

## C. Third-party scanner output — Aikido

Source: assessor-provided Aikido domain page for http://testfire.net. It displayed five issues:

1. Content Security Policy (CSP) header not set — Critical (Aikido label)
2. Domain SSL Certificate Expiration — High (Aikido label)
3. Missing anti-clickjacking header — Medium (Aikido label)
4. Server leaks version info via the Server HTTP header — Medium (Aikido label)
5. Subresource Integrity attribute missing — Low (Aikido label)

These are **scanner-reported leads**, not yet independently verified findings. Aikido's severity labels must not be copied directly into the internship report without evidence and an impact assessment. The displayed SSL-expiration label must be reconciled with the browser certificate details; NET::ERR_CERT_AUTHORITY_INVALID does not itself mean “expired”.

Before using any Aikido result:
- Open each issue's detail view and record its exact evidence, affected URL/resource, and check description.
- Do not start another scan, active scan, crawl, exploit, fuzz or attack feature.
- Establish what checks the scan already performed and whether they stayed within the assignment's read-only scope.
- If the check methodology cannot be established, cite the Aikido results only as external leads, not as assessment evidence.

## D. Provisional finding candidates (not yet confirmed)

| Candidate | Evidence needed before confirmation |
|---|---|
| HTTPS certificate trust/chain problem | Certificate viewer details: subject/SAN, issuer, validity dates, chain; repeat from a second trusted environment only if appropriate |
| HTTP transport exposure | Verify whether the HTTP site redirects to HTTPS; confirm whether sensitive functions/data are in scope (they are currently excluded) |
| Missing security headers | Capture complete headers for relevant public HTML responses and identify which headers are absent |
| Server banner disclosure | Confirm the header on a fresh response and assess whether it reveals actionable version detail |
| Cookie flags | Freshly inspect Set-Cookie attributes with cookie value redacted |
| Missing SRI | Identify specific third-party scripts/styles lacking integrity attributes; assess applicability and risk |


