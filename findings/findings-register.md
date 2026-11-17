# Findings Register

**Assessment status:** Incomplete. Historical observations exist; current reachability and several technical details need re-validation.

| ID | Area | Status | Evidence / next action |
|---|---|---|---|
| OBS-01 | HTTP transport / redirect behaviour | Historical HTTP 200 observed; current status unknown | Chrome (30 Oct) and Firefox (8 Nov) show `http://testfire.net/` returning 200. Verify current redirect behaviour with one normal browser visit. |
| OBS-02 | TLS certificate trust | Browser trust warning observed; cause unconfirmed | Chrome records `NET::ERR_CERT_AUTHORITY_INVALID` for `https://testfire.net/`. Do not claim expiry; inspect certificate and chain if safely available. |
| OBS-03 | HTTP security headers | Incomplete; possible missing headers to verify | Firefox capture shows Content-Type, Date, Server and Transfer-Encoding only. Capture full raw response headers from a reachable public page before concluding a header is absent. |
| OBS-04 | Session-cookie attributes | Partially observed | HttpOnly and Path were visible in the 30 Oct response. Secure and SameSite were not established. Ensure cookie value is redacted in any public screenshot. |
| OBS-05 | Server banner disclosure | Observed; impact unconfirmed | `Apache-Coyote/1.1` appears in historical response headers. A generic banner alone does not prove a vulnerable version. |

## Status definitions
- **Confirmed:** Reproducible evidence supports the security issue and its impact.
- **Observed / pending validation:** Supplied evidence shows a behaviour, but its security significance or current state is not established.
- **Incomplete:** Evidence is insufficient to determine presence or absence.
- **Limitation:** The target or test could not be reached/performed.

No confirmed vulnerability is claimed in this register. Do not count service unavailability as a vulnerability.
