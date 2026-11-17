# Future Interns — Task 1: Read-Only Vulnerability Assessment

> **Project status:** In progress — historical HTTP response evidence is available, but the hosted target is intermittent and HTTPS trust failed in the supplied browser capture. No vulnerability is marked confirmed yet.

## Overview
A read-only assessment of **Altoro Mutual (AltoroJ / Testfire)**, HCL's deliberately vulnerable sample banking application.

### Target identity — keep hosts distinct
- **Originally observed host:** `testfire.net` (screenshots show `http://testfire.net/`)
- **OWASP-listed online demo:** `demo.testfire.net` (`https://demo.testfire.net/`)
- **Application:** AltoroJ / Altoro Mutual
- **Assessment type:** Read-only manual review and passive observation
- **Evidence dates:** 30 October and 8 November 2026; fresh reachability still needs checking.

Do not assume `testfire.net` and `demo.testfire.net` have identical current behaviour. Record the exact hostname and scheme for every test.

## Scope and safety
**In scope:** public non-authenticated pages, ordinary browser GET requests, HTTP/HTTPS redirect behaviour, response headers, redacted cookie attributes, TLS certificate details and OWASP ZAP passive observation of manually browsed pages only.

**Out of scope:** login attempts, account access, transactions, form submissions, API probing, crawling, spidering, fuzzing, ZAP active scanning, Nmap port/service scanning, exploitation, brute force and denial-of-service.

Do not bypass certificate warnings, submit credentials or proceed through an unsafe-site interstitial.

## Repository guide
| Directory | Purpose |
|---|---|
| `methodology/` | Scope, testing approach and tools |
| `evidence/browser/` | General browser screenshots |
| `evidence/tls/` | Certificate and TLS evidence |
| `evidence/headers/` | HTTP response-header evidence |
| `evidence/zap/` | Passive ZAP evidence only |
| `findings/` | Observations, validation status and remediation |
| `report/` | Final PDF report |
| `references/` | Technical references |

## Evidence captured so far
- **30 October 2026 — HTTP:** Chrome DevTools records `GET http://testfire.net/` returning `200 OK` from `65.61.137.117:80`. It shows `Apache-Coyote/1.1`, HTML content type, chunked transfer encoding and a JSESSIONID cookie with HttpOnly and Path attributes visible.
- **30 October 2026 — HTTPS:** Chrome displayed `NET::ERR_CERT_AUTHORITY_INVALID` for `https://testfire.net/`. This establishes a trust error in that browser environment, not expiry or the precise cause.
- **8 November 2026 — HTTP:** Firefox DevTools records another `200 OK` for `http://testfire.net/` from `65.61.137.117:80`. Its response-header panel shows Content-Type, Date, Server and Transfer-Encoding.
- The Firefox capture does not show common security response headers such as CSP or X-Frame-Options. Treat them as **not evidenced in this capture**, not proven absent from every response or route.

See [Evidence Index](evidence/README.md), [TLS notes](evidence/tls/README.md), [Headers notes](evidence/headers/README.md), [Initial observations](findings/initial-observations-2026-10-30.md) and [Findings Register](findings/findings-register.md).

## Target availability — 17 November 2026
Availability reports are mixed. An external checker recorded no HTTP 200 response from `demo.testfire.net` on 16 November, while the application's status endpoint currently returns `HostStatus: OK`. OWASP ZAP warns that the online AltoroJ demo may be unavailable or broken and recommends a local deployment for consistent testing. These signals do not prove that the originally observed `testfire.net` host is down from every network.

Sources: [external availability check](https://www.websitedown.info/demo.testfire.net), [application status endpoint](https://demo.testfire.net/util/serverStatusCheckService.jsp), [OWASP ZAP AltoroJ notes](https://www.zaproxy.org/docs/testapps/altoroj/).

**Conclusion:** hosted availability is intermittent/uncertain. The supplied 8 November screenshot proves the original HTTP host responded at that time, not that it responds now. Before resuming, visit each intended hostname once and record timestamp, scheme, hostname, final URL and exact result. Do not keep retrying a failing service.

If the online demo remains unavailable, a local AltoroJ deployment can be a separate assessment target. Label it clearly and keep its evidence separate.

## Workflow
1. Confirm exact target hostname and reachability; record timestamp and result.
2. Review only public pages and ordinary browser GET requests.
3. Capture HTTP redirects and complete response headers.
4. Inspect TLS certificate details only if the HTTPS connection can be examined safely; do not bypass warnings.
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
Never commit passwords, authentication tokens, session-cookie values, personal data or unredacted browser storage. Redact cookie values in request/response screenshots. Use consistent names such as `http-response-headers-YYYY-MM-DD.png`.

## Disclaimer
This is an educational assessment of a deliberately vulnerable demonstration application, not a real banking service. Results apply only to the host, time, scope and methods documented. No finding should be described as confirmed without reproducible supporting evidence. Absence of findings does not demonstrate that the application is secure.
