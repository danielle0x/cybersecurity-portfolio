# **Windows Threat Detection: Initial Access Analysis & Event Log Auditing**

### **Overview**

This project documents the forensic analysis and log investigation of multiple **Initial Access methods** targeting Windows environments. The objective was to utilise the native **Windows Event Viewer** to parse specialised log channels, tracing distinct attack chains including **RDP brute-force exploitation**, weaponised **phishing attachments** (LNK and double-extension files), and **malicious removable media** execution. The process focused on auditing raw `.evt` and `.evtx` telemetry streams to isolate event IDs, map execution timelines, and identify indicators of compromise (IoCs).


**01. Remote Desktop Protocol (RDP) Breach Analysis**

I initiated the investigation by opening **Event Viewer** and navigating to the standard Windows **Security Logs** channel to reconstruct an unauthorised external access scenario over an exposed RDP interface.

An analysis of **Event ID 4625 (Failed Logon)** revealed a high-volume, automated brute-force campaign actively targeting the host. The log stream showed hundreds of rapid authentication failures concentrated against the native `Administrator` account, indicating a credential-guessing pattern common to botnet scanners.

By modifying my Event Viewer filters to track successful authentication logs under **Event ID 4624 (Successful Logon)** paired with **Logon Type 10** (Remote Interactive / RDP), I confirmed that the threat actor successfully guessed the credential baseline and established initial entry. Cross-referencing the XML log data isolated the attacking perimeter IP address `203.205.34.107` and mapped the threat actor's originating source workstation hostname: `DESKTOP-QNBC4UU`.

* [Event Viewer RDP breach indicators.](./evidence/RDP.png)

---

**02. Phishing Vector: Malicious Shortcuts & Double-Extensions**

Following the host infrastructure audit, I pivoted to the **Sysmon Operational Logs** channel within Event Viewer (`Applications and Services Logs > Microsoft > Windows > Sysmon > Operational`) to analyse a phishing-driven delivery chain.

Reviewing the file system triage logs, I tracked a multi-stage infection sequence originating from an unarchived archive file. The user downloaded a compressed file named `top-cats.zip` via their web browser, which was subsequently unpacked into the `C:\Users\Administrator\Pictures` folder.

Inside the directory, the user was tricked into executing a double-extension file designed to mimic a benign image asset: `best-cat.jpg.exe`. **Sysmon Event ID 1 (Process Create)** log streams confirmed that launching this binary initialised the malware process under **PID 5484**.

Further inspection of associated LNK files revealed that the attacker modified shortcut target paths to execute hidden secondary-stage payloads. An icon mimicking a benign web URL named `Official Website` was altered under the hood to target the system shell natively. By parsing the command-line arguments inside Sysmon Event ID 1 (Process Create), I caught the execution parameters explicitly forcing `powershell.exe` to quietly fetch an external script from a remote staging server: `wp16.hqywlqpa.thm:8000/cgi-bin/f`. 

The shortcut passed this network resource directly into a `.Content` method, demonstrating a critical **Living-off-the-Land (LotL)** download pattern used to pull a secondary-stage web payload into volatile host memory without saving the raw script onto the physical disk.

The network telemetry harvested from the process creation logs confirmed that the active binary attempted outbound command-and-control connection cycles directly to the malicious external domain: `rjj.store`.

* [LNK structural shortcuts](./evidence/lnk.png) and [network logs.](./evidence/network-activity.png)

---

**03. Removable Media (USB) Attack Tracking**

The final phase of the investigation focused on detecting physical initial access vectors by auditing specialised process tracking events within **the Sysmon log repository**.

By reviewing **Sysmon Event ID 1** records, I intercepted an attack chain simulating a hardware delivery campaign where the threat actor relied on graphical user interaction to induce the victim to double-click a file directly from a connected flash drive. The execution baseline was explicitly caught by tracing the parent process image directly back to the Windows shell: `C:\Windows\explorer.exe`.

The initial execution vector was identified as a binary named `Open Sandisk 4GB USB.exe`, which ran directly from the volatile storage boundaries of an external USB drive path designated as `E:\Open Sandisk 4GB USB.exe`.

Once the initial process became active, it acted as a dropper to establish persistent host residency. By monitoring **Sysmon Event ID 11 (File Create)** logs, I verified that the malware quietly dropped a secondary malicious file named `winupdate.exe` deeper into a local hidden directory: `C:\Users\Public\Documents\winupdate.exe`.

Furthermore, forensic log signatures confirmed that the threat possessed self-propagating capabilities. After establishing a foothold on the local disk, the malware scanned the system's hardware bus to identify additional attached storage media and successfully propagated its malicious payload onto a secondary connected USB interface designated as drive letter `F:`.

* [Sysmon Event USB drive execution](./evidence/usb-execution.png) and [file drops.](./evidence/usb-drop.png)
