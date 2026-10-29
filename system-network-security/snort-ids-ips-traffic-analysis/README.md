# **Snort IDS/IPS & Traffic Analysis**

### **Overview**

This project demonstrates a practical exploration of Snort as a Packet Sniffer, Network Logger, Intrusion Detection System (IDS), and inline Intrusion Prevention System (IPS). 

To set up the environment I used a Linux VM to simulate live network environments, execute pre-compiled traffic generation scripts, and test custom security signatures.

The goal of this write-up is to document the process of capturing raw traffic, transforming volatile packets into structured logs, and scaling up configurations from passive network detection to active inline prevention, as well as implementing optimised detection rules.


### **Deployment & Core Configurations**

**01. Packet Sniffing Mode**

Snort processes network traffic by stacking command flags to scale visibility layers natively.
* `-v` = Basic header info (IPs and ports).
* `-d` = Adds the application layer payload.
* `-e` = Adds the data-link (MAC address) layer details.
* `-X` = Full packet dump in HEX and ASCII (the most detailed mode).

These flags can be combined (like `sudo snort -vde`) depending on how deep you need to analyze a packet.

**Execution Milestone**

I captured raw packets live to analyse the different architectural layers of the network traffic. In my terminal output, I can explicitly trace the source/destination mapping (`10.66.119.228:40354 -> 10.66.165.68:80`), active TCP flags, hex stream memory arrays, and raw application payload extractions in the right-hand column.

* [Snort HEX and ASCII Payload Capture](./evidence/packet-capture.png)

---

**02. Packet Logging & Forensics**

Snort translates volatile network streams into permanent local storage configurations for offline analysis.

* **Binary Mode (-dev -l .):** creates a single binary packet capture (.log), readable only by tools like Snort, tcpdump, or Wireshark.
* **ASCII Mode (-dev -K ASCII -l .):** splits traffic into structured, human-readable text directories organised automatically by IP address and protocol.
* **BPF Filtering:** Leverages Berkeley Packet Filters directly in the CLI (e.g., `snort -r file.log icmp`) paired with the -n 10 flag to instantly micro-analyse targeted frames.

**Execution Milestone**

I configured Snort's logging output using the `-K ASCII -l .` engine parameter to change how data is saved. I verified via the command line that Snort's automated file management system successfully initialised, creating independent, human-readable storage directories on my filesystem named directly after the target network IP endpoints.

* [Snort ASCII Structured Directory Output](./evidence/directory-output.png)

---

**03. Intrusion Detection (IDS) Mode**

IDS mode monitors traffic patterns passively against a defined ruleset file without disrupting the physical network layer.

* Activated by pointing directly to the network configuration file (`-c /etc/snort/snort.conf`).
	* Alert Outputs (`-A`): `console` or `cmg` display alerts directly to the terminal interface. `fast` or `full` quiet the console and write structured warning indicators straight to log files.
	* Batch Auditing: Uses `--pcap-list="file1.pcap file2.pcap"` along with `--pcap-show` to forensically scan multiple historical packet capture files simultaneously while visually tracking the source of each alert.

**Execution Milestone**

I performed passive network data using bulk offline configurations against multiple historical captures. By combining the `--pcap-list` and `--pcap-show` directives combined with CLI pipelines, it enables rapid multi-capture forensic scanning while maintaining absolute visibility over the batch file execution history.

* [Snort Automated Bulk PCAP Forensic Scan](path/to/your/cropped_bulk_analysis.png)

---

**04. Intrusion Prevention (IPS) Mode**

IPS mode dynamically drops or terminates malicious sessions instantly when a rule matches an active threat vector.

* **Inline Infrastructure Setup:** Activating the Data Acquisition engine (`--daq afpacket`) and bridging dual network interface cards via `-i eth0:eth1` positions Snort directly inside the traffic wire. 
* **Signature Enforcement Power:** Unlike passive monitoring, implementing a true blocking configuration requires passing explicit `drop` or `reject` rule actions within the loaded rule files to active state drops.

**Execution Milestone**

I deployed a proof of concept of an inline defensive signature targeting the ICMP protocol to test active prevention. By setting the rule action to drop, the engine successfully simulates infrastructure hardening against unauthorised ping sweeps and network discovery scans.

* [Snort Active Inline IPS Packet Dropping](./evidence/packet-dropping.png)

---

**05. Custom Signature Engineering**

Writing optimised rules is the absolute foundation of a successful deployment, an IDS/IPS is only as effective as the signatures it enforces. Poorly written rules either blind your network to active exploits or flood your security console with false positives.

Defensive rule architecture consists of a fixed Header (Action, Protocol, IPs, Ports, Direction) and specific Options (Metadata, Payload strings, and Header targets).

* Payload matching: Looks inside the packet for specific text strings or hex codes using the `content` option and can use `nocase` to ignore capital letters and `fast_pattern` to scan traffic faster.
* Non-payload matching: Inspects the packet headers to find specific IP IDs, TCP flags, or anomalies like duplicate source and destination IPs.

**Execution Milestone**

I implemented optimised, enterprise-grade signatures inside the `local.rules` repository to showcase defensive rule engineering focused on eliminating false positives.

The configuration features a targeted HTTP payload analysis rule that isolates directory traversal attempts by chaining `content:"GET"` with `http_method` and specific path-traversal strings.

At the transport layer, the architecture leverages stateful thresholding via a dynamic `detection_filter` to flag aggressive `flags:S` port scans while ignoring standard TCP handshakes, alongside structural constraints using `flags:PA` and `dsize:>1000` rules to intercept anomalous bulk data transfers. 

Finally, the configuration deploys a protocol abuse trap utilising the `sameip` keyword to instantly detect and mitigate self-looping Land Attacks.

* [Snort Custom Ruleset Architecture ](./evidence/ruleset.png)
