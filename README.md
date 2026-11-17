# Future Interns — Task 1: Read-Only Vulnerability Assessment

**Status:** In progress. I have captured two successful HTTP homepage responses and one HTTPS certificate warning. I have not completed the full assessment or confirmed a vulnerability.

## Project overview

I am assessing the public Altoro Mutual demonstration application (AltoroJ / Testfire) using read-only checks.

### Target details
- **Host shown in my screenshots:** `testfire.net`
- **Other published demo hostname:** `demo.testfire.net`
- **Application:** AltoroJ / Altoro Mutual
- **Assessment type:** Read-only manual review and passive observation
- **Evidence captured:** 30 October and 8 November 2026

My screenshots show requests to `testfire.net`. I have kept that separate from `demo.testfire.net` rather than assuming both hostnames behave identically.

## Assessment scope

I reviewed public pages that did not require authentication. My checks were limited to normal browser requests and observations of HTTP responses, response headers, TLS/certificate behaviour, cookies and client-side resources. I planned to use OWASP ZAP in passive mode while manually browsing public pages.

I did not attempt logins, use credentials, access accounts, make transactions, submit forms, probe APIs, crawl or spider the site, fuzz inputs, run active scans, run Nmap port/service scans, exploit vulnerabilities, brute-force accounts or perform denial-of-service testing.

## Repository layout

| Folder | Contents |
|---|---|
| `methodology/` | My assessment scope, approach and tools |
| `evidence/browser/` | Browser screenshots |
| `evidence/tls/` | TLS and certificate evidence |
| `evidence/headers/` | HTTP response-header evidence |
| `findings/` | My observations and findings register |
| `report/` | Final assessment report |
| `references/` | Sources I referred to |

## Evidence captured

- **30 October 2026 — HTTP:** Chrome DevTools showed `GET http://testfire.net/` returning `200 OK` from `65.61.137.117:80`. The response details included `Apache-Coyote/1.1`, an HTML content type, chunked transfer encoding and a JSESSIONID cookie with HttpOnly and Path attributes visible.
- **30 October 2026 — HTTPS:** Chrome displayed `NET::ERR_CERT_AUTHORITY_INVALID` for `https://testfire.net/`. This shows that Chrome did not trust the certificate authority/chain in that browser environment. I have not established the precise cause or whether the certificate was expired.
- **8 November 2026 — HTTP:** Firefox DevTools showed another `200 OK` for `GET http://testfire.net/` from `65.61.137.117:80`. The screenshot shows Content-Type, Date, Server and Transfer-Encoding in the response-header panel.

The screenshots and notes are listed in the [Evidence Index](evidence/README.md). My interpretations are recorded in [Initial Observations](findings/initial-observations-2026-10-30.md) and the [Findings Register](findings/findings-register.md).

## Hosted target availability

The hosted demo has been unreliable. An external checker reported no HTTP 200 response from `demo.testfire.net` on 16 November, while the application's status endpoint returned `HostStatus: OK`. OWASP ZAP also notes that the online AltoroJ demo may be unavailable or broken and describes a local deployment as an alternative.

These checks do not prove that `testfire.net` is down from every network. My own screenshots show that `testfire.net` responded over HTTP on 30 October and 8 November; they do not establish its availability today.

Sources: [external availability check](https://www.websitedown.info/demo.testfire.net), [application status endpoint](https://demo.testfire.net/util/serverStatusCheckService.jsp), [OWASP ZAP AltoroJ notes](https://www.zaproxy.org/docs/testapps/altoroj/).

If I continue with a local AltoroJ installation, I will treat it as a separate target and keep its results separate from the hosted-site evidence.

## Work remaining

- [ ] Recheck the availability of `testfire.net` and `demo.testfire.net`
- [ ] Record HTTP-to-HTTPS redirect behaviour
- [ ] Capture certificate subject, issuer, validity, SANs and chain result, if available
- [ ] Capture complete response headers and cookie attributes, with cookie values redacted
- [ ] Complete OWASP ZAP passive observation, if the target is available
- [ ] Validate and prioritise any findings
- [ ] Complete and export the final PDF report

## Evidence handling

I have kept the screenshots and notes as evidence of what I observed. Before publishing screenshots, I check that session identifiers, cookie values, authentication tokens and personal data are not readable. Cookie values are not needed to demonstrate their security attributes.

## Disclaimer

This is an educational assessment of a demonstration application, not a real banking service. My observations apply only to the host, date, scope and methods recorded here. I have not marked any vulnerability as confirmed without supporting evidence.
