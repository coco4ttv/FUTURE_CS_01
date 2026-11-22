# Findings Register

**Target:** `http://testfire.net/`  
**Latest ZAP evidence:** 22 November 2026  
**Assessment type:** Limited read-only review; passive observation only

ZAP displayed 16 alert categories. This is not 16 confirmed vulnerabilities. Related alerts for the same underlying observation are grouped to avoid double-counting. The table separates ZAP's own risk/confidence from the proposed business-facing report priority.

## Risk rating approach

- **Medium:** A meaningful security-control weakness or customer-facing trust issue that merits planned remediation or investigation.
- **Low:** A limited standalone exposure or information disclosure with no demonstrated exploit or compromise.
- **Unconfirmed observation:** Evidence is not sufficient to assert that a vulnerability exists.

These are qualitative priorities for this limited assessment, not CVSS scores. No exploitability testing was performed.

| ID | Observation | ZAP risk / confidence | Proposed priority | Status |
|---|---|---|---|---|
| F-01 | Content-Security-Policy response header not set on sampled responses | Medium / High | Medium | Passive observation |
| F-02 | Anti-clickjacking protection not identified on the homepage response | Medium / Medium | Medium | Passive observation |
| F-03 | External JavaScript reference without Subresource Integrity | Medium / High for SRI; Low / Medium for cross-domain inclusion | Medium | Script reference observed; successful third-party delivery not established |
| F-04 | JSESSIONID cookie reported without SameSite | Low / Medium | Low | Cookie attribute observation |
| F-05 | Server header identifies `Apache-Coyote/1.1` | Low / High | Low | Header observed; no vulnerable version established |
| F-06 | `X-Content-Type-Options: nosniff` not set on sampled CSS response | Low / Medium | Low | Passive observation |
| O-01 | Possible absence of anti-CSRF tokens in login and subscription form markup | Medium / Low | Unconfirmed | No form submitted; behaviour not tested |
| O-02 | Generic `Internal server error` response at Swagger properties path | Low / Medium | Informational / unconfirmed | No sensitive diagnostic details visible |
| O-03 | Chrome HTTPS certificate trust warning | Browser error `NET::ERR_CERT_AUTHORITY_INVALID` | Medium investigation priority | Root cause unconfirmed; not counted as a confirmed vulnerability |

## F-01 — Content-Security-Policy header not set

**Evidence:** [ZAP CSP alert](../evidence/zap/06-content-security-policy-alert.png)

**What was observed:** ZAP reported that a Content-Security-Policy (CSP) response header was not set and marked the alert systemic across sampled responses.

**What this means in plain English:** A CSP is a set of browser instructions that tells a page which locations it is allowed to load scripts, styles and other resources from. Without it, the browser has fewer restrictions if unwanted code is ever introduced into a page.

**Why a business should care:** If another weakness allowed malicious code to appear on a customer-facing page, the lack of a CSP could increase the potential impact on visitors, customer trust and incident-response costs. This assessment did not find or test a code-injection flaw.

**Proposed priority:** Medium.

**Recommended fix:** Inventory the legitimate resource sources. Introduce a suitable CSP in report-only mode, review violations and application dependencies, then enforce a least-privilege policy. Avoid broad unsafe directives unless there is a documented application requirement.

**Guidance:** OWASP Content Security Policy Cheat Sheet — https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html

## F-02 — Anti-clickjacking protection not identified

**Evidence:** [ZAP anti-clickjacking alert](../evidence/zap/07-anti-clickjacking-header-alert.png)

**What was observed:** ZAP reported that the sampled homepage response did not include an identified `X-Frame-Options` header or CSP `frame-ancestors` directive.

**What this means in plain English:** These controls tell a browser whether another website is allowed to display the page inside a frame. Without a framing restriction, a page may be embedded elsewhere.

**Why a business should care:** A malicious page could potentially place an important page or button inside a misleading frame and trick a visitor into clicking it. If sensitive actions were exposed this way, customers and the business could be affected. No clickjacking attempt was performed and no impact was demonstrated.

**Proposed priority:** Medium.

