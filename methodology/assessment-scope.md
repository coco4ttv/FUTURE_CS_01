# Assessment Scope

## Target
Altoro Mutual (AltoroJ), the HCL-published demonstration application at https://demo.testfire.net/.

## Authorised scope for this project
- Public, non-authenticated pages only.
- Normal browser navigation and the requests it naturally generates.
- Read-only observation of HTTP response behaviour, headers, TLS certificate information, cookies and client-side resources.
- OWASP ZAP passive observation of manually browsed pages only, if the target is reachable.

## Explicit exclusions
No login attempts, credential use, account access, transactions, form submissions, API probing, crawling, spidering, fuzzing, active scanning, Nmap port/service scanning, exploitation, brute force or denial-of-service testing.

## Stop conditions
Stop if the site is unavailable, redirects to an unexpected destination, presents a certificate warning, or a check would require interaction beyond the scope above. Do not bypass certificate warnings. Record availability failures as limitations, not vulnerabilities.

## Evidence standard
Every finding must include the affected URL, timestamp, method, observed result, evidence reference, impact rationale, confidence and validation status. Distinguish confirmed findings from hypotheses and unverified leads. Redact session identifiers, cookies, tokens and personal data before committing evidence.
