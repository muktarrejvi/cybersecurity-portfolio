## 🔐 Security Fundamentals – Key Concepts

---

### 🔺 CIA Triad
Security is built around three core principles:

- **Confidentiality** – Protecting the secrecy of information.
- **Integrity** – Ensuring data is accurate, complete, and unaltered
- **Availability** – Ensuring information is accessible when needed

---

### 🔐 Authentication
Verifies **who** someone is using one or more factors:

- **Type 1:** Something you know (e.g., password)
- **Type 2:** Something you have (e.g., smart card)
- **Type 3:** Something you are (e.g., fingerprint).

---

### 🧾 Authenticity
- Ensures the **message** comes from a trusted source and **hasn't been modified**.

---

### ✍️ Nonrepudiation
- Guarantees that a sender **cannot deny** sending a message
- Achieved through methods like **digital signatures**.

---

### 🔒 Privacy
- Involves proper **handling of personal data**, giving individuals **control and consent** over how their data is used.

---

### 🛡️ Information Assurance
- Measures how **effective security controls** are in protecting information.

---

📘 *Source: CC Certified in Cybersecurity All-in-One Exam Guide by Steven Bennett*

## 🛡️ Common Cybersecurity Threats and Attack Types

---

### 🌐 Fake Websites
- Used to **harvest sensitive information**, such as login credentials or personal data
- Common in phishing campaigns

---

### 💣 Malware
- Any **malicious software** designed to cause harm or unauthorized access.

---

#### 🦠 Virus
- A type of malware typically **embedded in another application**.
- Requires user action to spread.

#### 🐴 Trojan
- A **disguised virus** that appears useful but is actually malicious.

#### 🐛 Worm
- A **self-replicating virus** that spreads across systems without user interaction.

#### 👁️ Rootkit
- Malware that **hides its presence** by altering the operating system.
- Designed to give persistent, undetectable access.

---

### 🧠 Social Engineering
- **Manipulating people** into taking actions or revealing confidential information.
- Example: phishing emails, pretexting, baiting.

---

### 📜 Scripting Attacks
- Manipulating input fields to produce **unintended or harmful results**.
- Common types: **SQL injection, XSS (Cross-site Scripting)**

---

### 🧱 Vulnerability-Specific Attacks
- Attacks that exploit **known software bugs or flaws**.
- Can often be prevented by applying security patches and updates.

---

📘 *Source: CC Certified in Cybersecurity All-in-One Exam Guide by Steven Bennett*

## 💻 Elements of a Cyberattack: A Summary

---

A typical cyberattack involves several key stages carried out by a cybercriminal:

---

### 1. 🕵️ Conduct Research
- The attacker gathers as much **information** as possible about the target.
- This can include:
  - System architecture
  - Publicly available data
  - Employee details (e.g., via social engineering)

---

### 2. 🛠️ Exploit Targets
- Uses tools such as **malware** to take advantage of **vulnerabilities**.
- The goal is to gain **unauthorized access** to systems or data.

---

### 3. 🔥 Do Bad Things
Once inside, the attacker may:

- **Steal data** – Compromises **Confidentiality**  
- **Modify data** – Compromises **Integrity**  
- **Destroy data or disrupt services** – Compromises **Availability**

> 🔺 These actions directly violate the **CIA Triad** of cybersecurity.

---

📘 *Source: CC Certified in Cybersecurity All-in-One Exam Guide by Steven Bennett*

## 🔒 Secure Protocols

- **Definition**: Protocols that **encrypt data** while it is being transmitted across a network.  
- **Purpose**: To protect the **confidentiality** and **integrity** of data in transit, preventing interception or tampering.  

### ✅ Examples of Secure Protocols
- **HTTPS** → Secure web browsing (encrypted HTTP).  
- **SSH** → Secure remote login and command execution.  
- **TLS/SSL** → Provides encryption for various applications (web, email, VoIP).  
- **SFTP/FTPS** → Secure file transfer.  
- **IPSec** → Encrypts and authenticates IP packets.  

---

🔑 **Key Idea**: Using secure protocols ensures that sensitive data (like passwords, payment info, or personal data) remains protected during transmission.

## 🔢 TCP/UDP Port Ranges with Examples

