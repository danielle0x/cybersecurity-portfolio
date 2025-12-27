# **EDR Alert Assessment – Suspicious Credential Dumping Attempt**



### **Description**



In this scenario, I analysed a simulated high-severity EDR alert triggered by an **unsigned binary** (syncsvc.exe) running from the temporary directory. The binary accessed the memory of **LSASS.EXE** and attempted to write a credential dump to disk. The outbound network connection to a remote domain was blocked by the EDR.



Although syncsvc.exe is unsigned and the behaviour is suspicious, the involved system processes (explorer.exe, lsass.exe) are legitimate and Microsoft-signed. This alert represents behaviour consistent with **credential dumping**, a common technique for persistence and lateral movement.



The alert was mapped to **MITRE ATT\&CK Persistence – T1003.002** (Credential Dumping) with a high confidence score. The EDR successfully **blocked the network exfiltration and quarantined the malicious file**, preventing further impact.

---

### **Assessment**



Based on the observed process chain, memory access, and attempted network activity, this alert was assessed as a **true positive**. It demonstrates how attackers may abuse system tools to extract credentials while trying to evade detection.

---

### **Evidence**



* [Process chain](./process-chain.png)

