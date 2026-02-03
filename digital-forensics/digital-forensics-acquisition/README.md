# **Digital Forensics Acquisition – FTK Imager Project**



### **Description**

To perform forensically sound acquisitions of a removable storage device (USB drive) using FTK Imager, creating both physical and logical images in multiple formats to ensure data integrity and chain of custody.

---

### **Technical Environment**

* **Tool:** AccessData FTK Imager and Hardware USB Write Blocker



* **Target Device:** Removable USB Storage (Source Evidence)



* **Image Formats Created:** RAW (.dd) and EnCase (.E01)


---


### **Key Implementation Steps**

**1.  Device and Environment Preparation**



* The target device (USB drive) was prepared for a non-invasive, read-only acquisition.



* FTK Imager was utilised in conjunction witha portable Hardware USB Write Blocker to ensure that no write commands were executed on the source media during the imaging process, maintaining the **integrity of the evidence.**



**2\. Physical and Logical Acquisitions**

Acquisitions were performed for both the entire device and the active file structure, using two industry-standard formats for compatibility:



* **Physical Acquisition (Full Disk):** Captured the entire drive sector-by-sector (including deleted data and unallocated space). Formats created were RAW (.dd) and E01 (EnCase Format).



* **Logical Acquisition (File System):** Extracted specific active files and folders based on the existing file system structure. Formats created were also RAW (.dd) and E01.



**3\. Verification and Integrity Check**

After acquisition, a crucial integrity check was performed to verify the authenticity of the captured image files against the source media.


* **Verification Process:** FTK Imager's built-in verification engine calculated the Computed Hash from the source data and compared it against the Reported Hash of the forensic images.
* **Hashing Algorithm:** MD5 and SHA1 checksums were generated and verified.
* **Result:** The hash values of the source and the images matched, proving the integrity and non-tampering of the evidence during the entire lifecycle.

---

### **Final Deliverables**

A comprehensive inventory of all generated forensic files with multi-algorithm hash digests was created, ready for detailed analysis.

* [HashMyFiles Report Here](https://danielle0x.github.io/cybersecurity-portfolio/digital-forensics/digital-forensics-acquisition/HashList.html)

