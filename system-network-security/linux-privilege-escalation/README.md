# **Linux Privilege Escalation – Known Kernel Vulnerability Validation**



### **Overview** 



This project focuses on validating the impact of a publicly documented Linux kernel vulnerability ([CVE‑2015‑1328](https://www.cve.org/CVERecord?id=CVE-2015-1328)) in a controlled virtual environment.



The goal was not to develop a new exploit, but to understand how **kernel‑level vulnerabilities can lead to privilege escalation** and to evaluate the importance of timely patching and system hardening.



A publicly available proof‑of‑concept was executed on a vulnerable virtual machine to demonstrate how a local, unprivileged user can gain **root privileges** when security updates are missing

---

### **Environment**



* Linux virtual machine
* **Kernel version:** Linux 3.13.0‑24‑generic (vulnerable)

---

### **Methodology** 



**1\.** Identified kernel version and mapped it to known CVEs



**2\.** Reviewed vulnerability description and impact



**3\.** Executed a public proof‑of‑concept to validate exploitability



**4\.** Verified privilege escalation (root access)



**5\.** Analysed defensive measures and mitigations


---


### **Vulnerability Description** 



**CVE-2015-1328** is a local privilege escalation vulnerability in the Linux kernel related to the overlayfs implementation.  

The issue is caused by improper permission checks during file creation in the upper directory of an overlay filesystem.  

In configurations where overlayfs is allowed within an arbitrary mount namespace, a local unprivileged user can exploit this flaw to obtain root privileges.

---

### **Mitigations \& Defensive Considerations**



* Apply kernel security updates



* Enable exploit mitigations (KASLR, SMEP, SMAP)



* Restrict local user access



* Monitor abnormal privilege escalation attempts
