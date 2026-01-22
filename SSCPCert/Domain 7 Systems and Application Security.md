# SSCP Domain 7 – Systems and Application Security
## Detailed Explanation with Examples (Exam-Oriented)

---

## 7.1 Identify and Analyze Malicious Code and Activity

---

### Malware Types

| Malware Type | Explanation | Example |
|--------------|------------|---------|
| Virus | Attaches to legitimate files and spreads when executed | Infected Word document |
| Worm | Self-propagates over networks without user action | WannaCry |
| Trojan | Disguised as legitimate software | Fake antivirus |
| Ransomware | Encrypts data and demands payment | LockBit |
| Spyware | Secretly collects user information | Keyloggers |
| Rootkit | Hides malicious activity with elevated privileges | Kernel rootkit |
| Scareware | Uses fear to trick users into actions | Fake virus alerts |
| Backdoor | Hidden access method bypassing authentication | Hardcoded admin account |
| Trapdoor | Deliberate backdoor left by developers | Debug account |
| Fileless Malware | Runs in memory without files | PowerShell attacks |
---

### Malware

#### Rootkit
**Explanation:**  
A rootkit hides malicious processes and gives attackers persistent, privileged access.

**Example:**  
An attacker installs a kernel rootkit that hides malicious processes from Task Manager and antivirus.

---

#### Spyware
**Explanation:**  
Spyware secretly monitors user activity and sends data to attackers.

**Example:**  
A keylogger records passwords typed on a banking website.

---

#### Scareware
**Explanation:**  
Uses fake alerts to scare users into installing malware or paying money.

**Example:**  
A popup claims “Your PC is infected!” and asks for payment.

---

#### Ransomware
**Explanation:**  
Encrypts files and demands ransom to restore access.

**Example:**  
WannaCry encrypts hospital systems and demands Bitcoin.

---

#### Trojan
**Explanation:**  
Malware disguised as legitimate software.

**Example:**  
A cracked software installer that installs a backdoor.

---

#### Virus
**Explanation:**  
Requires user action to spread; attaches to files.

**Example:**  
An infected USB spreads malware when opened.

---

#### Worm
**Explanation:**  
Self-propagates across networks without user interaction.

**Example:**  
Conficker spreads automatically via network vulnerabilities.

---

#### Trapdoor
**Explanation:**  
Hidden access left intentionally by developers.

**Example:**  
A hardcoded admin password left for testing.

---

#### Backdoor
**Explanation:**  
Hidden method to bypass authentication.

**Example:**  
Malware opens a secret SSH port.

---

#### Fileless Malware
**Explanation:**  
Runs in memory using legitimate tools (PowerShell).

**Example:**  
Attack executes malicious PowerShell commands from RAM.

---

### Malware Countermeasures

#### Scanners
**Explanation:**  
Detect known malware signatures.

**Example:**  
Scheduled antivirus scans detect trojans.

---

#### Anti-malware
**Explanation:**  
Detects, prevents, and removes malware.

**Example:**  
Windows Defender blocking ransomware behavior.

---

#### Code Signing
**Explanation:**  
Ensures software integrity and authenticity.

**Example:**  
Unsigned software blocked by OS security policy.

---

### Malicious Activity

#### Insider Threat
**Explanation:**  
Authorized user misuses access.

**Example:**  
Employee copies customer data to USB.

---

#### Data Theft
**Explanation:**  
Unauthorized exfiltration of sensitive data.

**Example:**  
Attacker steals credit card database.

---

#### DDoS
**Explanation:**  
Overwhelms systems to make them unavailable.

**Example:**  
Botnet floods website with traffic.

---

#### Botnet
**Explanation:**  
Network of compromised systems.

**Example:**  
IoT devices used for DDoS attack.

---

#### Zero-Day Exploit
**Explanation:**  
Attack exploiting unknown vulnerability.

**Example:**  
Attack occurs before patch exists.

---

#### Web-Based Attacks
**Explanation:**  
Attacks targeting web applications.

**Example:**  
SQL Injection stealing login credentials.

---

#### Advanced Persistent Threat (APT)
**Explanation:**  
Long-term, stealthy, targeted attack.

**Example:**  
Nation-state spying on government networks.

---

### Malicious Activity Countermeasures

#### User Awareness
**Example:**  
Training employees to detect phishing.

