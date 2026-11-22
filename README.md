# Future Interns — Task 1: Read-Only Vulnerability Assessment

**Status:** Assessment evidence captured; findings and final report are still being prepared.

## Project overview

This project documents a read-only security review of the public Altoro Mutual demonstration application hosted at **Testfire**.

| Item | Details |
|---|---|
| Target observed | `http://testfire.net/` |
| Application | Altoro Mutual (AltoroJ demonstration application) |
| Assessment type | Read-only browser review and passive security observation |
| Latest ZAP evidence | 22 November 2026 |
| Tools | Firefox DevTools, OWASP ZAP 2.17.0 |
| Report | To be added after findings review and Canva export |

The hosted Testfire target is the subject of this assessment. The separate AltoroJ Docker installation on my Kali VM is a practice environment and is **not** treated as the assessed target.

## Scope and ethical boundaries

The review was limited to publicly accessible pages and normal browser-generated requests. I inspected HTTP responses, response headers, cookie attributes, publicly returned page content and client-side resource references. OWASP ZAP was used in **Safe Mode** for passive observation while browsing manually.

I did not:
- attempt login bypass or unauthorised access;
- submit login, subscription or other application forms;
- exploit vulnerabilities or send attack payloads;
- perform brute-force, denial-of-service or other disruptive testing;
- run ZAP Active Scan, automated attack scans, spidering or fuzzing;
- run Nmap port or service scans.

ZAP reported a possible absence of anti-CSRF tokens in two forms based on passive HTML inspection. The forms were not submitted and the behaviour was not tested.

## Assessment activity and evidence

### Historical browser observations
- **30 October 2026 — HTTP:** Chrome DevTools recorded `GET http://testfire.net/` returning `200 OK`. The response showed `Apache-Coyote/1.1` and a JSESSIONID cookie with HttpOnly and Path attributes visible.
- **30 October 2026 — HTTPS:** Chrome displayed `NET::ERR_CERT_AUTHORITY_INVALID` for `https://testfire.net/`. This records a trust warning in that browser environment; it does not establish the exact certificate cause.
- **8 November 2026 — HTTP:** Firefox DevTools recorded another `200 OK` response for `GET http://testfire.net/`.

### OWASP ZAP passive observation — 22 November 2026
- ZAP was visibly set to **Safe Mode**.
- The History panel shows a normal `GET http://testfire.net/` request returning `200 OK`, along with other browser-generated page and resource requests.
- The Sites panel shows the Testfire host and paths observed during browsing. Other hostnames also appear because pages referenced third-party resources; those hosts were not independently assessed.
- ZAP displayed **16 alert categories**. This is a count of alert groups, **not 16 confirmed vulnerabilities**.
- The captured alerts include missing security headers, cookie attribute observations, an external JavaScript reference without a Subresource Integrity attribute, a possible anti-CSRF-token issue and a generic internal-server-error response. Each item is treated according to its evidence and confidence in the findings register.

The screenshot index is in [Evidence](evidence/README.md), with the ZAP captures listed in [OWASP ZAP Evidence](evidence/zap/README.md).

## Repository layout

| Folder | Contents |
|---|---|
| `methodology/` | Assessment scope, approach and tools |
| `evidence/browser/` | Browser screenshots |
| `evidence/headers/` | HTTP response-header evidence |
| `evidence/tls/` | Earlier browser TLS/certificate evidence |
| `evidence/zap/` | ZAP Sites, History, Response and passive alert screenshots |
| `findings/` | Initial observations and findings register |
| `report/` | Final assessment report when exported |
| `references/` | Technical references |

## Findings and limitations

ZAP's alerts are passive indicators. A missing response header or cookie attribute can be reported as an observed configuration weakness on the sampled response, but it does not by itself prove that an exploit is possible. Alerts with low confidence or generic error evidence are explicitly marked as unconfirmed.

The ZAP History capture includes some non-200 responses for individual paths or external resources. These are recorded as observations only; they are not treated as vulnerabilities or as evidence that the entire site was unavailable.

The HSTS alert is not treated as a finding based only on the HTTP capture. HTTPS behaviour must be assessed from an appropriate HTTPS response before drawing a conclusion. The third-party hostnames visible in ZAP were not separately tested.

## Evidence handling

Before public sharing, screenshots are checked for readable session identifiers, cookie values, tokens or personal data. Cookie values are not needed to demonstrate cookie security attributes and must remain redacted.

## Disclaimer

This is an educational, read-only assessment of a demonstration application. It is not a penetration test of a production banking service. Conclusions apply only to the target, pages, responses, date and limited methods recorded here. No exploitation or intrusive testing was performed.
