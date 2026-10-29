### **SSL/TLS – Deprecated SSLv2 and SSLv3 Protocol Detection**



**Asset:** \[Asset-name]

**Severity:** Medium

**CVSS Base Score:** 5.9

**Family:** SSL/TLS

---

### **Associated CVEs:**



* [CVE-2014-3566](https://www.cve.org/CVERecord?id=CVE-2014-3566)



* [CVE-2016-0800](https://www.cve.org/CVERecord?id=CVE-2016-0800)

---

### **Description**



The system was found to accept deprecated **SSLv2** and **SSLv3** protocols. These protocols contain known cryptographic weaknesses, such as:



CVE-2014-3566: Padding Oracle On Downgraded Legacy Encryption (**POODLE**)



CVE-2016-0800: Decrypting RSA with Obsolete and Weakened Encryption (**DROWN**)



Use of these protocols could allow attackers to intercept or manipulate sensitive data transmitted over secure connections. Additionally, no further security updates are provided for these legacy protocols.

---

### **Potential Impact**



Exploitation of SSLv2/SSLv3 could allow attackers to:



* Eavesdrop on encrypted connections



* Decrypt sensitive information or compromise data integrity



* Exploit new cryptographic vulnerabilities that will not be patched



Overall, this represents a medium risk, mainly due to exposure of secure communications to legacy cryptographic attacks.

---

### **Proposed Mitigation**



Recommended actions to remediate this vulnerability:



**1\.** Disable **SSLv2** and **SSLv3**, allowing only **TLSv1.2** and **TLSv1.3**



**2\.** Update server configurations for modern protocols



Ensuring only TLSv1.2+ protocols are active mitigates risks associated with legacy SSL protocols.

---

### **Supporting Evidence**



Screenshot demonstrating the vulnerability is provided below:



* [Overview](./evidence/sslv2-sslv3-protocol/description.png)

