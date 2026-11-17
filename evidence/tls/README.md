# TLS Evidence

## Current evidence
- [Chrome certificate warning](../browser/https-certificate-warning.png) — 30 October 2026, `https://testfire.net/`, Chrome error `NET::ERR_CERT_AUTHORITY_INVALID`.

## What this establishes
Chrome did not trust the certificate authority/chain in that browser environment at the time of capture.

## What it does not establish
The screenshot does not show the certificate subject, issuer, expiry, SANs or full chain. Do not label the certificate expired or identify a precise root cause without those details.

## Evidence still required
- Certificate details (subject, issuer, validity and SAN)
- Chain/trust verification result
- OpenSSL output, if the HTTPS endpoint can be inspected safely

Do not bypass the browser warning. If the TLS endpoint does not respond, record the connection error and stop.