**Recommended fix:** Configure CSP with a restrictive `frame-ancestors` directive. Where legacy browser compatibility is required, also configure an appropriate `X-Frame-Options` value. Validate legitimate embedding requirements before enforcing the policy.

**Guidance:** OWASP Clickjacking Defense Cheat Sheet — https://cheatsheetseries.owasp.org/cheatsheets/Clickjacking_Defense_Cheat_Sheet.html

## F-03 — External JavaScript reference without Subresource Integrity

**Evidence:** [ZAP SRI alert](../evidence/zap/08-subresource-integrity-alert.png) and [cross-domain JavaScript alert](../evidence/zap/10-cross-domain-javascript-alert.png)

**What was observed:** Page markup references `http://demo-analytics.testfire.net/urchin.js` from a different host without an `integrity` attribute. ZAP produced both an SRI alert and a cross-domain JavaScript alert for the same reference; they are treated as one observation. ZAP History shows a failed response for the external analytics request, so successful script delivery or execution was not established in this capture.

**What this means in plain English:** Subresource Integrity (SRI) lets a browser check that a downloaded script matches an expected hash. Without that check, the browser has no hash on this script tag to detect an unexpected file change.

**Why a business should care:** If a third-party script host or file were changed by an attacker, the website could potentially load altered code that affects what visitors see or do. The captured history shows the external request failed, so this assessment did not observe the script executing.

**Proposed priority:** Medium.

**Recommended fix:** Remove unnecessary third-party scripts. For required static resources, use HTTPS and a verified SRI hash with the correct `crossorigin` configuration. Review and restrict approved script origins.

**Guidance:** MDN Subresource Integrity — https://developer.mozilla.org/en-US/docs/Web/Security/Defenses/Subresource_Integrity

## F-04 — JSESSIONID cookie reported without SameSite

**Evidence:** [ZAP SameSite alert](../evidence/zap/09-samesite-cookie-alert.png) and [homepage HTTP response](../evidence/zap/04-homepage-http-response.png)

**What was observed:** ZAP reported that the JSESSIONID cookie was set without a SameSite attribute. The sampled response showed `Path=/` and `HttpOnly`; the session value is redacted.

**What this means in plain English:** SameSite helps control when a browser sends a site's session cookie along with requests started from another website. It provides an additional layer of protection against some cross-site request scenarios.

**Why a business should care:** If a separate request-forgery weakness existed, a browser sending the session cookie in a cross-site situation could make unintended actions easier. This review did not test or confirm that scenario. SameSite is an additional control, not a replacement for a proper CSRF defence.

**Proposed priority:** Low.

**Recommended fix:** Set `SameSite=Lax` or `SameSite=Strict` according to the application's legitimate cross-site flows. Review the `Secure` attribute and ensure session cookies are only transmitted over HTTPS. Keep `HttpOnly` enabled.

**Guidance:** OWASP Session Management Cheat Sheet — https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html

## F-05 — Server banner disclosure

**Evidence:** [ZAP server-header alert](../evidence/zap/13-server-header-disclosure-alert.png) and [homepage HTTP response](../evidence/zap/04-homepage-http-response.png)

**What was observed:** The sampled response included `Server: Apache-Coyote/1.1`.

**What this means in plain English:** The server response gives visitors a clue about the technology used to run the website. It does not identify an exact software release or prove that the server is vulnerable.

**Why a business should care:** This small amount of information may help an outsider focus research on the software in use. On its own, it does not show that the website can be compromised.

**Proposed priority:** Low.

**Recommended fix:** Suppress the server banner or replace it with generic information where supported. Keep the server stack supported and patched, and track exact component versions internally.

**Guidance:** OWASP HTTP Headers Cheat Sheet — https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Headers_Cheat_Sheet.html

## F-06 — X-Content-Type-Options header missing

**Evidence:** [ZAP X-Content-Type-Options alert](../evidence/zap/14-x-content-type-options-alert.png)

**What was observed:** ZAP reported that the sampled CSS response did not set `X-Content-Type-Options: nosniff`.

**What this means in plain English:** The `nosniff` setting tells a browser to respect the content type declared by the website rather than trying to guess a different type.

