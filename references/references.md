# References

The following guidance informed interpretation and remediation recommendations. The assessment evidence itself comes from the dated browser and passive ZAP captures in this repository.

## OWASP guidance
- [OWASP ZAP — Alerts](https://www.zaproxy.org/docs/desktop/start/features/alerts/) — how ZAP organises alert risk, confidence, evidence and recommendations.
- [OWASP Content Security Policy Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html) — CSP design and deployment.
- [OWASP Clickjacking Defense Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Clickjacking_Defense_Cheat_Sheet.html) — framing restrictions and anti-clickjacking controls.
- [OWASP CSRF Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html) — anti-CSRF protection and the role of SameSite.
- [OWASP Session Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html) — session cookie protection and lifecycle.
- [OWASP HTTP Headers Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Headers_Cheat_Sheet.html) — recommended HTTP security headers.
- [OWASP Secure Headers Project](https://owasp.org/www-project-secure-headers/) — overview of browser security response headers.
- [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/) — general web application security assessment methodology.

## MDN
- [MDN Subresource Integrity](https://developer.mozilla.org/en-US/docs/Web/Security/Defenses/Subresource_Integrity) — how browsers verify externally loaded resources against a declared integrity hash.

## Application references
- [OWASP ZAP — AltoroJ / Testfire](https://www.zaproxy.org/docs/testapps/altoroj/) — information about the AltoroJ demonstration application and limitations of the hosted demo.
- [HCL AltoroJ project on GitHub](https://github.com/HCL-TECH-SOFTWARE/AltoroJ) — source project for the demonstration application.

External documentation is used to support interpretation and recommendations. It is not evidence that any finding was exploited or independently verified.
