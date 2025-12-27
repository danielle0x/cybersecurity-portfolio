# **Bitdefender Investigation**



### **1. Title:**



### **Phishing Attempt via Suspicious Domain tsmtphit.com – Incident #28**

---

### **2. Bitdefender Incident (or detection) Link:**



[https://cloudgz.gravityzone.bitdefender.com/#!/incidents](https://cloudgz.gravityzone.bitdefender.com/#!/incidents)

---

### **3. Description:**



On October 9, 2025 at 10:48:58, the endpoint \[endpoint-name] at the \[site-name] of \[company-name] site attempted to access the suspicious domain tsmtphit.com, which has been classified as a phishing site by multiple antivirus engines and web reputation sources, including Bitdefender and Kaspersky (verified via VirusTotal: [https://www.virustotal.com/gui/domain/tsmtphit.com](https://www.virustotal.com/gui/domain/tsmtphit.com)).



The phishing attempt was detected as part of two alerts (URL.Phishing) associated with the endpoint.



The incident appears similar to previous incidents recorded on:



\[Endpoint-name] – 02 Oct 2025, 14:40:03



\[Endpoint-name] – 29 Sep 2025, 10:53:47



\[Endpoint-name] – 10 Sep 2025, 16:21:57



\[Endpoint-name] – 01 Sep 2025, 15:49:47

---

### **4\. Investigation Findings**



● **Observed Endpoint:**



\[Endpoint-name]

**IP:** \[ip]

**MAC Address:** \[MAC]



● **Observed Domain / URL:**



tsmtphit.com

hxxps://tsmtphit.com/



**IP:** 185.228.39.61



● **Alerts:**



URL.Phishing (2 alerts)



● **MITRE Techniques:**



[T1566](https://attack.mitre.org/techniques/T1566/) - Phishing



[T1566.002](https://attack.mitre.org/techniques/T1566/002/) - Spearphishing Link



[T1204 User](https://attack.mitre.org/techniques/T1204/) - User Execution



[T1204.001](https://attack.mitre.org/techniques/T1204/001/) - User Execution: Malicious Link



● **Analyst Assessment:**



The endpoint attempted to access the suspicious domain, which was confirmed as phishing by multiple threat intelligence sources. This type of incident aligns with previously recorded phishing attempts in the organization.



● **Response:**



Access to the malicious site was **blocked**.

---

### **5. Recommended Actions**



* Perform a full endpoint scan.



* Update blacklists and blocklists for the network and endpoint security.



* Conduct user awareness training to prevent future phishing attempts.

---

### **6. Ticket Priority:**



21/100 – Low

---

### **7. Assigned Analyst:**



Danielle (L1 SOC Analyst)