**Why a business should care:** In some circumstances, browsers guessing a content type incorrectly can increase exposure if untrusted content is served with a misleading type. No content-type confusion or exploit was demonstrated here.

**Proposed priority:** Low.

**Recommended fix:** Configure the application to send `X-Content-Type-Options: nosniff` on appropriate responses and ensure each resource has the correct `Content-Type`.

**Guidance:** OWASP HTTP Headers Cheat Sheet — https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Headers_Cheat_Sheet.html

## O-01 — Possible absence of anti-CSRF tokens

**Evidence:** [ZAP anti-CSRF alert](../evidence/zap/05-anti-csrf-token-alert.png)

ZAP did not identify a recognised anti-CSRF token in inspected login and subscription form markup. The alert confidence is Low. No form was submitted and no request behaviour was tested. Another protection mechanism may exist, so this is not treated as a confirmed CSRF vulnerability.

**Business meaning:** If no effective CSRF protections existed, a user who was signed in could potentially be tricked into causing an unintended action. This assessment did not establish that the application is vulnerable.

**Recommendation:** The application owner should verify its CSRF design in an explicitly authorised review. OWASP recommends framework-provided CSRF protection or validated anti-CSRF tokens for state-changing requests, with SameSite used as an additional layer.

**Guidance:** OWASP CSRF Prevention Cheat Sheet — https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html

## O-02 — Generic internal server error

**Evidence:** [ZAP debug-error alert](../evidence/zap/11-debug-error-message-alert.png) and [detail view](../evidence/zap/12-debug-error-message-detail.png)

ZAP flagged the text `Internal server error` at `/swagger/properties.json`. The screenshot does not show a stack trace, source path, database detail or other sensitive diagnostic information. This remains informational/unconfirmed.

**Business meaning:** The response indicates that the requested resource produced a server error at that time, but does not show sensitive technical details. A generic error alone is not evidence of a data leak.

**Recommendation:** Return generic error messages to users and keep detailed diagnostics in access-controlled server-side logs. Review the server logs through an authorised administrative process.

## O-03 — HTTPS certificate trust warning; root cause unconfirmed

**Evidence:** Historical Chrome browser capture, 30 October 2026, showing `NET::ERR_CERT_AUTHORITY_INVALID`.

Chrome displayed a browser trust warning for `https://testfire.net/` and stated that the certificate was not trusted by the computer's operating system. This proves that this browser did not trust the presented certificate chain in that environment at that time. It does not establish whether the certificate was expired, mis-issued, self-signed, intercepted or affected by a local trust-store issue.

**Business meaning:** Visitors may abandon the site when a browser warns that it cannot verify the site's identity. This can reduce customer confidence and transactions. The screenshot does not demonstrate that anyone intercepted traffic.

**Proposed priority:** Medium investigation priority; not a confirmed vulnerability until the certificate and chain are inspected.

**Recommended owner action:** Inspect the certificate and full chain on the server. Confirm that it is issued by a publicly trusted CA, covers `testfire.net` in its Subject Alternative Name, is within its validity dates and includes required intermediate certificates. Review renewal automation and re-test in a normal browser without bypassing the warning.

## Alerts excluded from the findings count

- **Strict-Transport-Security not set:** Not assessed from the HTTP capture alone; an appropriate HTTPS response is required.
- **Suspicious comments:** The alert details were not reviewed sufficiently to establish a security impact.
- **Modern Web Application, Session Management Response Identified, Apache Tomcat, Java and Swagger UI:** Technology or application characteristics, not vulnerabilities by themselves.
- Third-party hosts visible in ZAP were not independently assessed.

## Assessment limitations

- The review was limited to public-facing pages and passive browser-generated traffic.
- No forms were submitted and no authentication workflow was tested.
- No active scanning, spidering, fuzzing, exploitation, brute force, DoS or Nmap scan was performed.
- The separate AltoroJ Docker practice environment was not part of the Testfire assessment.
- Findings describe the sampled pages and responses captured on the dates recorded in the evidence; they are not a guarantee of the application's current or future configuration.
