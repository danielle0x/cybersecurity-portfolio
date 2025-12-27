# **Host Discovery (Nmap)**



### **Overview**



This assessment demonstrates the use of Nmap host discovery techniques to identify live hosts within a local network segment.

All scans were executed against the private LAN subnet **192.168.1.0/24** with explicit consent.

All IP addresses, MAC addresses, hostnames and vendor information have been **anonymised** to preserve confidentiality.


---

### **Passive & Non-Intrusive Discovery**
### **● List Scan (-sL)**



`nmap -sL 192.168.1.0/24`



Lists all target IP addresses and performs reverse DNS resolution when available.

No packets are sent to the targets, so host availability is not determined.



**Result summary:**

* All IP addresses in the subnet were enumerated

* Reverse DNS names were resolved where possible



**Analysis:**

List scan is useful to verify scan scope and target ranges before executing active scans.



###### 

### **● Ping Scan (-sn)**



`nmap -sn 192.168.1.0/24`



Performs host discovery only, without scanning ports.

Used to quickly identify which hosts are online within the target network.



As shown in the [scan output](./Scan-output.png), here's the **result summary:**

* Several hosts (**16**) were detected as online

* MAC addresses and vendor information were resolved

* Provides a quick overview with minimal network noise



**Analysis:**

Ping scan is effective for **fast reconnaissance** but may miss hosts if ICMP traffic is blocked.



###### 

### **● ARP Ping (-PR)**



`sudo nmap -sn -PR 192.168.1.0/24`



Uses ARP requests to discover active hosts on the local network.

This is the **most reliable** host discovery method in LAN environments and requires elevated privileges.



**Result summary:**

* All live hosts in the subnet were reliably identified



**Analysis:**

ARP-based discovery provides the most accurate results in a LAN, as ARP packets cannot be filtered like ICMP.



###### 

### **● ICMP Echo Ping (-PE)**



`nmap -sn -PE 192.168.1.0/24`



Sends ICMP Echo Request packets (classic ping) to identify responsive hosts.



**Result summary:**

* Most live hosts responded to ICMP requests

* Some hosts did not respond due to firewall restrictions



**Analysis:**

ICMP Echo is simple and widely supported, but its reliability depends on network filtering policies.



###### 

### **● ICMP Address Mask Ping (-PM)**



`nmap -sn -PM 192.168.1.0/24`



Uses ICMP Address Mask Request packets.



**Result summary:**

* The same hosts detected via ICMP Echo Ping were identified

* No additional hosts were discovered in this environment



**Analysis:**

Address Mask Ping is an uncommon and mostly legacy ICMP type; it may reveal additional hosts only in misconfigured or older networks.



###### 

### **● ICMP Timestamp Ping (-PP)**



`nmap -sn -PP 192.168.1.0/24`



Sends ICMP Timestamp Request packets to identify live hosts.



**Result summary:**

* The same set of live hosts identified via ICMP Echo Ping responded

* Did not reveal additional hosts in this environment



**Analysis:**

In this environment, ICMP Timestamp requests did not reveal additional hosts compared to ICMP Echo Ping, indicating uniform ICMP filtering. 
However, in networks with selective ICMP policies, this technique may still be useful for host discovery.



###### 

### **● TCP SYN Ping (-PS)**



`sudo nmap -sn -PS80,443,22 192.168.1.0/24`



Performs host discovery by sending TCP SYN packets to specified ports.



**Result summary:**

* Hosts with open TCP ports **80, 443,** and **22** were detected

* Effective against hosts that block ICMP



**Analysis:**

TCP SYN discovery allows detection of live hosts through **service exposure** rather than ICMP.



###### 

### **● TCP ACK Ping (-PA)**



`nmap -sn -PA80,443,22 192.168.1.0/24`



Uses TCP ACK packets for host discovery.



**Result summary:**

* Similar live hosts detected as with TCP SYN

* Can **bypass certain firewall rules** without requiring elevated privileges



**Analysis:**

TCP ACK ping is useful in environments where TCP SYN is filtered or restricted.



###### 

### **● UDP Ping (-PU)**



`sudo nmap -sn -PU53,123 192.168.1.0/24`



Sends UDP packets to selected ports (e.g., DNS and NTP) to identify active hosts.



**Result summary:**

* The same set of live hosts previously identified responded to UDP probes

* Slower than TCP/ICMP scans due to timeout behaviour



**Analysis:**

UDP discovery is effective when TCP/ICMP traffic is filtered, but requires patience due to **slower responses.**


---


### **Conclusion**



This assessment demonstrate different Nmap host discovery techniques and show how to adapt reconnaissance strategies based on network restrictions, firewall behaviour and privilege level.

