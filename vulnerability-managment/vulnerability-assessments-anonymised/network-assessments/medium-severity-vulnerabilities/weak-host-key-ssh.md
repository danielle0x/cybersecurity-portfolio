# **Weak Host Key Algorithm(s) (SSH)**



**Asset:** \[Asset-name]

**Severity:** Medium

**CVSS Base Score:** 5.3

**Family:** SSH

**Associated CVEs:** None reported

---

### **Description**



The remote SSH server was found to support **weak host key algorithms.**

Weak or outdated cryptographic algorithms reduce the overall security of SSH connections and may allow attackers to perform **cryptographic downgrade attacks** or exploit weaknesses in key exchange mechanisms.



Supporting weak algorithms weakens the trust model of SSH and increases the risk of unauthorised access.

---

### **Potential Impact**



If exploited, this vulnerability could allow attackers to:



* Intercept or manipulate SSH connections



* Perform cryptographic attacks against weak key algorithms



* Increase the risk of unauthorised system access



Overall, this represents a medium risk, primarily due to the potential compromise of secure remote administration.

---

### **Proposed Mitigation**



Recommended actions to remediate this vulnerability:



**1\.** Edit the SSH server configuration file



**2\.** Restrict host key and public key algorithms to secure ones only, such as **Ed25519** and **RSA** with **SHA-2 (rsa-sha2-256 / rsa-sha2-512)**



**3\.** Restart the SSH service



**4\.** Verify that weak algorithms are disabled (e.g., with Nmap)

---

### **Supporting Evidence**



Screenshot demonstrating the vulnerability is provided below:



* [Overview](./evidence/weak-host-key-ssh/description.png)

---

### **References**



* [https://www.rfc-editor.org/rfc/rfc8332](https://www.rfc-editor.org/rfc/rfc8332)

* [https://www.rfc-editor.org/rfc/rfc8709](https://www.rfc-editor.org/rfc/rfc8709)

* [https://www.rfc-editor.org/rfc/rfc4253#section-6.6](https://www.rfc-editor.org/rfc/rfc4253#section-6.6)


