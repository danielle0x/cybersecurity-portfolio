# **EDR Alert Assessment – Unsigned Binary Creating Scheduled Task for Persistence**



### **Description**



In this scenario, I analysed a simulated medium-severity EDR alert triggered by an **unsigned binary** (svcupdate.exe) executing from an unusual path (CUsersjohnAppDataLocalTemp). The binary created a scheduled task named WinUpdateService, a common technique used for **persistence**.



Scheduled tasks are frequently leveraged by attackers to maintain long-term access. Although the binary was unsigned and its behaviour suspicious, no malicious payload or further compromise was observed. The alert highlights how monitoring for unusual execution paths and task creation is important in identifying potential persistence attempts.



The alert was mapped to **MITRE ATT\&CK Persistence – T1053.005 (Scheduled Task)** to classify the observed behaviour. The technique indicates the type of suspicious activity but does not automatically imply a confirmed attack.

---

### **Assessment**



Based on process execution, file location, and task creation, this alert was assessed as a **true positive observation of suspicious behaviour**, demonstrating potential persistence tactics. No active compromise occurred, but the scenario illustrates the need for alert triage and careful evaluation of unsigned binaries performing system modifications.

---

### **Evidence**



* [Process chain](./process-chain.png)

