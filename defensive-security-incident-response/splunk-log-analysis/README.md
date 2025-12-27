# **Splunk Log Analysis – Web Server Compromise Investigation**



**Environment:** Simulated SOC environment

**Data sources:** Web server logs, Firewall logs  

**Tool:** Splunk Search \& Reporting  



---



### **Overview**

In this project, I investigated a simulated web server compromise using Splunk.
By analysing the web traffic and firewall logs, I reconstructed the full attack chain, from initial reconnaissance to data exfiltration, identifying key malicious activities and potential vulnerabilities.



---



### **Investigation \& Findings**



**1.Traffic Anomaly Detection**

I conducted a time-based analysis and identified an abnormal spike in web traffic on 2025-10-12, totaling 2,267 events, indicating the likely attack window.



* [View Traffic Spike](./evidence/traffic-spike.png)







**2. Attacker Identification**

By filtering out legitimate browser traffic, I determined a single external IP responsible for the majority of automated requests, accounting for 7,876 events.



* [Suspicious IP](./evidence/suspicious-IP.png)







**3. Reconnaissance Activity**

I analysed requests targeting sensitive system paths using non-browser tools such as curl, wget, zgrab, and Go-http-client.

Some of these requests included directory traversal attempts aimed at accessing system files (e.g., /etc/passwd) and returned a mix of HTTP responses (200, 400, 500), indicating active probing and the presence of a path traversal vulnerability.



* [Table of reconnaissance paths](./evidence/directory-traversal.png)







**4. Exploitation Attempts**

I analysed multiple SQL injection payloads were observed targeting application parameters.  

The presence of Havij and sqlmap user agents, together with time-based SQL payloads (e.g., 'SLEEP(5)'), indicates active SQL injection exploitation attempts against the application.



* [SQLi events](./evidence/sqli-events.png)







**5. Post-Exploitation \& Remote Code Execution**

I observed requests to a malicious PHP web shell in the web application logs, which was subsequently used to execute an external binary ('bunnylock.bin') on the compromised server.  

This activity confirms that the attacker achieved remote code execution (RCE) following successful exploitation of the application.



* [Web shell and binary execution logs](./evidence/web-shell.png)





**6. Command-and-Control (C2) Communication \& Data Exfiltration**


I analysed firewall logs and confirmed outbound connections initiated by the compromised server toward the attacker-controlled external IP address.

The analysis of network traffic revealed a significant volume of data transferred, indicating successful data exfiltration and active command-and-control (C2) communication.



* [Firewall logs showing C2 communication and data exfiltration](./evidence/c2-traffic.png)



---



### **Impact Summary**



The investigation confirmed a **full compromise** of the web server.  
The attacker successfully progressed through multiple attack stages, resulting in remote code execution, establishment of a command-and-control (C2) channel and large-scale data exfiltration.



This scenario demonstrates the potential business impact of web application vulnerabilities when combined with insufficient monitoring and privilege controls.

---

### **Mitigations & Defensive Recommendations**

* Enforce strict input validation and parameterized queries to prevent SQL injection attacks.
* Apply the principle of least privilege to database users, removing FILE and administrative permissions.
* Disable directory listing and implement proper path validation to mitigate directory traversal attempts.
* Restrict web server write permissions to prevent unauthorized file creation (e.g., PHP web shells).
* Monitor and alert on non-browser user agents and anomalous request patterns.
* Implement outbound traffic monitoring to detect potential C2 communication and data exfiltration.
* Prefer modern encryption and security configurations where applicable (e.g., secure authentication mechanisms).




