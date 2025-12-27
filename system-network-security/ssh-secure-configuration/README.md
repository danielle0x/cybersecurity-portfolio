# **SSH Setup and Secure Access Between Ubuntu Machines**



### **Description**

This project demonstrates how to set up secure remote access between two Ubuntu machines using SSH. It includes **passwordless login** with **SSH keys** and security hardening by disabling password authentication.

---

### **Technical Environment**

* **Platform:** Linux Server (Debian-based) and Client
* **Protocol:** OpenSSH
* **Core Feature:** ED25519 key pairs

---

### **Key Implementation \& Security Hardening**

**1\. Server and Client Setup**

Installed the OpenSSH server package and ensured the service was active and enabled for automatic startup on the target machine.

The corresponding OpenSSH client package was also installed on the client machine to complete the environment setup.



* Server installation Command: `sudo apt install openssh-server -y`

* Client installation Command: `sudo apt install openssh-client -y`



**2. Key Generation and Deployment (Passwordless Access)**

To enforce a higher level of security, an **ED25519 key pair** was generated on the Client machine, and the public key was deployed to the Server.



* Key Generation (Client): `ssh-keygen -t ed25519`
* Key Deployment (Client to Server): `ssh-copy-id username@server-ip`



**3.Critical Security Configuration Update**

Modified the SSH daemon configuration file (**/etc/ssh/sshd\_config**) on the Server to enforce key-based access and prevent common attack vectors.



* Set `PasswordAuthentication no` to mitigate **brute-force risks**, forcing key usage.
* Enable `PubkeyAuthentication yes`, making secure SSH key pairs mandatory for all remote access.

Optionally, the SSH service can be configured to listen on a **non-standard port**, which reduces automated scanning attempts, while key-based authentication remains the primary security control.



The SSH service was restarted to apply the changes.



* Service Restart: `sudo systemctl restart ssh`

---

### **Final Result**

Successfully connected from the Client to the Server without requiring a password, confirming the success of the **key-based authentication** implementation.



* Connection Command: `ssh username@server-ip`




