# **Port Scanning and Service Enumeration (Nmap)**




### **Overview**



This assessment demonstrates the use of Nmap to identify active services and exposed ports on a local system.

All scans were conducted against the loopback interface (127.0.0.1) within a Kali Linux virtual machine to analyse service exposure, scan behaviour and result interpretation.


---

### **Scan Techniques**
### **● TCP SYN Scan (-sS)**



A TCP SYN scan was performed to identify open TCP ports without completing the full TCP handshake.



**Result summary:**

* Ports 80/tcp and 8080/tcp were identified as open
* All other scanned ports were closed and responded with TCP reset packets



**Analysis:**

The SYN scan successfully identified the presence of two active HTTP services with minimal noise.

The results confirm that the web services are actively listening on the local system and that no additional unexpected TCP services are exposed within the default scan range.



###### 

### **● TCP Connect Scan (-sT)**



A TCP connect scan was executed to compare results when completing the full TCP three‑way handshake.



**Result summary:**

* Same open ports detected: 80/tcp and 8080/tcp
* Closed ports responded with connection refused messages



**Analysis:**

The results matched the SYN scan, confirming consistency across scan types.

This scan demonstrates how service discovery remains reliable even when raw packet privileges are not available, albeit with increased detectability.





### **● UDP Scan (-sU)**



A UDP scan was performed to identify exposed UDP services.



**Result summary:**

* No open UDP ports detected
* All scanned UDP ports returned ICMP port unreachable responses



**Analysis:**

The absence of open UDP services indicates that no common UDP-based services (e.g., DNS, SNMP, NTP) are running on the system.

This reduces the overall attack surface and highlights how UDP scans often yield limited results in minimal lab environments.





### **● Full Port Scan (-p-)**



A full TCP port scan was conducted to enumerate all 65,535 TCP ports.



**Result summary:**

* 80/tcp – HTTP
* 8080/tcp – HTTP (Apache)
* 42069/tcp – Unknown service



**Analysis:**

The full port scan revealed an additional high‑numbered open port that was not visible during the default scan.

This demonstrates the importance of full port enumeration, as services running on non‑standard ports may otherwise remain undetected and represent potential security risks if misconfigured.





### **● Service Version Detection (-sV)**



Service version detection was used to identify the software running on exposed ports.



**Identified services:**

* 80/tcp: Python BaseHTTPServer 0.6 (Python 3.13.9)
* 8080/tcp: Apache HTTP Server 2.4.25 (Debian)



**Analysis:**

Version detection confirms that two separate HTTP services are accessible on the system.

Identifying service versions is critical during reconnaissance, as outdated or misconfigured services may introduce additional risk in real-world environments.




### **● OS Detection (-O)**



Operating system fingerprinting was performed.



**Result summary:**

* Linux kernel versions 5.x–6.x detected
* Network distance: 0 hops



**Analysis:**

Accurate OS detection was achieved due to the scan being executed against the local host.

In real network scenarios, OS fingerprinting may be less precise due to firewalls and network filtering.





### **● Aggressive Scan (-A)**



An aggressive scan was used to combine OS detection, version detection and script scanning.



As shown in the [scan output](scan-output.png), the following elements were identified:



* DVWA (Damn Vulnerable Web Application) login page identified on both HTTP services
* Missing HttpOnly flag on session cookies
* robots.txt file detected
* HTTP proxy behaviour flagged on port 8080



**Analysis:**

The aggressive scan provided extensive information but generated significantly more noise.

While highly informative in lab environments, this scan would be easily detected in production networks.





### **● Default Script Scan (-sC)**



Produced similar results as -A for web-related findings (title, robots.txt, cookie flags).



**Analysis:**

Confirms common misconfigurations; no additional critical information compared to aggressive scan.





### **● Scan Output Preservation (-oA)**



To ensure proper documentation and reproducibility of the assessment, the results of the aggressive scan (-A) were saved using Nmap’s -oA option.



This generated output files in three different formats:



* .nmap – standard human‑readable output
* .gnmap – grepable format for quick filtering and correlation
* .xml – structured output suitable for automated processing and reporting tools



**Analysis:**

Saving scan results in multiple formats allows for efficient reporting, later review and integration with other security tools, reflecting common practices used during professional security assessments.

---

### **Conclusion**



This assessment demonstrates how Nmap can be used to methodically identify exposed services, enumerate software versions and evaluate potential security risks.

Although the scans were conducted against the local system, the same principles apply to remote reconnaissance when adjusted for network segmentation and defensive controls.

