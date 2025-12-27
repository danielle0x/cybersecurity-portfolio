# **Wi-Fi Security Evaluation – WPA/WPA2 Handshake Capture**



### **Overview**


This project provides a technical overview of a WPA/WPA2 wireless security workflow, emphasising both offensive techniques and defensive implications.

The focus is on illustrating how weaknesses in **WPA/WPA2-PSK** authentication can be leveraged to obtain a **4-way handshake** and how captured authentication data can be evaluated through **offline password analysis.**

--- 

### **Environment**



**Operating System:** Kali Linux (virtualised)



**Tools:** Aircrack-ng suite, Hashcat



**Target Context:** Personal hotspot

---

### **Assessment Workflow (Methodology)**



**1\. Wireless Interface Preparation**



The workflow begins with the identification of a compatible wireless interface and its configuration in monitor mode.

This step enables passive observation of IEEE 802.11 management and authentication frames without associating with the target network.

###### 

**2. Passive Reconnaissance**



A passive reconnaissance phase allows the identification of nearby access points and relevant metadata, including:



* BSSID



* Operating channel



* Encryption standard



* Presence of connected clients



This information is used to define the assessment scope and select the target access point.

######

**3. Targeted Authentication Traffic Analysis**



Once the target parameters are defined, traffic analysis is focused on the selected access point.

The objective of this phase is to observe the WPA/WPA2 authentication process and identify the conditions under which a 4-way handshake is generated.

######

**Handshake Generation via Client Reconnection**


If a handshake is not observed during passive monitoring, the workflow includes a controlled client **deauthentication** scenario.

This forces a **reconnection attempt**, resulting in the generation of new authentication material suitable for offline analysis.



This phase highlights the role of client behaviour in the exposure of WPA/WPA2 authentication data.

###### 

**4. Offline Password Strength Evaluation**


Captured handshake data can be analysed offline using industry-standard password auditing tools, such as Hashcat.

Because this phase is fully offline, it does not interact with the access point and remains invisible to network monitoring once the handshake has been obtained.



The analysis demonstrates that WPA/WPA2 security depends heavily on passphrase complexity rather than encryption strength alone.

---

### **Security Implications**


This assessment model shows that:



* WPA/WPA2 encryption algorithms remain cryptographically strong



* Weak or predictable passwords significantly reduce wireless security



* Handshake capture enables silent offline evaluation of password strength


---


### **Mitigations and Defensive Considerations**


To reduce exposure to this attack vector, the following defensive measures are recommended:



* Enforce strong, non-dictionary passphrases (16+ characters)



* Migrate to WPA3 where supported



* Disable WPS



* Monitor repeated authentication failures and deauthentication attempts


