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

