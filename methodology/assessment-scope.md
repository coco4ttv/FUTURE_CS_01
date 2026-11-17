# Assessment Scope

## Target
I initially reviewed the public Altoro Mutual demonstration site at `testfire.net`. OWASP's AltoroJ page also identifies `demo.testfire.net` as its online demo. My screenshots in this repository show requests to `testfire.net`; I have kept the two hostnames separate in my notes.

## What I included
I limited the assessment to public pages that did not require authentication. I reviewed normal browser requests and observed HTTP responses, response headers, TLS certificate warnings, cookies and client-side resources. Where available, I used OWASP ZAP for passive observation of pages I browsed manually.

## What I did not test
I did not attempt logins, use credentials, access accounts, make transactions, submit forms, probe APIs, crawl or spider the site, fuzz inputs, run active scans, run Nmap port/service scans, exploit vulnerabilities, brute-force accounts or perform denial-of-service testing.

## Scope limitations
I stopped at the browser's certificate warning rather than bypassing it. When the hosted site was unavailable, I recorded that as a limitation rather than treating downtime as a vulnerability. I have not treated a different hostname or a local installation as the same target; any such work is recorded separately.

## How I recorded observations
For each observation, I recorded the URL, date and time, request method, result and supporting evidence where available. I separated what the screenshots directly show from anything that still needs validation. I removed or redacted session identifiers and other sensitive values from evidence intended for public sharing.
