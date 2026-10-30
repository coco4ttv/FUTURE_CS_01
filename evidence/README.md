# Evidence

## HTTPS certificate warning

- [https-certificate-warning.png](https-certificate-warning.png) — Chrome's warning for https://testfire.net/ showing NET::ERR_CERT_AUTHORITY_INVALID (30 October 2026).

## HTTP homepage and response headers

The original DevTools screenshot was removed because it exposed a JSESSIONID session-cookie value. A redacted replacement is required before adding this evidence to the public repository. Do not upload the original unredacted screenshot.

## Evidence handling

Never publish session-cookie values, authentication tokens, or other secrets. Capture redacted evidence that preserves only the relevant header names, cookie security attributes and browser error details.
