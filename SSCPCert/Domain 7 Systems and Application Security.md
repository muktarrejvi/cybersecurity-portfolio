# Domain 7: Systems and Application Security (15%)

**Domain Weight**: 15%  
**Key Focus**: Identify/analyze malicious code & activity, secure endpoints & mobile devices, manage cloud/virtual environments, and apply countermeasures to protect systems and applications.

This domain emphasizes practical defenses against common threats (malware, social engineering, cloud misconfigurations) and secure operations in modern environments (endpoints, mobile, cloud, virtualization).

## 7.1 Identify and analyze malicious code and activity

### Malware Types
- **Rootkits** — Hide presence/processes (kernel/user-mode)  
- **Spyware** — Steals data (keystrokes, screenshots)  
- **Scareware** — Fake alerts to trick purchases  
- **Ransomware** — Encrypts files, demands payment  
- **Trojans** — Disguised as legitimate software  
- **Viruses** — Self-replicating, attaches to files  
- **Worms** — Self-propagating over networks  
- **Trapdoors / Backdoors** — Unauthorized access paths  
- **Fileless malware** — Lives in memory (PowerShell, WMI)  
- **App/code/OS/mobile code vulnerabilities** — Exploit flaws in software  

**Example**: Emotet trojan spreads via phishing → installs ransomware → encrypts files and exfiltrates data.

### Malware Countermeasures
- Scanners / anti-malware (signature + heuristic + behavioral)  
- Code signing (verify authenticity)  
- Containment/remediation (quarantine, rollback)  
- Software security (secure development, patching)  

**Example**: Endpoint anti-malware detects WannaCry exploit → quarantines file → prevents spread via SMB.

### Malicious Activity Types
- Insider threat (malicious or negligent)  
- Data theft / exfiltration  
- DDoS (flooding targets)  
- Botnet (zombie devices for attacks)  
- Zero-day exploits  
- Web-based attacks (XSS, SQLi, CSRF)  
- APT (advanced persistent threat – stealthy, targeted)  

**Example**: APT group uses spear-phishing + zero-day to gain foothold → lateral movement → data exfiltration over months.

### Malicious Activity Countermeasures
- User awareness/training  
- System hardening (disable unnecessary services, least privilege)  
- Patching/vulnerability management  
- Isolation (segmentation, sandboxing)  
- DLP (prevent unauthorized data movement)  

**Example**: After insider data theft, implement DLP rules to block USB copies of sensitive files + mandatory security awareness training.

### Social Engineering
- Phishing/smishing/vishing  
- Impersonation  
- Scarcity/urgency tactics  
- Whaling (targeting executives)  

**Example**: CEO receives email pretending to be CFO requesting urgent wire transfer → falls for impersonation → financial loss.

### Behavior Analytics
- Machine learning / AI for anomaly detection  
- UEBA (User and Entity Behavior Analytics)  

**Example**: UEBA flags employee downloading 10 GB at 3 AM from unusual location → triggers alert for potential insider exfiltration.

## 7.2 Implement and operate endpoint device security

- **HIPS / HIDS** — Host-based prevention/detection (blocks/monitors suspicious activity)  
- **Host-based firewalls** — Control inbound/outbound traffic per host  
- **Application whitelisting** — Only allow approved apps to run  
- **Endpoint encryption** — Full disk encryption (BitLocker, FileVault)  
- **TPM** — Hardware root of trust (secure boot, key storage)  
- **Secure browsing** — Validate certificates, block malicious sites  
- **EDR** — Endpoint Detection and Response (advanced hunting, behavioral blocking)  

**Example**: Company deploys EDR → detects living-off-the-land attack using legitimate tools (PsExec) → isolates endpoint automatically.

## 7.3 Administer and manage mobile devices

- **Provisioning** — COPE (corporate-owned), BYOD (personal), MDM enrollment  
- **Containerization** — Separate work/personal data (e.g., Samsung Knox, Microsoft Intune MAM)  
- **Encryption** — Device + app-level  
- **MAM** — Manage apps without full device control (wipe corporate apps only)  

**Example**: BYOD policy uses MDM + containerization → employee installs work email app in secure container → personal data remains untouched if device is wiped for security reasons.

## 7.4 Understand and configure cloud security

- **Deployment models** — Public, private, hybrid, community  
- **Service models** — IaaS (you manage OS/apps), PaaS (platform managed), SaaS (fully managed)  
- **Virtualization** — Hypervisor, VPC  
- **Legal/regulatory** — Privacy (GDPR), jurisdiction, eDiscovery, shadow IT  
- **Data handling** — Storage, processing, transmission, backup/recovery/resilience  
- **Third-party** — SLA, data portability, destruction, auditing  
- **Shared responsibility model** — Provider vs. customer duties (e.g., AWS secures hardware, you secure data/configs)  

**Example**: In IaaS (AWS EC2), customer responsible for OS patching + IAM policies; AWS handles physical security + hypervisor.

## 7.5 Operate and maintain secure virtual environments

- **Hypervisor types** — Type 1 (bare-metal, e.g., ESXi), Type 2 (hosted, e.g., VirtualBox)  
- **Virtual appliances** — Pre-configured VMs (e.g., firewall appliance)  
- **Containers** — Lightweight (Docker, Kubernetes) vs. VMs  
- **Continuity/resilience** — Snapshots, replication, HA clusters  
- **Storage** — Shared storage risks (e.g., data domain deduplication)  
- **Threats & countermeasures** — VM escape, brute-force, threat hunting  

**Example**: Attacker exploits hypervisor vulnerability for VM escape → countermeasures: patch hypervisor, isolate VMs with micro-segmentation, monitor for anomalous VM behavior.

## Quick Reference Table – Key Concepts & Tools

| Concept/Tool          | Purpose                                      | Example / SSCP Tip                     |
|-----------------------|----------------------------------------------|----------------------------------------|
| EDR vs Anti-malware   | Behavioral detection + response              | EDR for advanced threats (fileless)    |
| Shared Responsibility | Cloud security duties                        | Memorize: Provider = physical, you = data/config |
| Container vs VM       | Isolation level                              | Containers share kernel → higher escape risk |
| TPM                   | Hardware trust anchor                        | Enables secure boot & credential guard |
| DLP                   | Prevents data leaks                          | Blocks PII upload to personal cloud    |
| Zero-day              | Unknown vulnerability exploit                | Mitigate with behavior-based tools     |

**Study Tips for Domain 7**  
- Know malware types + indicators (exam loves examples like fileless, ransomware)  
- Memorize shared responsibility differences (IaaS vs PaaS vs SaaS)  
- Understand endpoint tools stack: HIPS → EDR → whitelisting → encryption  
- Mobile: BYOD vs COPE + containerization/MDM/MAM distinctions  
- Virtualization threats: focus on escape, hypervisor attacks  

Cross-reference: NIST SP 800-83 (malware), NIST SP 800-125 (virtualization), Cloud Security Alliance CCM, (ISC)² SSCP Study Guide.

A DNS sinkhole (also called blackhole DNS) is the best and most scalable option here.
Jennifer (as AD domain admin) can configure the organization's internal DNS servers (Active Directory-integrated DNS) or use a forwarding DNS setup to intercept queries for the known botnet C2 domain names and return a false/non-routable IP (e.g., 127.0.0.1, 0.0.0.0, or a local sinkhole server IP).

Last updated: February 2026
