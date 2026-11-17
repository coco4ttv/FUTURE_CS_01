# Future Interns — Task 1: Read-Only Vulnerability Assessment

> **Project status:** In progress. Preliminary browser observations are documented; the target's current availability is inconsistent and further testing is paused until reachability is confirmed.

## Overview

This project documents a cautious, read-only security assessment of **Altoro Mutual (Testfire)**, HCL's intentionally vulnerable sample banking application. The objective is to identify and explain evidence-backed security observations, assess their potential impact, and recommend practical remediation.

- **Target:** https://demo.testfire.net/ (historical entry point: http://testfire.net/)
- **Application:** AltoroJ / Altoro Mutual demonstration application
- **Assessment type:** Read-only, manual review and passive observation
- **Status:** Preliminary evidence captured; availability and remaining checks require re-validation
- **Assessment evidence date:** 30 October 2026

## Scope and safety

### In scope
- Publicly accessible, non-authenticated pages only
- Ordinary browser-generated page requests
- Response headers and redirect behaviour
- TLS certificate details and trust-chain observations
- Cookie security attributes, with cookie values and session identifiers redacted
- OWASP ZAP **passive mode only**, observing manually browsed public pages if the target is reachable

### Out of scope
- Login attempts, account access, transactions or form submissions
- API probing, crawling, spidering or fuzzing
- ZAP active scanning or attack features
- Nmap port/service scanning
- Exploitation, brute force, denial-of-service or any intrusive testing
- Any action that could affect service availability or access private data

Only perform checks that remain within this documented scope. Do not bypass browser certificate warnings or submit credentials.

## Repository guide

| Directory | Purpose |
|---|---|
| `methodology/` | Scope, approach and tool notes |
| `evidence/browser/` | Browser screenshots from the initial observation |
| `evidence/tls/` | TLS certificate evidence, when collected |
| `evidence/headers/` | Sanitised response-header evidence |
| `evidence/zap/` | Passive ZAP evidence only |
| `findings/` | Observations, validation status and remediation |
| `report/` | Final assessment report |
| `references/` | Technical references used in the assessment |

## Current observations

The initial browser evidence records an HTTP 200 response for the homepage and a Chrome HTTPS certificate warning. These are **preliminary observations**, not a complete or independently revalidated assessment. The certificate warning alone does not establish whether a certificate is expired, misissued or otherwise invalid; inspect certificate details before making that claim.

See:
- [Initial observations](findings/initial-observations-2026-10-30.md)
- [Findings register](findings/findings-register.md)
- [Evidence index](evidence/README.md)

## Target availability note

The demo has a history of intermittent availability. On 17 November 2026, public status sources returned mixed signals: an external checker reported no successful HTTP 200 response for the demo host on 16 November, while the application's own status endpoint returned `HostStatus: OK`. This does **not** establish that the public homepage is consistently reachable from every network. Record your own timestamped connection result before resuming the assessment.

If the hosted demo remains unavailable, do not silently substitute another target or present a local lab as the hosted target. A locally deployed AltoroJ instance may be used as a separately labelled assessment, with its own scope and evidence.

## Workflow and deliverables

1. Confirm target reachability and record date/time, requested URL, final URL and response/error.
2. Review only public pages and ordinary browser requests.
3. Capture relevant headers and TLS certificate details without bypassing warnings.
4. If reachable, observe manually browsed traffic with ZAP passive mode only.
5. Record each observation with evidence, impact, confidence, validation status and remediation.
6. Separate confirmed findings from unverified leads and environmental limitations.
7. Produce a concise PDF report and perform a final privacy/scope review.

- [ ] Recheck target availability and record exact result
- [ ] Validate HTTP/HTTPS behaviour and redirects
- [ ] Capture TLS certificate subject, issuer, validity, SANs and chain result
- [ ] Capture relevant response headers and redacted cookie attributes
- [ ] Capture ZAP passive observations, if target is reachable
- [ ] Complete findings register and remediation
- [ ] Export and review final PDF report

## Evidence handling

Never commit passwords, authentication tokens, session-cookie values, personal data or unredacted browser storage. Keep screenshots tightly cropped to the relevant evidence. Label dates and distinguish original observations from later re-tests.

## Disclaimer

This is an educational assessment of a deliberately vulnerable demonstration application, not a real banking service. Results apply only to the target, time, scope and methods documented. No finding should be described as confirmed without reproducible supporting evidence. Absence of findings does not demonstrate that the application is secure.
