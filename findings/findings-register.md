# Findings Register

**Target:** `http://testfire.net/`  
**Latest evidence:** OWASP ZAP passive observation, 22 November 2026  
**Assessment status:** Evidence captured; findings remain subject to final report review.

ZAP displayed 16 alert categories. This does not mean 16 confirmed vulnerabilities. The register below combines related alerts where they describe the same underlying observation and distinguishes observed configuration weaknesses from alerts that remain unverified.

## Risk interpretation

The ZAP risk rating is shown separately from the proposed report priority. The proposed priority considers the evidence, ZAP confidence and limited read-only scope. No exploitability testing was performed.

| ID | Observation | ZAP risk / confidence | Proposed report rating | Status |
|---|---|---|---|---|
| F-01 | Content-Security-Policy response header not set on sampled responses | Medium / High | Medium | Observed by passive response analysis |
| F-02 | Anti-clickjacking protection not identified on the homepage response | Medium / Medium | Medium | Observed by passive response analysis |
| F-03 | External JavaScript reference without Subresource Integrity | Medium / High for SRI; Low / Medium for cross-domain inclusion | Medium | Script reference observed; successful third-party delivery not established |
| F-04 | JSESSIONID cookie reported without SameSite | Low / Medium | Low | Attribute observation on sampled response |
| F-05 | Server header identifies `Apache-Coyote/1.1` | Low / High | Low | Header observed; no vulnerable version established |
| F-06 | `X-Content-Type-Options: nosniff` not set on sampled CSS response | Low / Medium | Low | Observed by passive response analysis |
| O-01 | Possible absence of anti-CSRF tokens in login and subscription forms | Medium / Low | Unconfirmed | Passive HTML observation only; no submission or behaviour test |
| O-02 | Generic `Internal server error` response at Swagger properties path | Low / Medium | Informational / unconfirmed | Visible evidence is generic and contains no detailed diagnostic data |

## Finding details

### F-01 — Content-Security-Policy header not set
**Evidence:** [ZAP CSP alert](../evidence/zap/06-content-security-policy-alert.png)

ZAP reported that a Content-Security-Policy header was not set and marked the alert systemic. The alert lists sampled Testfire responses. A CSP helps restrict the origins from which browser content may be loaded and can reduce the impact of certain content-injection attacks.

**Recommendation:** Define and deploy a suitable Content-Security-Policy for the application. Start with report-only monitoring where appropriate, review required scripts/styles/resources, then enforce a restrictive policy. Avoid broad unsafe directives unless a documented application requirement exists.

### F-02 — Anti-clickjacking protection not identified
**Evidence:** [ZAP anti-clickjacking alert](../evidence/zap/07-anti-clickjacking-header-alert.png)

ZAP reported that the homepage response did not include an identified `X-Frame-Options` header or an appropriate CSP `frame-ancestors` directive. This may allow the page to be framed by another site.

**Recommendation:** Set an appropriate `Content-Security-Policy: frame-ancestors` directive. Where needed for legacy browser support, configure `X-Frame-Options` consistently.

### F-03 — External JavaScript reference without Subresource Integrity
**Evidence:** [ZAP SRI alert](../evidence/zap/08-subresource-integrity-alert.png) and [cross-domain JavaScript alert](../evidence/zap/10-cross-domain-javascript-alert.png)

The observed page markup references `http://demo-analytics.testfire.net/urchin.js` from a different host and ZAP reported no `integrity` attribute. These two alerts relate to the same external script reference and are treated as one finding to avoid double-counting. The History screenshot shows a failed response for the external request, so successful script delivery was not established in this capture.

**Recommendation:** Remove unnecessary third-party scripts. For required static third-party resources, use HTTPS and a verified Subresource Integrity hash with the appropriate cross-origin configuration. Review and restrict approved script sources.

### F-04 — JSESSIONID cookie reported without SameSite
**Evidence:** [ZAP SameSite alert](../evidence/zap/09-samesite-cookie-alert.png) and [homepage HTTP response](../evidence/zap/04-homepage-http-response.png)

ZAP reported that the JSESSIONID cookie was set without a SameSite attribute. The response screenshot shows the cookie value redacted and the `Path=/` and `HttpOnly` attributes visible.

**Recommendation:** Set an appropriate `SameSite=Lax` or `SameSite=Strict` attribute based on application requirements. Review the use of `Secure` and ensure session cookies are only transmitted over HTTPS.

### F-05 — Server banner disclosure
**Evidence:** [ZAP server-header alert](../evidence/zap/13-server-header-disclosure-alert.png) and [homepage HTTP response](../evidence/zap/04-homepage-http-response.png)

The response includes `Server: Apache-Coyote/1.1`. This reveals a server technology identifier. It does not establish a specific software release or prove that the server is vulnerable.

**Recommendation:** Configure the server or application gateway to suppress the banner or return a generic value. Keep server components patched and maintained.

### F-06 — X-Content-Type-Options header missing
**Evidence:** [ZAP X-Content-Type-Options alert](../evidence/zap/14-x-content-type-options-alert.png)

ZAP reported that the observed CSS response did not set `X-Content-Type-Options: nosniff`.

**Recommendation:** Configure the application to send `X-Content-Type-Options: nosniff` on appropriate responses and ensure the correct Content-Type is returned.

## Observations not treated as confirmed findings

### O-01 — Possible absence of anti-CSRF tokens
**Evidence:** [ZAP anti-CSRF alert](../evidence/zap/05-anti-csrf-token-alert.png)

ZAP did not identify a recognised anti-CSRF token in the inspected login and subscription form markup. The alert confidence is Low. No form was submitted and no request behaviour was tested. This is not sufficient to conclude that the application is vulnerable to CSRF; another control or token mechanism may exist.

**Recommended follow-up for an authorised, separately scoped review:** Confirm the application's intended CSRF protection design and validate it only with explicit authorisation. For this read-only assessment, retain the observation as unverified.

### O-02 — Generic internal server error
**Evidence:** [ZAP debug-error alert](../evidence/zap/11-debug-error-message-alert.png) and [detail view](../evidence/zap/12-debug-error-message-detail.png)

ZAP flagged the text `Internal server error` at `/swagger/properties.json`. The screenshots do not show a stack trace, source path, database detail or other sensitive diagnostic information. The alert is therefore not treated as a confirmed information-disclosure vulnerability.

**Recommendation:** Return generic error messages to users and retain detailed diagnostics in access-controlled server-side logs. Review server logs through an authorised administrative process.

## Alerts excluded from the findings count

- **Strict-Transport-Security not set:** Not assessed as a finding from the HTTP response capture alone; an appropriate HTTPS response is needed.
- **Suspicious comments:** The alert details were not reviewed sufficiently to establish a security impact.
- **Modern Web Application, Session Management Response Identified, Apache Tomcat, Java and Swagger UI:** Technology or application characteristics, not vulnerabilities by themselves.

## Assessment limitations

- The assessment was limited to public-facing pages and passive browser-generated traffic.
- No forms were submitted and no authentication workflow was tested.
- No active scanning, spidering, fuzzing, exploitation, brute force, DoS or Nmap scan was performed.
- Third-party hosts visible in ZAP were not independently assessed.
- The findings describe the responses and pages observed on 22 November 2026; they are not a guarantee of the application's current or future configuration.
