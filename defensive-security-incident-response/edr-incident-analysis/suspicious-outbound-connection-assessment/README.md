# **EDR Alert Assessment – Suspicious Outbound Connection from User AppData**



### **Description**



In this scenario, I analysed a simulated medium-severity EDR alert triggered by an **unsigned binary** (UpdateAgent.exe) executing from the user’s AppData folder. The binary initiated an outbound HTTP connection to an internal IP, a behaviour that can resemble staging or dropper malware.



Although the binary was unsigned, it is a **legitimate internal IT utility**, and no malicious payload was observed. This alert highlights user-executed binaries from non-standard locations, which can sometimes be abused for persistence or lateral movement.



The alert was associated with **MITRE ATT\&CK Execution – T1204.002 (User Execution: Malicious File)** to classify the observed behaviour. The technique indicates the type of activity, not that it is an actual attack. The EDR logged the activity and marked the indicators as safe, preventing any potential impact.

---

### **Assessment**



Based on process execution, location, and network activity, this alert was assessed as a **false positive**. The observed behaviour was unusual but involved a legitimate internal tool. This case demonstrates the importance of monitoring user-space binaries executing from non-standard directories and correctly identifying false positives during alert triage.

--- 

### **Evidence**



* [Process chain](./Process-chain.png)

