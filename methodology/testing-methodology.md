# Testing Methodology

## Work completed

I used normal browser navigation to review the public homepage and its HTTP response. I captured the browser's Network/Headers details without submitting forms or interacting with account features.

- On 30 October 2026, Chrome showed a `200 OK` response for `GET http://testfire.net/`.
- On 30 October 2026, Chrome displayed `NET::ERR_CERT_AUTHORITY_INVALID` when I opened `https://testfire.net/`. I recorded the warning and did not bypass it.
- On 8 November 2026, Firefox showed another `200 OK` response for `GET http://testfire.net/`. I captured the response headers visible in DevTools.

I have not yet captured a complete TLS certificate chain, a complete set of security response headers or OWASP ZAP passive results. Those parts of my assessment remain unfinished.

## Checks used in my review

When the target was available, I used normal browser requests to:
1. Open the public homepage and record the URL, response status and time.
2. Observe the HTTP response and any redirect behaviour.
3. Review the browser's TLS/certificate result.
4. Inspect response headers from ordinary public-page requests.
5. Review cookie attributes visible in the response without recording cookie values.
6. Observe manually browsed public pages with OWASP ZAP passive mode, if available.

I did not spider, crawl, fuzz or run an active scan.

## Availability limitations

The hosted demo has been intermittent. When a request failed, I recorded the error and date rather than interpreting the failure as a security weakness. My historical screenshots show that `testfire.net` responded over HTTP on 30 October and 8 November 2026; they do not establish its current availability.

If I continue with a local AltoroJ installation, I will identify it as a separate target and keep its results distinct from the hosted-site evidence.
