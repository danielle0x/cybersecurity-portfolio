# **Content Security Policy (CSP) Header Not Set**



**Asset:** Web Application 

**Severity:** Medium

**Family:** Application Misconfiguration

---

### **Description**



The web application does not include a Content Security Policy (**CSP**) header in its HTTP responses.

CSP is a critical security mechanism that helps prevent and mitigate client-side attacks, especially:



* Cross-Site Scripting (**XSS**)



* Data injection attacks



* Malicious content loading



Without a CSP, the browser has no restrictions on where scripts, styles, images, fonts, frames and other resources can be loaded from, significantly increasing the attack surface.

---

### **Potential Impact**



The absence of a CSP header could allow attackers to:



* Execute malicious JavaScript (XSS) in users’ browsers



* Inject malicious content into trusted pages



* Steal sensitive data such as **session cookies** or credentials



* Redirect users to malicious websites



* Distribute malware through the compromised application



Overall, this represents a medium risk, but it may escalate to high impact if combined with other vulnerabilities such as XSS.

---

### **Proposed Mitigation**



Recommended actions to remediate this vulnerability:



**1\.** Define and enforce a Content Security Policy header across the entire web application



**2\.** Apply the policy at the web server level (recommended) to ensure consistent protection for all responses



**3\.** Start with a restrictive baseline policy, such as:



* Allow content only from the application’s own domain



* Block all inline scripts where possible



* Restrict framing and object embedding



**4\.** Gradually refine the policy based on application functionality, testing thoroughly to avoid breaking legitimate features



**5\.** Monitor CSP violations using browser reports or logging to fine-tune the policy securely

---

### **Supporting Evidence**



Screenshot demonstrating the vulnerability is provided below:



* [Overview](./evidence/csp-not-set/description-mitigation.png)
