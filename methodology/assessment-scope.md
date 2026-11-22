# Assessment Scope

## Target

The assessed target is the public Altoro Mutual demonstration application at `http://testfire.net/`. The ZAP evidence captured on 22 November 2026 records requests to this hostname.

The ZAP Sites tree also contains third-party hostnames referenced by the application, including an analytics hostname. These hosts were not independently assessed and are not included as targets.

The separate AltoroJ Docker practice installation on Kali is not part of this hosted Testfire assessment.

## Included

- Public-facing pages accessed through normal browser navigation.
- Passive observation of browser-generated HTTP requests and responses using OWASP ZAP in Safe Mode.
- Review of response headers, cookie attributes and publicly returned page/resource references.
- Review of ZAP passive alert descriptions, risk ratings and confidence.

## Excluded

- Login bypass, unauthorised access or use of credentials.
- Submitting login, subscription, transaction or other application forms.
- Exploitation, attack payloads, brute force or denial-of-service testing.
- ZAP Active Scan, automated attack scans, spidering, crawling or fuzzing.
- Nmap port or service scans.
- Independent testing of third-party hosts shown in the Sites tree.

## Scope limitations

Passive alerts are indicators and do not establish exploitability. The absence of an anti-CSRF token in observed form markup was reported with low confidence and was not verified through form submission or request-behaviour testing. A generic internal server error was not treated as confirmed sensitive information disclosure.

The HSTS alert was not included as a finding based only on the HTTP response capture. HTTPS behaviour requires a suitable HTTPS response for assessment.

All observations apply only to the sampled public pages and responses captured on the dates recorded in the evidence index.