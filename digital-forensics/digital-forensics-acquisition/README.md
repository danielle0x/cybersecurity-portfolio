# **Digital Forensics Acquisition – FTK Imager Project**



### **Description**

To perform forensically sound acquisitions of a removable storage device (USB drive) using FTK Imager, creating both physical and logical images in multiple formats to ensure data integrity and chain of custody.

---

### **Technical Environment**

* **Tool:** AccessData FTK Imager and HashMyFiles



* **Target Device:** Removable USB Storage (Source Evidence)



* **Image Formats Created:** RAW (.dd) and EnCase (.E01)


---


### **Key Implementation Steps**

**1.  Device and Environment Preparation**



* The target device (USB drive) was prepared for a non-invasive, read-only acquisition.



* FTK Imager was utilised, leveraging its **read-only functionality** to ensure that no write commands were executed on the source media during the imaging process, maintaining the **integrity of the evidence.**



**2\. Physical and Logical Acquisitions**

Acquisitions were performed for both the entire device and the active file structure, using two industry-standard formats for compatibility:



* **Physical Acquisition (Full Disk):** Captured the entire drive sector-by-sector (including deleted data and unallocated space). Formats created were RAW (.dd) and E01 (EnCase Format).



* **Logical Acquisition (File System):** Extracted specific active files and folders based on the existing file system structure. Formats created were also RAW (.dd) and E01.



**3\. Verification and Integrity Check**

After acquisition, a crucial integrity check was performed to verify the authenticity of the captured image files against the source media.



* **Hashing Algorithm:** Generated multiple industry-standard hash values for verification, including MD5, SHA1, SHA-256, and SHA-512, for both the source drive and the created image files (Physical and Logical).
* **Result:** The hash values of the source and the images matched, proving the integrity and non-tampering of the evidence.

---

### **Final Deliverables and Proof of Integrity**

The successful execution resulted in verified, forensically sound image files, ready for detailed analysis.

* [HashMyFiles Report Here](./HashList.html)

