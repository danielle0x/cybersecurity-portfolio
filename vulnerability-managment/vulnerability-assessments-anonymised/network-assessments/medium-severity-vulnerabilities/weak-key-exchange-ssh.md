# **Weak Key Exchange (KEX) Algorithm(s) Supported (SSH)**



**Asset:** \[Asset-name]

**Severity:** Medium

**CVSS Base Score:** 5.3

**Family:** SSH

**Associated CVEs:** None reported

---

### **Description**



The remote SSH server was found to support **weak key exchange (KEX) algorithms**, specifically based on **1024-bit MODP Diffie-Hellman groups.**

These algorithms rely on commonly reused prime numbers. Although new key exchanges are generated for each session, modern cryptographic research has demonstrated that 1024-bit Diffie-Hellman parameters can be broken by well-resourced attackers, including nation-state adversaries.



As a result, the security of the cryptographic handshake used to establish SSH sessions is significantly weakened.

---

### **Potential Impact**



Exploitation of weak KEX algorithms could allow attackers to:



* Break the cryptographic protection of individual SSH sessions



* Perform man-in-the-middle attacks during the key exchange phase



* Decrypt or manipulate SSH traffic



* Compromise the confidentiality and integrity of remote administration sessions



Overall, this represents a medium risk, due to the possibility of real-time session compromise.

---

### **Proposed Mitigation**



Recommended actions to remediate this vulnerability:



**1\.** Update the SSH server configuration



**2\.** Restrict accepted KEX algorithms to strong options, such as:



* **Curve25519**



* **Diffie-Hellman group exchange with SHA-256**



**3\.** Restart the SSH service



**4\.** Verify the configuration (e.g., with Nmap)

---

### **Supporting Evidence**



Screenshot demonstrating the vulnerability is provided below:



* [Overview](./evidence/weak-key-exchange-ssh/description.png)

---

### **References**



* [https://weakdh.org/sysadmin.html](https://weakdh.org/sysadmin.html)

* [https://www.rfc-editor.org/rfc/rfc9142](https://www.rfc-editor.org/rfc/rfc9142)

* [https://www.rfc-editor.org/rfc/rfc9142#name-summary-guidance-for-implem](https://www.rfc-editor.org/rfc/rfc9142#name-summary-guidance-for-implem)

* [https://www.rfc-editor.org/rfc/rfc6194](https://www.rfc-editor.org/rfc/rfc6194)

* [https://www.rfc-editor.org/rfc/rfc4253#section-6.5](https://www.rfc-editor.org/rfc/rfc4253#section-6.5)


