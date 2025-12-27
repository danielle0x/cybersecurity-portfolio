# **Passive Reconnaissance – OSINT \& External Attack Surface Mapping**



### **Overview**



This project demonstrates passive reconnaissance techniques to collect publicly available information about domains and internet-facing assets **without directly interacting** with target systems.

The goal was to assess how much information is unintentionally exposed through **OSINT** sources and how it can contribute to an organization’s external attack surface, while maintaining ethical and professional standards.

---

### **Objectives**



* Understand the role of passive reconnaissance in security assessments.



* Identify exposed domains, subdomains, IP addresses and services.



* Collect intelligence without triggering alerts or interacting with hosts.



* Emphasise ethical and professional considerations in reconnaissance activities.

---

### **What I Did**



* Enumerated subdomains using **Certificate Transparency Logs (crt.sh)**.



* Analysed DNS records including **A, AAAA, MX, NS** and **TXT** to understand mail and name server infrastructure.



* Identified publicly exposed services and ports using **Shodan** and **Censys.**



* Collected intelligence without interacting directly with any target systems.

---

### **Tools \& Techniques**



**WHOIS:** domain registration and ownership details.



**nslookup / dig**: DNS record analysis.



**crt.sh:** subdomain enumeration and historical certificate discovery.



**DNSDumpster:** mapping DNS infrastructure and hosting providers.



**Shodan \& Censys:** internet-wide visibility of services, software versions and potential misconfigurations.



**OSINT Framework:** structured reference for relevant tools and data sources.

---

### **Defensive Perspective**



Organizations can unintentionally expose sensitive information through DNS configurations, certificates and internet-facing services.



Awareness of this exposure allows defenders to:



* Reduce attack surface visibility.



* Audit certificate transparency logs for unintended leaks.



* Improve the accuracy of asset inventories.



* Monitor public data sources for changes that could increase exposure.



Understanding passive reconnaissance strengthens both **offensive and defensive security awareness** and informs better security practices.

---

### **Professional Note**



For ethical and professional reasons, specific target details and raw outputs are intentionally omitted. The focus is on methodology, reasoning and defensive implications.

