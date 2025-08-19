## 🔐 Security Fundamentals – Key Concepts

---

### 🔺 CIA Triad
Security is built around three core principles:

- **Confidentiality** – Protecting the secrecy of information.
- **Integrity** – Ensuring data is accurate, complete, and unaltered.
- **Availability** – Ensuring information is accessible when needed.

---

### 🔐 Authentication
Verifies **who** someone is using one or more factors:

- **Type 1:** Something you know (e.g., password)
- **Type 2:** Something you have (e.g., smart card)
- **Type 3:** Something you are (e.g., fingerprint)

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
- Used to **harvest sensitive information**, such as login credentials or personal data.
- Common in phishing campaigns.

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

## 🔢 TCP/UDP Port Ranges

Port numbers are categorized into three main ranges, as defined by **IANA**:

| Range            | Name                  | Description | Examples |
|------------------|-----------------------|-------------|----------|
| **0 – 1023**     | Well-known ports      | Used by standard protocols that are part of the TCP/IP suite. Commonly referred to as **system ports**. | HTTP (80), HTTPS (443), DNS (53), SMTP (25) |
| **1024 – 49151** | Registered ports      | Ports registered with IANA for specific applications or vendor software. | Microsoft SQL Server (1433), Oracle DB (1521) |
| **49152 – 65535**| Dynamic / Private ports | Also called **ephemeral ports**. Assigned temporarily by applications for client connections. Not controlled by IANA. | Used by web browsers, custom apps, etc. |

---

### 🔑 Key Notes:
- **Secure vs. Nonsecure Ports**  
  - HTTPS (443) = Secure  
  - HTTP (80) = Nonsecure  
- While common services use standard ports, **any service can technically run on any port**.  
- **Ephemeral ports** are created for a short period (e.g., when your browser connects to a website, it uses one).  




Thanks

