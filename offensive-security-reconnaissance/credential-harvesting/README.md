# **Social Engineering Credential Harvesting – SET**



### **Overview**



This project demonstrates a social engineering credential harvesting attack performed in a controlled virtual environment.

The objective was to understand how attackers can capture user credentials by leveraging fake login pages and to analyse the risks associated with **human trust rather than technical vulnerabilities.**



The assessment focuses on the attack workflow, the interaction between attacker and victim systems, and the visibility of such attacks from a defensive perspective.


---


### **Environment Setup**



The environment was built using two virtual machines to simulate a realistic attack scenario:



**Attacker Machine**



* **OS:** Kali Linux



* **Tools:** Social Engineering Toolkit (SET), Apache



* **IP address:** 10.6.6.2



**Target Machine**



* **OS:** Linux-based VM



* **Application:** Damn Vulnerable Web Application (DVWA)



* **IP address:** 10.6.6.1



Both virtual machines were configured in bridged mode and assigned IP addresses from the same local network, allowing direct host‑to‑host communication.


---


### **Attack Scenario**



The attack simulates a credential harvesting scenario where an attacker clones the DVWA login page and captures credentials submitted by a victim.



Rather than exploiting application-level vulnerabilities, this attack targets user behaviour, highlighting how credentials can be compromised even when no software vulnerability is present.


---


### **Methodology**



**1. Target Application Setup**



DVWA was installed and configured on the target virtual machine to simulate a real-world web application requiring user authentication.



**2. SET Configuration**



On the Kali Linux machine, the Social Engineering Toolkit (SET) was used with the following attack vector:



* Website Attack Vectors



* Credential Harvester Attack Method



* Web Cloner / Custom Login Page



A controlled login page was used to demonstrate how credentials can be captured when users submit authentication data to a malicious endpoint.



**3. Credential Harvesting**



When a user entered credentials into the fake login page, SET intercepted the HTTP POST request containing the username and password fields and logged the credentials locally on the attacker machine.

This demonstrated how attackers can successfully collect usernames and passwords without exploiting technical vulnerabilities.


---


### **Results**



The attack successfully captured submitted credentials, which were logged by SET during the session.
This confirms the effectiveness of **social engineering attacks** when users trust malicious interfaces.



**Evidence:**



* [captured credentials output](./Output.png)


---


### **Defensive Considerations**



* Users should be trained to recognise suspicious login pages and URLs



* HTTPS alone does not prevent social engineering attacks



* Multi-factor authentication (MFA) significantly reduces the impact of credential theft



* Monitoring unusual authentication patterns can help detect harvesting attempts