Port numbers are categorized into three main ranges, as defined by **IANA**:

| Range            | Name                  | Description | Common Examples |
|------------------|-----------------------|-------------|-----------------|
| **0 – 1023**     | Well-known ports      | Standard services and protocols. Also called **system ports**. | - **20/21** FTP (File Transfer Protocol)<br>- **22** SSH (Secure Shell)<br>- **23** Telnet<br>- **25** SMTP (Email)<br>- **53** DNS (Domain Name System)<br>- **67/68** DHCP (Dynamic Host Config)<br>- **80** HTTP (Web)<br>- **110** POP3 (Email)<br>- **143** IMAP (Email)<br>- **161** SNMP (Network Management)<br>- **443** HTTPS (Secure Web)<br>- **3389** RDP (Remote Desktop) |
| **1024 – 49151** | Registered ports      | Assigned to vendor-specific or widely used applications. | - **1433** Microsoft SQL Server<br>- **1521** Oracle Database<br>- **2049** NFS (Network File System)<br>- **2082/2083** cPanel admin<br>- **3306** MySQL Database<br>- **3389** (sometimes registered for RDP)<br>- **3690** Subversion (SVN)<br>- **5432** PostgreSQL<br>- **5900** VNC (Virtual Network Computing)<br>- **8080** HTTP Alternative (often web apps) |
| **49152 – 65535**| Dynamic / Private ports | **Ephemeral ports**, used temporarily by client applications for outbound connections. Not registered with IANA. | - A web browser connecting to HTTPS might use a random port like **49160** → server **443**<br>- Skype / Zoom dynamically allocate ports<br>- Online games use these for peer-to-peer connections<br>- BitTorrent clients often bind to dynamic ports |

---

### 🔑 Key Notes:
- **Well-known ports** are fixed and universally recognized.  
- **Registered ports** may vary but are often standardized by vendors.  
- **Dynamic/private ports** are chosen by the OS when a client initiates a connection.  
- Example:  
  - Client (ephemeral port `49160`) → Server (`443` HTTPS).  
  - When session ends, the ephemeral port is released.  

## 🌐 OSI Model: Application & Presentation Layers

### Application Layer (Layer 7)
- **Note**: "Application" here refers to **protocols used by applications**, not the apps themselves.  
- **Function**: Provides services that allow user applications (like browsers or email clients) to communicate over a network.  
- **Common Protocols**:  
  - DNS → Domain Name resolution  
  - FTP / SFTP → File transfers  
  - SNMP → Network management  
  - Telnet & SSH → Remote access  
  - HTTP / HTTPS → Web communication  
  - LDAP → Directory services  
- **Data Unit**: `Data` (same for Layers 5–7)

---
# 🌐 OSI Model – 7 Layers Summary

| Layer | Name            | Main Function                                                                 | Examples of Protocols / Technologies     | Data Unit |
|-------|-----------------|-------------------------------------------------------------------------------|------------------------------------------|-----------|
| 7     | **Application** | Provides services to applications for network communication.                  | HTTP, HTTPS, DNS, FTP, SFTP, LDAP, SNMP  | Data      |
| 6     | **Presentation**| Translates, encrypts, compresses data so it can be properly understood.       | JPEG, PNG, GIF, MP3, TLS/SSL (encryption)| Data      |
| 5     | **Session**     | Establishes, manages, and terminates sessions between applications.           | NetBIOS, RPC, PPTP, SQL session handling | Data      |
| 4     | **Transport**   | Ensures reliable delivery, error checking, flow control, segmentation.        | TCP, UDP, SCTP                            | Segments  |
| 3     | **Network**     | Determines best path, logical addressing, routing of packets.                 | IP, ICMP, IPsec, RIP, OSPF, BGP          | Packets   |
| 2     | **Data Link**   | Provides node-to-node delivery, physical addressing (MAC), error detection.   | Ethernet, PPP, Switches, ARP, Frame Relay| Frames    |
| 1     | **Physical**    | Transmits raw bits over a physical medium (cables, signals, voltages).        | Cables, Hubs, Wi-Fi (radio waves), Fiber | Bits      |

---

