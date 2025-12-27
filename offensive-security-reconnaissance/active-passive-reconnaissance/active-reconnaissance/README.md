# **Active Reconnaissance – Network Interaction**



### **Overview**



This project focuses on active reconnaissance techniques performed in a controlled virtual environment.
The goal was to **interact directly** with target systems in order to collect network and host-level information, while evaluating how visible and detectable these actions are from a defensive perspective.

---

### **Objectives**



* Understand the purpose, usefulness and risks of active reconnaissance.



* Identify live hosts, reachable services and network paths.



* Observe how direct probing techniques generate detectable network traffic.



* Evaluate the security impact of exposed services and open ports.

---

### **Techniques Used and Observations**



### ● **Ping (ICMP)**



Ping was used to identify whether the target machine was online and reachable within the lab network.

By sending multiple ICMP echo requests, it was possible to confirm host availability and measure round-trip time, which helped assess basic network responsiveness.



**Command used:**



`ping -c 10 MACHINE_IP`





**Observation:**

The target host responded consistently to ICMP requests, confirming that it was active. The stable latency suggested a local or lightly segmented network. This also demonstrated how ICMP traffic can easily reveal live systems during reconnaissance.


######


### ●  **Traceroute**



Traceroute was used to map the network path between the attacking machine and the target. This allowed the identification of intermediate network devices and provided insight into the network topology.



**Command used:**



`traceroute MACHINE_IP`





**Observation:**

The output revealed a single hop, consistent with a virtualized lab environment. This confirmed the presence of intermediate routing components and highlighted how traceroute can expose internal network structure if not properly restricted.





### ● **Telnet**



Telnet was used as a simple method to probe specific TCP ports and verify whether services were listening and accepting connections.



**Command used:**



`telnet MACHINE_IP 80`





**Observation:**

Successful connections indicated that the target service was active and reachable, showing a server using **nginx/1.6.2.** This demonstrated how legacy tools like Telnet can still be useful for basic service enumeration during active reconnaissance.





### ●  **Netcat**



Netcat was used to actively interact with network services and test direct TCP connectivity.


**Commands used:**



`nc MACHINE_IP 80`





**Observation:**

Netcat successfully established connections to exposed services, confirming nginx/1.6.2 service availability and responsiveness. 

---

### **Defensive Perspective**



Active reconnaissance activities generated clear and observable network traffic, including ICMP echo requests and TCP connection attempts.



* Repeated ping and traceroute activity would be easily detectable by firewalls and IDS/IPS systems.



* Direct interaction with services creates logs that can be correlated to identify*suspicious behaviour.



* Exposed services and unnecessary open ports increase the attack surface and should be restricted.



* Early detection of reconnaissance activity can allow defenders to respond before exploitation attempts occur.



This project reinforced the importance of monitoring early-stage network interactions as a key part of defensive security.