#### System Hardening
**Example:**  
Disabling unused services.

#### Patching
**Example:**  
Applying OS security updates.

#### Isolation
**Example:**  
Quarantining infected endpoint.

#### Data Loss Prevention (DLP)
**Example:**  
Blocking email with sensitive data.

---

### Social Engineering

#### Phishing
**Explanation:**  
Fraudulent emails to steal credentials.

**Example:**  
Fake Microsoft password reset email.

---

#### Impersonation
**Explanation:**  
Pretending to be a trusted entity.

**Example:**  
Attacker claims to be IT support.

---

### Behavior Analytics

#### Machine Learning
**Example:**  
Detecting unusual login times.

#### Artificial Intelligence
**Example:**  
AI flags abnormal network behavior.

#### Data Analytics
**Example:**  
Correlating logs to detect attacks.

---

## 7.2 Endpoint Device Security

---

### Host-based Intrusion Prevention System (HIPS)
**Explanation:**  
Blocks malicious behavior in real time.

**Example:**  
Stops unauthorized registry changes.

---

### Host-based Firewall
**Explanation:**  
Filters traffic at endpoint.

**Example:**  
Blocks inbound RDP connections.

---

### Application Whitelisting
**Explanation:**  
Only approved apps can run.

**Example:**  
Blocks unknown executable files.

---

### Endpoint Encryption
**Explanation:**  
Encrypts data on device.

**Example:**  
BitLocker encrypts laptop hard drive.

---

### Trusted Platform Module (TPM)
**Explanation:**  
Hardware security chip.

**Example:**  
Stores encryption keys securely.

---

### Secure Browsing
**Explanation:**  
Protects against malicious websites.

**Example:**  
Browser blocks phishing site.

---

### Endpoint Detection and Response (EDR)
**Explanation:**  
Detects, investigates, and responds.

**Example:**  
EDR isolates infected laptop.

---

## 7.3 Mobile Device Management (MDM)

---

### Corporate-Owned
**Example:**  
Company-issued iPhone with policies.

---

### COPE
**Explanation:**  
Work + personal use.

**Example:**  
Employee installs personal apps on work phone.

---

### BYOD
**Explanation:**  
Employee-owned device.

**Example:**  
Personal phone accessing work email.

---

### Containerization
**Explanation:**  
Separates work and personal data.

**Example:**  
Work email stored in encrypted container.

---

### Encryption
**Example:**  
Encrypts phone storage.

---

### Mobile Application Management (MAM)
**Explanation:**  
Controls corporate apps only.

**Example:**  
Restricts copy-paste from work apps.

---

## 7.4 Cloud Security

---

### Public Cloud
**Example:**  
AWS shared infrastructure.

---

### Private Cloud
**Example:**  
Company-owned data center cloud.

---

### Hybrid Cloud
**Example:**  
Sensitive data on private, apps on public cloud.

---

### Community Cloud
**Example:**  
Government agencies sharing cloud.

---

### IaaS
**Example:**  
AWS EC2 – customer manages OS.

---

### PaaS
**Example:**  
Google App Engine – no OS management.

---

### SaaS
**Example:**  
Microsoft 365 – provider manages everything.

---

### Hypervisor
**Explanation:**  
Manages virtual machines.

**Example:**  
VMware ESXi.

---

### Legal and Regulatory Concerns

- Privacy laws
- Data ownership
- Jurisdiction

**Example:**  
Data stored outside country violates law.

---

### Data Storage, Processing, Transmission
**Example:**  
Encrypted backups with disaster recovery.

---

### Third-Party Requirements
**Example:**  
SLA guarantees uptime and data deletion.

---

### Shared Responsibility Model
**Example:**  
AWS secures infrastructure, customer secures data.

---

## 7.5 Secure Virtual Environments

---

### Virtual Appliances
**Example:**  
Preconfigured firewall VM.

---

### Containers
**Example:**  
Docker container running web app.

---

### Continuity and Resilience
**Example:**  
Failover VM in another region.

---

### Attacks and Countermeasures
**Example:**  
VM escape prevented by patching.

---

### Shared Storage
**Example:**  
SAN used by multiple VMs.

---

## FINAL EXAM TIP
If you can **explain each topic with a simple real-life example**, you will **pass SSCP Domain 7 confidently**.