### 🔑 Quick Memory Aids
- **Top-down data unit flow**: Data → Segments → Packets → Frames → Bits  
- **Mnemonic (Layer 7 → Layer 1)**: *"All People Seem To Need Data Processing"*  
- **Mnemonic (Layer 1 → Layer 7)**: *"Please Do Not Throw Sausage Pizza Away"*

# 🌐 Network Fundamentals Summary

### Key Points
- **LAN (Local Area Network)** and **WAN (Wide Area Network)** are the main network types.  
- Networks can be **wired** (cables) or **wireless** (Wi-Fi, Bluetooth, NFC).  
- Devices use **MAC addresses** (hardware) and **IP addresses** (logical).  
- **OSI Model** has 7 layers; **TCP/IP Model** has 4 layers.  
- Two versions of IP: **IPv4** and **IPv6**.  

## 🚨 Network Threats and Attacks – Summary

### 🔹 Common Attack Categories
- **Malware** – Viruses, trojans, worms, botnets, ransomware, rootkits.  
- **Scripting Attacks** – Buffer overflows, XSS (cross-site scripting), HTTP response splitting, SQL injection, timing/race conditions.  
- **Social Engineering** – Tricks users into actions that harm security (e.g., phishing, spear phishing).  
- **Password Attacks** – Methods include social engineering, phishing, brute force, dictionary attacks, rainbow tables.  
- **Man-in-the-Middle (MitM)** – Criminals intercept and manipulate communication between two parties.  

### 🔹 Additional Threats
- **Backdoors** – Hidden ways to bypass normal authentication or access.  
- **Exfiltration** – Unauthorized transfer of data out of a system.  
- **Cyber Extortion** – Criminals demand money or data in exchange for not causing harm.  
- **Denial of Service (DoS/DDoS)** – Attacks that disrupt system **availability** by overwhelming resources.  

---

✅ **Key Idea**: Most attacks target the **CIA triad** (Confidentiality, Integrity, Availability).  
- Malware & exfiltration → Confidentiality  
- SQL injection & data modification → Integrity  
- DoS/DDoS → Availability  

## 🔐 Quick Review – Data Lifecycle & Encryption

### 📂 Data Lifecycle
1. **Creation** – Data is generated or collected.  
2. **Storage** – Data is stored securely.  
3. **Usage** – Data is actively used by applications or users.  
4. **Sharing** – Data is transmitted or made available to others.  
5. **Archival** – Data is stored long-term but rarely accessed.  
6. **Destruction** – Data is securely deleted when no longer needed.  

---

### 🔑 Encryption Concepts
- **Encryption** – Converts plaintext ➝ ciphertext (unreadable format).  
- **Decryption** – Converts ciphertext ➝ plaintext (readable format).  

#### Types of Encryption:
- **Symmetric Encryption**  
  - Same key used for **encryption and decryption**.  
  - Faster, but key distribution is challenging.  

- **Asymmetric Encryption**  
  - Uses a **public key** (shareable) and a **private key** (kept secret).  
  - More secure for key exchange, but computationally slower.  

---

✅ **Key Idea**:  
- **Symmetric = One Key** (fast, efficient, but less secure for sharing).  
- **Asymmetric = Two Keys** (secure sharing, slower performance).  

## 🔎 Key Cybersecurity Terms

- **Event**  
  An occurrence of an activity on an information system.  

- **Incident**  
  One or more events that **jeopardize confidentiality, integrity, or availability (CIA)** of an asset.  
  - If it results in unauthorized access, it may be called a **breach, intrusion, or compromise**.  

- **Exploit**  
  An action, program, or tool that takes advantage of a system **vulnerability**.  

- **Threat**  
  An event with the potential to **damage the organization**.  
  - Examples: Cyberattack, social engineering, natural disaster, physical intrusion.  

- **Threat Actors**  
  Individuals or groups that can damage the organization.  
  - Examples: Hackers, cyber criminals, insider threats.  

- **Vulnerability**  
  A weakness that can be exploited by a threat actor.  
  - **Zero-day**: A vulnerability not yet widely known or patched.  

---

✅ **Key Point:**  
- **Threat actor** uses an **exploit** to take advantage of a **vulnerability**, causing an **incident** that impacts CIA.

Hi Thanks


