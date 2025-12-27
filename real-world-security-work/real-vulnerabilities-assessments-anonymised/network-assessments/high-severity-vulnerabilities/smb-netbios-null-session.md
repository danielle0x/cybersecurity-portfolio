# **Microsoft Windows SMB/NETBIOS NULL Session Authentication Bypass**



**Asset:** \[Asset-name]

**Severity:** High

**CVSS Base Score:** 7.5

**Family:** Windows

---

### **Associated CVEs:**



* [CVE-1999-0519](https://www.cve.org/CVERecord?id=CVE-1999-0519)



* [CVE-1999-0520](https://www.cve.org/CVERecord?id=CVE-1999-0520)



* [CVE-2002-1117](https://www.cve.org/CVERecord?id=CVE-2002-1117)

---

### **Description**



Microsoft Windows contains an authentication bypass vulnerability via **SMB/NETBIOS.**

The flaw exists because certain SMB shares allow full access to Guest users. If the **Guest account** is enabled, an attacker could connect without a valid user account or password, gaining unauthorised access to the system.

---

### **Potential Impact**



Successful exploitation of this vulnerability could allow attackers to:



* Access SMB shares without authentication



* Read, modify or delete files on shared resources



* Potentially crash the system or disrupt services



Overall, this vulnerability represents a high risk due to its ability to bypass authentication and compromise system integrity.

---

### **Proposed Mitigation**



Recommended actions to remediate this vulnerability:



**1\.** Apply all relevant Microsoft security patches and updates to protect the system against known vulnerabilities.



**2\.** Disable **SMBv1** and block unauthenticated (**null**) sessions to prevent unauthorised access to shares.



**3\.** Restrict anonymous enumeration and remove or secure any shared resources or null session pipes.



**4\.** Enforce firewall rules to block SMB access from untrusted networks and monitor logs for suspicious activity.



Optional hardening: enable SMB signing/encryption and apply the principle of least privilege on shared resources.

---

### **Supporting Evidence**



Screenshot demonstrating the vulnerability is provided below:



* [Overview](evidence/SMB-NETBIOS-NULL-session/Description.png)

