# **Bitdefender Investigation**



### **1. Title:**



### **Phishing Attempt via Suspicious Domain tsmtphit.com – Incident #28**

---

### **2. Bitdefender Incident (or detection) Link:**



[https://cloudgz.gravityzone.bitdefender.com/#!/incidents](https://cloudgz.gravityzone.bitdefender.com/#!/incidents) (Note: Access to this link is restricted and requires active authentication to the GravityZone console.)

---

### **3. Description:**



On October 9, 2025 at 10:48:58, the endpoint \[hostname] at the \[site-name] of \[company-name] site attempted to access the suspicious domain tsmtphit.com, which has been flagged as phishing by multiple security vendors. The connection was automatically blocked by Bitdefender’s web protection layer.

---

### **4. Contextual Analysis (Historical Correlation)**



The investigation revealed that this is not an isolated event. The same Indicator of Compromise (IoC: tsmtphit.com) has been detected across multiple unique endpoints within the organization over the last 40 days.

**Historical Detections:**

● \[hostname] – 02 Oct 2025, 14:40:03



● \[hostname] – 29 Sep 2025, 10:53:47



● \[hostname] – 10 Sep 2025, 16:21:57



● \[hostname] – 01 Sep 2025, 15:49:47

---

### **5\. Investigation Findings**

● **Incident Classification:** True Positive (TP)

● **Confidence Level:** High

● **Observed Endpoint:**

-**Hostname**:\[hostname]

-**Internal IP:** \[ip]

-**MAC Address:** \[MAC]

### **5.1. Indicators of Compromise (IoC) & Evidence**

The following indicators confirm the malicious nature of the connection attempt:

● **Domain:** tsmtphit.com

● **IP address:** 185.228.39.61

● **Malicious URL:** hxxps://tsmtphit.com/

● **VirusTotal Analysis:** [View Report](https://www.virustotal.com/gui/domain/tsmtphit.com)

● **Detection Ratio:** 11/93 (Phishing/Malicious)

● [Virus total screenshot here](./virustotal-screenshot.png): VirusTotal scan results confirming the malicious reputation of the domain.


### **5.2 MITRE Techniques:**



● [T1566](https://attack.mitre.org/techniques/T1566/) - Phishing 



● [T1566.002](https://attack.mitre.org/techniques/T1566/002/) - Spearphishing Link 



● [T1204 User](https://attack.mitre.org/techniques/T1204/) - User Execution



● [T1204.001](https://attack.mitre.org/techniques/T1204/001/) - User Execution: Malicious Link



### **5.3 Analyst Assessment:**



The investigation confirms that the connection attempt to tsmtphit.com is a True Positive phishing event. This assessment is based on the domain's malicious reputation (confirmed by multiple vendors on VirusTotal) and the high-confidence correlation with previous incidents across the organization.

The fact that this IoC has appeared on multiple unique endpoints over a 40-day period strongly suggests an ongoing phishing campaign or a persistent malicious link circulating via internal communication channels. Bitdefender successfully mitigated the risk, but the recurrence indicates that the delivery vector (e.g., a specific email or file) may still be accessible to users.

---

### **6 Response:**



Access to the malicious site was **blocked** and a full endpoint scan was performed.

---

### **7. Recommended Actions**



● Update blacklists and blocklists for the network and endpoint security.



● Conduct user awareness training to prevent future phishing attempts.

---

### **8. Ticket Metadata:**

● **Ticket Priority:** 21/100 – Low 

● **Status:** Resolved

● **Assigned Analyst:** Danielle (L1 SOC Analyst)
