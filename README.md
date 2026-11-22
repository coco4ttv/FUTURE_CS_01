# Future Interns — Task 1: Read-Only Vulnerability Assessment

**Status:** Read-only assessment completed; nine-page report prepared.

## Project overview

This project documents a limited read-only security review of the public Altoro Mutual demonstration application hosted at Testfire.

| Item | Details |
|---|---|
| Target observed | `http://testfire.net/` |
| Application | Altoro Mutual (AltoroJ demonstration application) |
| Assessment type | Read-only browser review and passive security observation |
| Evidence dates | 30 October, 8 November and 22 November 2026 |
| Tools | Chrome/Firefox Developer Tools, OWASP ZAP 2.17.0, Canva |
| Report | [Nine-page PDF report](report/FUTURE_CS_01_Vulnerability_Assessment_Report.pdf) |

**Editable Canva report:** https://www.canva.com/d/QaO7S9C3HdCNRsj

The hosted Testfire target is the subject of this assessment. The separate AltoroJ Docker installation on Kali is a practice environment and is **not** treated as the assessed target.

## Scope and ethical boundaries

The review was limited to publicly accessible pages and normal browser-generated requests. I inspected HTTP responses, response headers, cookie attributes, publicly returned page content and client-side resource references. OWASP ZAP was used in **Safe Mode** for passive observation while browsing manually.

I did not:
- attempt login bypass or unauthorised access;
- use credentials, submit forms or make transactions;
- exploit vulnerabilities or send attack payloads;
- perform brute-force, denial-of-service or other disruptive testing;
- run ZAP Active Scan, automated attack scans, spidering, crawling or fuzzing;
- run Nmap port or service scans.

ZAP reported a possible absence of anti-CSRF tokens in two forms based on passive HTML inspection. The forms were not submitted and the behaviour was not tested.

## Assessment activity and evidence

### Browser observations
- **30 October 2026 — HTTP:** Chrome DevTools recorded `GET http://testfire.net/` returning `200 OK`. The response showed `Apache-Coyote/1.1` and a JSESSIONID cookie with HttpOnly and Path attributes visible. A session identifier appeared in the original screenshot; that unredacted original has been removed from the current repository file tree.
- **30 October 2026 — HTTPS:** Chrome displayed `NET::ERR_CERT_AUTHORITY_INVALID` for `https://testfire.net/`. This records a browser trust warning; the exact certificate cause was not established.
- **8 November 2026 — HTTP:** Firefox Developer Tools recorded a `GET /` response of `200 OK`, with Content-Type, Date, Server and Transfer-Encoding visible.

### OWASP ZAP passive observation — 22 November 2026
- ZAP was visibly set to **Safe Mode**.
- The History panel shows a normal `GET http://testfire.net/` request returning `200 OK`, alongside other browser-generated requests.
- The Sites panel shows Testfire paths and other hostnames referenced as external resources; those hosts were not independently assessed.
- ZAP displayed **16 alert categories**. This is a count of alert groups, **not 16 confirmed vulnerabilities**.
- The findings register groups related alerts and distinguishes observed configuration weaknesses from low-confidence or informational observations.

Evidence indexes:
- [Evidence overview](evidence/README.md)
- [OWASP ZAP screenshots](evidence/zap/README.md)
- [Findings register](findings/findings-register.md)
- [Technical references](references/references.md)

## Findings and limitations

Six candidate configuration observations are prioritised for remediation: CSP, anti-clickjacking protection, external JavaScript without SRI, SameSite cookie attribute, server banner and X-Content-Type-Options. Proposed priorities are qualitative and separate from ZAP's own ratings.

The HTTPS certificate trust warning is recorded separately as an observation with medium investigation priority; its root cause is unconfirmed. The anti-CSRF and generic internal-server-error alerts are also not treated as confirmed vulnerabilities.

The report explains what each issue means in plain English, its potential business impact, proposed priority and recommended remediation. It references OWASP guidance and MDN documentation.

## Disclaimer

This is an educational, read-only assessment of a demonstration application. It is not a penetration test of a production banking service. Conclusions apply only to the target, pages, responses, dates and limited methods recorded here. No exploitation or intrusive testing was performed.
