**Beacon Frames** in Wi-Fi are management frames that periodically advertise the network's existence and can include information directing users to a captive portal.


for patterns of multiple entries in quick succession is the most effective technique to detect **tailgating**, as it identifies when multiple individuals enter after a single valid badge swipe, a typical indicator of tailgating.


## 📑 Agreements and Contracts in Cybersecurity & Business

---

### A. Service Level Agreement (SLA)
- A **formal contract** between a service provider and a customer.  
- Defines:
  - Expected **service quality** (e.g., uptime, response times).  
  - **Performance metrics** and reporting.  
  - **Penalties** for not meeting commitments.  
- Example: A cloud provider guaranteeing **99.9% uptime**.

---

### B. Memorandum of Agreement (MOA)
- A **formal and legally binding agreement** between two or more parties.  
- Specifies **roles, responsibilities, and obligations**.  
- Stronger than an MOU, but less detailed than a full contract.  

---

### C. Memorandum of Understanding (MOU)
- A **non-binding agreement** that outlines **intentions** and **collaboration plans**.  
- Used when parties want to express commitment but not yet enter a formal contract.  
- Example: Two companies agreeing to explore a **joint research project**.  

---

### D. Partnership Contract
- A **legally enforceable agreement** that establishes a business partnership.  
- Covers:
  - Profit/loss sharing.  
  - Partner responsibilities.  
  - Legal rights and dispute resolution.  
- Much broader than SLA, MOA, or MOU.  

---

✅ **Key Differences**:  
- **SLA** → Service performance commitment.  
- **MOA** → Formal, binding, roles defined.  
- **MOU** → Informal, non-binding, intent only.  
- **Partnership Contract** → Full legal partnership agreement.  

## 🌐 Types of VPNs

---

### A. Site-to-Site VPN
- Connects **two entire networks** (e.g., branch office ↔ headquarters).  
- Used by organizations with **multiple office locations**.  
- Transparent to end users; traffic between sites is encrypted.  
- Often configured on **routers or firewalls**.  

---

### B. Remote Access VPN
- Allows **individual users** to securely connect to a private network.  
- Example: Employees connecting to their company’s network from home.  
- Requires **VPN client software** or built-in OS support.  

---

### C. SSL/TLS VPN
- A type of **Remote Access VPN** that uses **SSL/TLS encryption**.  
- Users connect via a **web browser** (no special client needed).  
- Popular for secure access to **web applications, email, portals**.  
- Easier to deploy compared to traditional VPNs.  

---

### D. Layer 2 Tunneling Protocol (L2TP) VPN
- A VPN protocol that works at **Layer 2** (Data Link layer).  
- Typically combined with **IPSec** for encryption (L2TP/IPSec).  
- Provides strong security but can be **slower** due to double encapsulation.  
- Supported natively by most operating systems.  

---

✅ **Quick Comparison**
| VPN Type              | Best For                          | Notes |
|-----------------------|------------------------------------|-------|
| **Site-to-Site**      | Office-to-office secure links      | Configured on network devices |
| **Remote Access**     | Individual employee connections    | Requires client or OS support |
| **SSL/TLS VPN**       | Web-based secure access            | Works via browser, user-friendly |
| **L2TP/IPSec VPN**    | Secure tunneling with encryption   | Strong security, more overhead |


## 🦠 Virus – Characteristics

- A **virus** is a type of malware that:
  - **Attaches itself to executable files or programs**.
  - **Replicates** by spreading to other files and systems.
  - Often requires **user action** (e.g., running an infected file) to activate.  

- **Spread Mechanism**:
  - Via **file sharing**, **email attachments**, or **infected software**.
  - Once executed, the virus may spread across a **local network** or the internet.  

- **Key Point**:  
  Unlike worms (which spread automatically), viruses **depend on host files** and usually need **human interaction** to propagate.

## 📡 Malware Beaconing

- Workstations connect **periodically** to a **malicious IP**.  
- Sends **small data packets** to a **Command & Control (C2) server**.  
- Purpose: Get **instructions**, send **status updates**, or exfiltrate data.  
- **Indicator**: Regular outbound connections to suspicious domains/IPs.  


## 🛡️ Posture Validation Server (NAC)

- Part of **Network Access Control (NAC)**.  
- **Function**: Checks device compliance with security policies before allowing access.  
- Validates:
  - Antivirus status  
  - Patch levels  
  - Security configurations  
- **Purpose**: Ensure only **secure, compliant devices** connect to the network.  



## ⚙️ Standard Security Templates

- Applied via **automated deployment scripts**.  
- Ensure all servers follow **predefined security policies**.  
- Benefits:
  - **Consistency** in configuration  
  - Easier **compliance** with regulations  
  - Reduces **human error**  



## 🔄 Redundancy & Failover Concepts

- **(D) Active-Passive Failover**  
  - Secondary device takes over if primary fails.  
  - Ensures **continuous network operations**. ✅ Best for critical devices.  

- **(A) SPOF Mitigation**  
  - Identify & remove **Single Points of Failure**.  
  - Improves resilience but does not define redundancy method.  

- **(B) Network Segmentation**  
  - Divides network into zones for **security & performance**.  
  - Not a redundancy solution.  

- **(C) Spanning Tree Protocol (STP)**  
  - Prevents **Layer 2 loops**, provides some redundancy.  
  - Less comprehensive than **active-passive failover**.
  - 


  ## 🛰️ Command and Control (C2) Communication

- **C2 Communication (Correct)**  
  - Increased outbound traffic to an external server.  
  - Compromised systems communicate with attacker’s server for **instructions or data exfiltration**.  

- **(A) DDoS ❌**  
  - Overwhelms a target with traffic.  
  - Not traffic to a single external server.  

- **(C) Phishing ❌**  
  - Deceptive emails/websites to steal information.  
  - Not unusual traffic patterns.  

- **(D) XSS ❌**  
  - Injects malicious scripts into web pages.  
  - Runs on client-side, not external server communication.  

## 📊 Standardizing Data Protection Practices

- **Correct:** Ensures sensitive data is consistently protected per org. policies → reduces risk of breaches.  
- **Option A (❌):** Too broad — cannot guarantee compliance with all international regulations.  


## ⚙️ Automated Configuration Management Tools

- Ensure consistent configuration across all systems  
- Reduce human error  
- Enforce baseline security policies automatically  
- Detect and correct configuration deviations  

