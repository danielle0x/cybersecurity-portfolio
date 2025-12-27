# **X-Frame-Options Header Not Set**



**Asset:** Web Application

**Severity:** Medium

**Family:** Application Misconfiguration

---

### **Description**



The HTTP response from the web application does not include the **X-Frame-Options header**.

This header is important to protect against **Clickjacking attacks**, where an attacker can embed the site in a malicious frame and trick users into performing unintended actions. Without this protection, users may unknowingly interact with the application in a way that compromises security or privacy.

---

### **Potential Impact**



Exploitation of this misconfiguration could allow attackers to:



* Perform Clickjacking attacks, tricking users into clicking hidden buttons or links



* Manipulate user actions on sensitive pages (e.g., submitting forms, changing settings)



* Compromise user trust or cause unintended operations on the web application



Overall, this represents a medium risk, as it affects client-side protection but can lead to serious consequences if users are tricked.

---

### **Proposed Mitigation**



Recommended actions to remediate this vulnerability:



**1\.** Set the X-Frame-Options header on all responses from your web application.



**2\.** Choose the appropriate value based on how your pages are used:



* **DENY**: The page cannot be framed at all (most secure, recommended if framing is not required)



* **SAMEORIGIN**: Only pages from the same origin can frame this page (useful for internal frames or dashboards)



* **ALLOW-FROM \[URI]**: Allows framing only from specific trusted websites (limited browser support)



**3\.** Apply the header at the server level (recommended) or within the application code



**4\.** Verify the configuration using browser developer tools or security scanning tools to ensure the header is properly set

---

### **Supporting Evidence**



Screenshot demonstrating the vulnerability is provided below:



* [Overview](evidence/X-frame-not-set/Description-mitigation.png)




