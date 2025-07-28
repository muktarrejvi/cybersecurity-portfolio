***Chapter 12*** 

## 🔐 Intrusion Detection and Prevention – Key Takeaways

- **Intrusion Detection Systems (IDS):**  
  Monitor network traffic for signs of potentially malicious activity and alert administrators.

- **Intrusion Prevention Systems (IPS):**  
  Detect threats **and** take immediate corrective action to block malicious traffic.

- **Detection Methods Used by IDS/IPS:**  
  - **Signature Detection:** Matches known patterns of malicious activity.  
  - **Anomaly Detection:** Identifies deviations from normal behavior.

- **Types of Errors:**  
  - **False Positives:** Incorrectly flagging normal activity as malicious.  
  - **False Negatives:** Failing to detect actual malicious activity.

> ⚠️ It's crucial to balance detection sensitivity to minimize false alerts while ensuring strong protection.



## 🛡️ Key Takeaways from the "Malware Prevention" Video

- **Antimalware Software**  
  Modern antimalware software protects against a wide range of threats including viruses, worms, Trojan horses, and spyware.

- **Signature Detection**  
  Relies on databases of known malware signatures to scan and identify malicious files.  
  🔄 **Frequent updates** to virus definition files are essential to remain effective.

- **Heuristic / Behavior Detection**  
  Uses models of normal system behavior to detect anomalies.  
  📌 Common in advanced tools like **Endpoint Detection and Response (EDR)** solutions, providing real-time threat protection.

- **Sandboxing**  
  Suspicious files are executed in a **controlled, isolated environment** (sandbox) to detect harmful behavior **before** they affect the actual system.

- **Windows Defender**  
  Built-in antimalware solution in Windows that offers real-time protection, scanning, threat history, and automatic updates.


## 🌐 Key Takeaways from the "Port Scanners" Video

- **Port Scanners**  
  Tools that probe a system for **open network ports**, helping identify potentially vulnerable points of entry.

---

### 🔧 Types of Vulnerability Assessment Tools

- **Port Scanners** – Probe systems for open network ports.  
- **Vulnerability Scanners** – Check open ports for known vulnerabilities.  
- **Application Scanners** – Test web applications for flaws and misconfigurations.

---

### ⚙️ Functionality of Port Scanners

Port scanners test **all 65,535 network ports** on a server to determine which are open —  
💡 *This is similar to rattling all the doorknobs on a house to find unlocked doors.*

---

### 🛠️ Popular Tool: `nmap`

- Demonstrated tool: **nmap**, a widely-used port scanner.
- Basic Command:  
  ```bash
  nmap [IP address]

## 🛡️ Key Takeaways from the "Vulnerability Scanners" Video

- **Functionality**  
  Vulnerability scanners do more than just identify open ports. They **analyze the services running on those ports** and **check for known vulnerabilities** in configurations, software, and protocols.

---

### 🛠️ Popular Tool: **Nessus**

- Demonstrated in the video as a **web-based vulnerability scanning tool**.
- Designed to scan systems like **Windows servers** for a wide range of known issues.

---

### 📋 Scan Results

- Nessus identifies vulnerabilities such as:
  - **SSL certificate problems**
  - Use of **medium-strength cipher suites**
  - Additional misconfigurations and outdated software
- It also provides:
  - **Detailed vulnerability descriptions**
  - **Remediation guidance** to help secure the system

