# **SSL/TLS – Deprecated TLSv1.0 and TLSv1.1 Protocol Detection**



**Asset:** \[Asset-name]

**Severity:** Medium

**CVSS Base Score:** 4.3

**Family:** SSL/TLS

---

### **Associated CVEs:**



* [CVE-2011-3389](https://www.cve.org/CVERecord?id=CVE-2011-3389)



* [CVE-2015-0204](https://www.cve.org/CVERecord?id=CVE-2015-0204)



* [CVE-2023-41928](https://www.cve.org/CVERecord?id=CVE-2023-41928)



* [CVE-2024-41270](https://www.cve.org/CVERecord?id=CVE-2024-41270)



* [CVE-2025-3200](https://www.cve.org/CVERecord?id=CVE-2025-3200)

---

### **Description**



The system was found to accept deprecated **TLSv1.0** and **TLSv1.1** protocols. These protocols contain known cryptographic flaws, such as:



* CVE-2011-3389: Browser Exploit Against SSL/TLS (**BEAST**)



* CVE-2015-0204: Factoring Attack on RSA-EXPORT Keys (**FREAK**)



Use of these protocols may allow attackers to eavesdrop on secure communications or exploit other cryptographic weaknesses. Additionally, these protocols no longer receive security updates, increasing the long-term risk.

---

### **Potential Impact**



Exploitation of deprecated TLS protocols could allow attackers to:



* Intercept and decrypt sensitive data transmitted over HTTPS



* Exploit legacy cryptographic flaws to compromise confidentiality



* Expose the system to new vulnerabilities that will no longer be patched



Overall, this represents a medium risk, primarily due to potential data exposure over HTTPS.

---

### **Proposed Mitigation**



Recommended actions to remediate this vulnerability:



**1\.** Disable **TLSv1.0** and **TLSv1.1** and enable only **TLSv1.2** and **TLSv1.3.**



**2\.** Update server configurations for modern protocols.



**3\.** Verify the configuration after restart (e.g., with Nmap)

---

### **Supporting Evidence**



Screenshot demonstrating the vulnerability is provided below:

* [Overview](evidence/TLSv1.0-TLSv1.1-protocol/Description.png)

