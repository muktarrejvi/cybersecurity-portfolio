# Domain 7: Systems and Application Security (SSCP)

---

## 7.1 Identify and Analyze Malicious Code and Activity

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

### Malware Countermeasures

- Anti-malware software
- Malware scanners
- Code signing
- Regular updates and patches
- Least privilege access

**Example:**  
Digitally signed software ensures code integrity and authenticity.

---

### Malicious Activities

| Activity | Description |
|--------|-------------|
| Insider Threat | Abuse by authorized users |
| Data Theft | Unauthorized data exfiltration |
| DDoS | Overwhelming systems with traffic |
| Botnet | Network of compromised devices |
| Zero-Day | Exploits unknown vulnerabilities |
| Web Attacks | SQL injection, XSS |
| APT | Long-term targeted attacks |

---

### Malicious Activity Countermeasures

- User awareness training
- System hardening
- Patch management
- Network isolation
- Data Loss Prevention (DLP)

---

### Social Engineering

- Phishing
- Impersonation
- Pretexting

**Example:**  
Fake email pretending to be IT asking for password reset.

---

### Behavior Analytics

- Machine Learning (ML)
- Artificial Intelligence (AI)
- Data Analytics

**Purpose:**  
Detect anomalies in user or system behavior.

---

## 7.2 Implement and Operate Endpoint Device Security

### Endpoint Security Controls

| Control | Description |
|------|-------------|
| HIPS | Prevents malicious activity on host |
| Host Firewall | Filters traffic at host level |
| Application Whitelisting | Only approved apps can run |
| Endpoint Encryption | Protects data at rest |
| TPM | Hardware-based security chip |
| Secure Browsing | Protects against malicious websites |
| EDR | Detects and responds to endpoint threats |

**Example:**  
EDR detects suspicious PowerShell behavior and isolates device.

---

## 7.3 Administer Mobile Device Management (MDM)

### Provisioning Techniques

| Model | Description |
|------|-------------|
| Corporate Owned | Organization owns device |
| COPE | Corporate Owned, Personally Enabled |
| BYOD | User-owned device |

---

### MDM Security Features

- Containerization (separate work/personal data)
- Encryption
- Mobile Application Management (MAM)
- Remote wipe
- Policy enforcement

**Example:**  
Work email stored in encrypted container on personal phone.

---

## 7.4 Understand and Configure Cloud Security

### Cloud Deployment Models

| Model | Description |
|------|-------------|
| Public | Shared infrastructure |
| Private | Dedicated infrastructure |
| Hybrid | Public + Private |
| Community | Shared by similar organizations |

---

### Cloud Service Models

| Model | Responsibility |
|------|---------------|
| IaaS | Customer manages OS & apps |
| PaaS | Provider manages OS |
| SaaS | Provider manages everything |

---

### Virtualization

- Hypervisors manage virtual machines
- Type 1 (bare metal)
- Type 2 (hosted)

---

### Legal and Regulatory Concerns

- Data privacy
- Surveillance laws
- Data ownership
- Jurisdiction
- eDiscovery

---

### Data Storage, Processing, and Transmission

- Archiving
- Backup and recovery
- Resilience
- Encryption in transit and at rest

---

### Third-Party / Outsourcing Requirements

- Service Level Agreements (SLA)
- Data portability
- Secure data destruction
- Auditing rights

---

### Shared Responsibility Model

- Cloud provider secures infrastructure
- Customer secures data and access

---

## 7.5 Operate and Maintain Secure Virtual Environments

### Virtualization Components

| Component | Description |
|--------|-------------|
| Hypervisor | Manages virtual machines |
| Virtual Appliances | Preconfigured VM images |
| Containers | Lightweight app isolation |

---

### Security Considerations

- VM escape attacks
- Hypervisor hardening
- Patch management
- Network segmentation

---

### Continuity and Resilience

- High availability
- Failover
- Snapshots
- Backups

---

### Shared Storage

- SAN
- NAS
- Risks: data leakage, misconfiguration

---

## Key Exam Tips

- **Malware vs Attack** → Malware is code, attack is activity  
- **EDR > Antivirus** (detect + respond)  
- **SaaS = least customer responsibility**  
- **Shared responsibility model is critical**

---

## Reference
Chapple, Mike, and David Seidl.  
*ISC2 SSCP Systems Security Certified Practitioner Official Practice Tests*, Wiley, 2021.
