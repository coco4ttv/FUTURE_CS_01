# Future Interns — Task 1: Read-Only Vulnerability Assessment

> **Status:** In progress. Historical HTTP responses and a browser TLS trust warning are documented. Current reachability remains uncertain; no vulnerability is confirmed yet.

## Target identity
- **Observed host:** `testfire.net`
- **OWASP online demo hostname:** `demo.testfire.net`
- **Application:** AltoroJ / Altoro Mutual
- **Assessment:** Read-only manual review and passive observation
- **Evidence dates:** 30 October and 8 November 2026

Keep the two hostnames distinct. The supplied browser captures show `testfire.net`; OWASP's AltoroJ documentation names `demo.testfire.net` as the online demo. Record the exact hostname and scheme for every test.

## Scope and safety
**In scope:** public non-authenticated pages, ordinary browser GET requests, HTTP/HTTPS redirect behaviour, response headers, redacted cookie attributes, TLS certificate details and OWASP ZAP passive observation of manually browsed pages only.

**Out of scope:** login attempts, account access, transactions, form submissions, API probing, crawling, spidering, fuzzing, ZAP active scanning, Nmap port/service scanning, exploitation, brute force and denial-of-service.

Do not bypass certificate warnings or proceed through an unsafe-site interstitial.

## Repository guide
| Directory | Purpose |
|---|---|
| `methodology/` | Scope, testing approach and tools |
| `evidence/browser/` | HTTP browser captures |
| `evidence/tls/` | Certificate and TLS evidence |
| `evidence/headers/` | HTTP response-header evidence |
| `evidence/zap/` | Passive ZAP evidence only |
| `findings/` | Observations, validation status and remediation |
| `report/` | Final PDF report |
| `references/` | Technical references |

## Evidence captured
- **30 October — HTTP:** Chrome DevTools shows `GET http://testfire.net/` returning `200 OK` from `65.61.137.117:80`. The capture shows `Apache-Coyote/1.1`, HTML content type, chunked transfer encoding and a JSESSIONID cookie with HttpOnly and Path attributes visible.
- **30 October — HTTPS:** Chrome displayed `NET::ERR_CERT_AUTHORITY_INVALID` for `https://testfire.net/`. This establishes a trust error in that browser environment, not expiry or the precise cause.
- **8 November — HTTP:** Firefox DevTools again shows `GET http://testfire.net/` returning `200 OK` from `65.61.137.117:80`. Four response headers are visible: Content-Type, Date, Server and Transfer-Encoding.
- The 8 November raw header capture is transcribed in [raw-response-headers-2026-11-08.txt](evidence/headers/raw-response-headers-2026-11-08.txt). It does not prove other headers are absent from every route or response.

See [Evidence Index](evidence/README.md), [TLS notes](evidence/tls/README.md), [Headers notes](evidence/headers/README.md), [Initial observations](findings/initial-observations-2026-10-30.md) and [Findings Register](findings/findings-register.md).

## Is Testfire down? — 17 November 2026
The latest checks are mixed:
- An external availability checker reported no HTTP 200 response from `demo.testfire.net` on 16 November. <https://www.websitedown.info/demo.testfire.net>
- The app's own status endpoint returns `HostStatus: OK`, but that is not proof the homepage works. <https://demo.testfire.net/util/serverStatusCheckService.jsp>
- Direct web retrieval today timed out for `https://testfire.net/` and returned a 502 for `https://demo.testfire.net/`. These are independent retrieval failures, not a definitive test from your browser/network.
- OWASP ZAP explicitly warns the online AltoroJ demo may be unavailable or broken and recommends local deployment for more consistent testing. <https://www.zaproxy.org/docs/testapps/altoroj/>

**Conclusion:** Yes, the hosted demo appears unreliable and may currently be unavailable, but do not claim both hostnames are universally down. The screenshots prove `testfire.net` HTTP worked on 8 November, not today. Check `testfire.net` and `demo.testfire.net` separately once and record the result. Do not keep retrying a failing service.

If it remains unavailable, use a local AltoroJ deployment as a separately labelled assessment target. Keep local evidence separate from the historical hosted evidence.

## Workflow
1. Confirm exact hostname and reachability; record timestamp and result.
2. Review only public pages and ordinary browser GET requests.
3. Capture HTTP redirects and complete response headers.
4. Inspect TLS certificate details only if safely available; do not bypass warnings.
5. If reachable, observe manually browsed traffic with ZAP passive mode only.
6. Record observations with evidence, impact, confidence, validation status and remediation.
7. Produce a concise PDF report and review it for unsupported claims and exposed secrets.

- [ ] Recheck `testfire.net` and `demo.testfire.net` separately
- [ ] Validate HTTP-to-HTTPS redirect behaviour
- [ ] Capture certificate subject, issuer, validity, SANs and chain result
- [ ] Capture complete response headers and redacted cookie attributes
- [ ] Capture ZAP passive observations, if reachable
- [ ] Validate and prioritise findings
- [ ] Export and review final PDF report

## Evidence handling
Never commit passwords, authentication tokens, session-cookie values, personal data or unredacted browser storage. Redact cookie values in screenshots. Use lowercase, hyphenated filenames with dates.

## Disclaimer
This is an educational assessment of a deliberately vulnerable demonstration application, not a real banking service. Results apply only to the host, time, scope and methods documented. No finding should be described as confirmed without reproducible supporting evidence.
