# **Absence of Anti-CSRF Tokens**



**Asset:** Web Application

**Severity:** Medium

**Family:** Cross-Site Request Forgery

---

### **Description**



The application does not implement **Anti-CSRF tokens** in at least one HTML form.

Cross-Site Request Forgery (**CSRF**) is an attack that forces a victim’s browser to send an unauthorised request to a vulnerable web application while the user is authenticated. As a result, the attacker can perform actions on behalf of the victim without their knowledge or consent.

---

### **Potential Impact**



Successful exploitation of this vulnerability may allow an attacker to:



* Perform unauthorized actions using the victim’s authenticated session



* Modify user account settings or sensitive data



* Trigger critical operations without user interaction



* Combine the attack with other vulnerabilities such as XSS for greater impact



Overall, this vulnerability represents a medium security risk, especially in applications that handle user data or sensitive operations.

---

### **Proposed Mitigation**



Recommended actions to remediate this vulnerability:



**1\.** Implement **Anti-CSRF tokens** in all forms and state-changing requests by generating a unique and unpredictable token for each user session and validating it on the server side.



**2\.** Use secure frameworks or built-in security libraries that provide automatic CSRF protection.



**3\.** Avoid using the **GET method** for any operation that modifies application data.



**4\.** Configure session cookies with the **SameSite attribute** (Lax or Strict) to reduce the risk of cross-site request exploitation.



**5\.** Add additional validation by checking the **Origin** and **Referer** HTTP headers where applicable.



**6\.** Ensure proper protection against **Cross-Site Scripting (XSS)**, since XSS can be used to bypass CSRF defenses.

---

### **Supporting Evidence**



Screenshot demonstrating the vulnerability is provided below:



* [Overview](./evidence/anti-csrf-absence/description.png)

