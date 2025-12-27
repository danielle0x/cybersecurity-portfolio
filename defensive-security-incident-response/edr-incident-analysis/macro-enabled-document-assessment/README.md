# **EDR Alert Assessment – Macro-Enabled Document Payload Staging**



### **Description**



In this scenario, I analysed a simulated high-severity EDR alert triggered by a macro-enabled Microsoft Word document (invoice.docm). After the document was opened, **WINWORD.EXE** spawned **CMD.EXE**, which then used **cURL.EXE to download an external executable** from a remote domain.



The downloaded file (install.exe) was written to the **Public directory** but was **never executed**, indicating behaviour consistent with **malware staging rather than immediate execution**. Although the involved binaries (WINWORD, CMD, cURL) are legitimate and signed by Microsoft, their chained execution represents an abnormal pattern commonly associated with malicious macro abuse.



The alert was mapped to [MITRE ATT\&CK Initial Access** – T1566.001](https://attack.mitre.org/techniques/T1566/001/) (Spearphishing Attachment) with a high confidence score. The EDR successfully **quarantined the dropped payload and blocked the external domain**, preventing further impact.

---

### **Assessment**



Based on the process chain, command-line activity, and associated indicators, this alert was assessed as a **true positive**. The behaviour demonstrates how trusted system tools can be abused to deliver malware while evading simple signature-based detection.

---

### **Evidence** 



* [Process chain](./process-chain.png)

