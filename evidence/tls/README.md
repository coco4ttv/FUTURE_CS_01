# TLS Evidence

## Evidence captured

- [Chrome certificate warning](certificate-warning-2026-10-30.png) — 30 October 2026, `https://testfire.net/`, Chrome error `NET::ERR_CERT_AUTHORITY_INVALID`.

## What I observed

Chrome did not trust the certificate authority/chain in that browser environment at the time of capture.

The screenshot does not show the certificate subject, issuer, expiry date, SANs or full chain. I have not established whether the certificate was expired or identified the precise cause of the trust error.

## Evidence still outstanding

I have not yet saved:
- Certificate subject, issuer, validity dates and SANs
- Certificate-chain/trust verification result
- OpenSSL certificate inspection output

I did not bypass the browser warning.
