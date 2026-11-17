# Findings Register

**Assessment status:** Incomplete — target availability and technical observations require re-validation.

| ID | Area | Current status | Evidence / next action |
|---|---|---|---|
| OBS-01 | HTTP transport / redirect behaviour | Pending re-validation | Initial HTTP GET screenshot exists. Re-check redirect behaviour if the host responds. |
| OBS-02 | TLS certificate trust | Observed warning; cause unconfirmed | Browser screenshot records NET::ERR_CERT_AUTHORITY_INVALID. Inspect certificate details only if endpoint responds safely. |
| OBS-03 | Security response headers | Incomplete | Existing screenshot shows selected headers only. Capture complete relevant response headers on a reachable public page. |
| OBS-04 | Session-cookie attributes | Incomplete | HttpOnly and Path were visible; Secure and SameSite were not established. Re-capture with value redacted. |
| OBS-05 | Server banner disclosure | Observed, impact unconfirmed | Apache-Coyote/1.1 was visible in one response. Do not infer a vulnerable version from this banner alone. |

## Status definitions
- **Confirmed:** Reproducible evidence supports the security issue and its impact.
- **Pending validation:** Candidate observation needs further in-scope verification.
- **Not applicable / not observed:** The check could not be completed or did not produce evidence.

No confirmed vulnerability is claimed in this register at present.
