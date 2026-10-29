# **SQL Injection**


**Asset:** Web Application

**Severity:** High

**Family:** SQL Injection

**Affected Parameter:** pswd

---

### **Description**



The web application is vulnerable to SQL Injection, a critical web security flaw that occurs when user-controlled input is improperly handled within SQL queries. 



During testing, the application behaviour was successfully altered using the following boolean-based payloads:



`ZAP AND 1=1 --`



`ZAP AND 1=2 --`



These payloads produced different responses, confirming that the input parameter "pswd" is being interpreted as part of a backend SQL query. This indicates that the application does not correctly sanitize or parameterize user input before sending it to the database.



As a result, attackers may be able to inject malicious SQL code and manipulate database queries.

---

### **Potential Impact**



Successful exploitation of this vulnerability could allow an attacker to:



* Bypass authentication mechanisms



* Extract sensitive information from the database (credentials, personal data, etc.)



* Modify or delete database records



* Escalate privileges within the application



* Fully compromise the backend database in severe cases



Overall, this vulnerability represents a high security risk because it directly affects data confidentiality, integrity and availability.

---

### **Proposed Mitigation**



To properly remediate this vulnerability, the following actions are recommended:



**1\.** Use parameterized queries (prepared statements) – Avoid concatenating user input into SQL queries.



**2\.** Validate all input on the server side – Ensure inputs are type-checked and sanitized.



**3\.** Apply the principle of least privilege – Use only the necessary database permissions.



**4\.** Implement input filtering policies – Prefer whitelists or strict blacklists.



**5\.** Use stored procedures safely (optional) – Avoid dynamic SQL inside procedures.

---

### **Supporting Evidence**



Screenshot demonstrating the vulnerability is provided below:



* [Overview](./evidence/sql-injection/description.png)

---

### **References**



* [https://www.owasp.org/index.php/Top\_10\_2010-A1](https://www.owasp.org/index.php/Top_10_2010-A1)

* [https://www.owasp.org/index.php/SQL\_Injection\_Prevention\_Cheat\_Sheet](https://www.owasp.org/index.php/SQL_Injection_Prevention_Cheat_Sheet)


