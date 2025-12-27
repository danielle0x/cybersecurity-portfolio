### **SSL/TLS – Vulnerable Cipher Suites for HTTPS**



**Asset:** \[Asset-name]

**Severity:** High

**CVSS Base Score:** 7.5

**Family:** SSL/TLS

---

### **Associated CVEs:**



* [CVE-2016-2183](https://www.cve.org/CVERecord?id=CVE-2016-2183)



* [CVE-2016-6329](https://www.cve.org/CVERecord?id=CVE-2016-6329)



* [CVE-2020-12872](https://www.cve.org/CVERecord?id=CVE-2020-12872)

---

### **Description**



This vulnerability occurs when a service accepts weak or outdated **SSL/TLS cipher suites** over HTTPS. For example, 64-bit block ciphers like **3DES** are vulnerable to attacks such as **SWEET32** (CVE-2016-2183). Attackers could exploit these cipher suites to compromise confidentiality of transmitted data or gain other unauthorised access.

---

### **Potential Impact**



Exploitation of weak SSL/TLS cipher suites could allow attackers to:



* Decrypt sensitive information in transit



* Exploit cryptographic weaknesses for attacks such as SWEET32



* Potentially compromise the confidentiality or integrity of secure communications



Overall, this represents a high risk, particularly for services handling sensitive data.

---

### **Proposed Mitigation**



Recommended actions to remediate this vulnerability:



**1\.** Use **TLS 1.2** and **TLS 1.3**, disabling legacy protocols **TLS 1.0** and **TLS 1.1.**



**2\.** Prefer modern cipher suites with **forward secrecy** and **AEAD**:



* **ECDHE + AES-GCM** or **ChaCha20-Poly1305**



**3\.** Disable weak ciphers: **3DES/DES, RC4, EXPORT, NULL.**



**4\.** Enforce server-side cipher preference to control cipher negotiation order.



Optional hardening: Enable TLS 1.3 features if supported by the server and clients.

---

### **Supporting Evidence**



Screenshot demonstrating the vulnerability is provided below:



* [Overview](evidence/Vulnerable-HTTPS-Cipher-Suites/Description.png)

