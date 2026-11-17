# Testing Methodology

## Work completed

I used normal browser navigation to review the public homepage and its HTTP response. I captured the browser's Network/Headers details rather than submitting forms or interacting with account features.

- On 30 October 2026, Chrome showed a `200 OK` response for `GET http://testfire.net/`.
- On 30 October 2026, Chrome displayed `NET::ERR_CERT_AUTHORITY_INVALID` when I opened `https://testfire.net/`. I recorded the warning and did not bypass it.
- On 8 November 2026, Firefox showed another `200 OK` response for `GET http://testfire.net/`. I captured the response headers visible in DevTools.

I have not yet captured a complete TLS certificate chain, a complete set of security response headers, or OWASP ZAP passive results. Those checks remain incomplete.

## How I approached the review

I used the following read-only checks where the target was available:

1. I checked the public homepage and recorded the exact URL, response status and time.
2. I observed the HTTP response and any redirect behaviour.
3. I reviewed the browser's TLS/certificate result. I did not proceed through a certificate warning.
4. I inspected response headers from ordinary public-page requests.
5. I checked cookie attributes visible in the response, without recording cookie values.
6. If the site was available, I used OWASP ZAP in passive mode while manually browsing public pages. I did not spider, crawl, fuzz or run an active scan.

## Availability limitations

The hosted demo has been intermittent. When a request failed, I recorded the error and date rather than interpreting the failure as a security weakness. The historical screenshots show that `testfire.net` responded over HTTP on 30 October and 8 November 2026; they do not establish its current availability.

If I continue with a local AltoroJ installation, I will identify it as a separate target and keep its results distinct from the hosted-site evidence.
