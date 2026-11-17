# Assessment Scope

## Target

I initially reviewed the public Altoro Mutual demonstration site at `testfire.net`. OWASP's AltoroJ documentation also identifies `demo.testfire.net` as an online demo. The screenshots in this repository show requests to `testfire.net`, so I have kept the two hostnames separate in my notes.

## What I included

I limited my review to public pages that did not require authentication. I used normal browser navigation and observed HTTP responses, response headers, TLS certificate behaviour, cookies and client-side resources. I also planned passive observation with OWASP ZAP while manually browsing public pages.

## What I did not test

I did not attempt logins, use credentials, access accounts, make transactions, submit forms, probe APIs, crawl or spider the site, fuzz inputs, run active scans, run Nmap port/service scans, exploit vulnerabilities, brute-force accounts or perform denial-of-service testing.

## Scope limitations

I did not bypass the browser's certificate warning. When the hosted site was unavailable, I recorded that as a limitation rather than treating downtime as a vulnerability. I have not treated a different hostname or a local installation as the same target; any such work will be recorded separately.

## Recording observations

I recorded the URL, date and time, request method, result and supporting evidence where available. I separated what the screenshots directly show from anything that still needs validation. I have redacted session identifiers and other sensitive values from evidence intended for public sharing.
