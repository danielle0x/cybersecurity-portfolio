# **Windows Host Compromise: NIST Incident Response Lifecycle Implementation**

### **Overview**

This project documents a structured, end-to-end incident response investigation on a **compromised Windows workstation**. The objective was to **isolate an active threat**, identify the **initial infection vector**, analyse the attacker’s **persistence mechanisms**, and fully remediate the host using standard **containment, eradication,** and **recovery workflows**.
The incident handling process was executed in strict alignment with the **NIST SP 800-61 Rev. 2** Incident Handling Guide, transforming raw system anomalies into a structured forensic timeline.


**01. Detection & Analysis**

I initiated the investigative activity by analysing the machine to identify the root cause of the abnormal resource consumption.

Through a triage of active processes in Task Manager, I isolated a suspicious executable named `32th4ckm3.exe`. The process was running directly under the local user profile and consuming a critical percentage of the CPU.

Inspecting the file properties revealed that the executable was residing within a temporary system directory: `C:\Users\User\AppData\Local\Temp`. This specific file path is a strong indicator of unauthorised software deployment or a quietly dropped second-stage payload.

To determine if the threat was actively communicating with an external entity, I verified network socket connections using the Command Prompt. By filtering the active network streams against the process ID (PID) of the malware using the command `netstat -aofn | find "3520"`, I detected an active TCP session. The host was maintaining a stable connection to the remote IP address `45.33.35.156` on the non-standard port `42424`, confirming a live Command and Control (C2) beacon or active data exfiltration channel.

* [Task Manager and netstat command prompt.](./evidence/task-manager.png)

---

**02. Identifying the Infection Vector**

Once the compromise was confirmed and the C2 network footprint was isolated, I shifted my analysis backwards to establish the initial access vector.

I conducted an audit of the browser download history (`edge://downloads/all`) and isolated the origin of the infection. The user had downloaded a macro-enabled Microsoft Word document named `invoice n. 65748224.docm`. The file originated directly from a public external IP address rather than a verified business domain.

* [Browser download history.](./evidence/browser-history.png)

I performed a deep-dive analysis of the Word document using the built-in VBA Editor to inspect how native security warnings were bypassed. Upon opening the file, an embedded macro named `AutoOpen` automatically triggered a sequence of obfuscated administrative commands:

**1. Process Inspection:** The macro queried WMI services (`winmgmts`) to check if the target malware executable was already active on the machine, terminating its own script if true to avoid running duplicate instances.

**2. Living-off-the-Land (LotL) Download:** If the process was not active, the macro abused the native, trusted Windows administrative utility `certutil` to quietly download the malicious executable from the C2 IP, dropping it directly into the user's Temp directory. This execution happened through a hidden command prompt (`vbHide`) to avoid alerting the victim.

**3. Persistence Injection:** Finally, the macro constructed a command string to alter the operating system's startup configuration, guaranteeing the malware the ability to execute automatically upon system boot.

* [VBA Editor macro code.](./evidence/macro-code.png)

---

**03. Containment Strategies**

With the nature of the threat fully mapped, I immediately implemented containment strategies to isolate the host and prevent the attacker from moving laterally across the internal corporate network.

I instantly cut off the workstation from the local network by disconnecting its network interface. Following network isolation, I forcibly terminated the malicious engine process (`End Task`) via Task Manager to stop further resource exhaustion and break the active C2 session.

During my analysis, I harvested the following Indicators of Compromise (IoCs) to launch defensive sweeps and implement blocklists on enterprise firewalls and EDR solutions:

* **C2 IP & Port:** `45.33.35.156:42424`

* **Payload Delivery URL:** `xttp://172.233.61.246`

* **Local Dropped File Path:** `C:\Users\User\AppData\Local\Temp\32th4ckm3.exe`

---

**04. Eradication & Recovery**

The final phase focused on completely eradicating all traces left by the threat actor to return the workstation to a verified, clean operating baseline.

My prior macro code analysis confirmed that the attacker abused the Windows Registry to maintain persistent access to the workstation. Navigating through the Registry Editor (`regedit`), I located the malicious configuration inside the user's automated startup hive:

* **Registry Path:** `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`

* **Value Name:** `MyApp` (configured to point directly to the malicious executable path inside the Temp directory).

I permanently deleted the `MyApp` persistence key to prevent the malware from executing during future user logons. Once the registry configuration was sanitised, I manually purged the raw executable file `32th4ckm3.exe` from the temporary folder, removed the malicious decoy Word document, and cleared the browser cache, fully restoring the host to a clean baseline.

* [Registry Editor key.](./evidence/registry-key.png)
