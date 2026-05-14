# Chapter 7: Security Operations (Domain 7)

**Domain Weight**: 13% of the CISSP Exam (2024/2025 outline)

**Purpose of this Domain**:  
This is one of the **largest and most practical** domains. It focuses on the **day-to-day execution** of security — running, maintaining, and improving security operations. It covers how to keep the organization secure during normal operations and especially during incidents, disasters, and changes.

---

## 7.1 Understand and Comply with Investigations

### Types of Investigations
- **Administrative Investigations** — Internal policy violations, HR-related.
- **Criminal Investigations** — Law enforcement involvement, chain of custody critical.
- **Civil Investigations** — Lawsuits, regulatory matters.
- **Forensic Investigations** — Technical deep dive (evidence collection & preservation).

### Key Concepts
- **Chain of Custody** — Documenting who handled evidence, when, and how (must be unbroken).
- **Order of Volatility** — Collect most volatile evidence first (RAM → Disk → Logs → Backups).
- **Legal Hold** — Preserving data when litigation is anticipated.
- **E-Discovery** — Finding and producing electronic evidence for court.

**Exam Tip**: Know the difference between **criminal** (beyond reasonable doubt) vs **civil** (preponderance of evidence) standards.

---

## 7.2 Conduct Logging and Monitoring Activities

### Logging Categories
- **Security Logs** — Authentication, authorization, privilege use.
- **System Logs** — OS events, errors, startups.
- **Application Logs** — App-specific events, transactions.
- **Network Logs** — Firewall, IDS/IPS, NetFlow, packet captures.

### Monitoring Types
- **Continuous Monitoring**
- **Anomaly-based Monitoring**
- **Signature-based Monitoring**
- **Behavioral Monitoring**

### SIEM (Security Information and Event Management)
- Central collection, correlation, alerting, and reporting.
- Key functions: Aggregation, Normalization, Correlation, Alerting.

**Best Practices**: Log retention policies, log protection (integrity), centralized logging.

---

## 7.3 Perform Configuration Management (CM)

### Core Activities
- **Provisioning** — Deploying new systems securely.
- **Baselining** — Creating and maintaining secure configuration standards (Gold Images).
- **Automation** — Using tools like Ansible, Puppet, Chef, Terraform for consistency.

### Key Concepts
- **Configuration Items (CIs)**
- **CM Database (CMDB)**
- **Version Control**
- **Immutable Infrastructure** (e.g., containers, IaC)

**Exam Tip**: Strong CM reduces misconfigurations — one of the biggest causes of breaches.

---

## 7.4 Apply Foundational Security Operations Concepts

### Core Principles
- **Need-to-Know** — Access only to information required for job.
- **Least Privilege** — Minimum permissions necessary.
- **Separation of Duties (SoD)** — Prevent single person from completing critical task alone.
- **Two-Person Control / Dual Control**
- **Job Rotation**
- **Mandatory Vacations**

### Other Concepts
- **Privileged Account Management (PAM)**
- **Zero Trust Principles** in operations.

---

## 7.5 Apply Resource Protection

### Types of Resources to Protect
- **Hardware Assets** — Servers, laptops, mobile devices.
- **Media Protection**:
  - **Sensitive Media** (tapes, USBs, hard drives).
  - **Sanitization Methods**: Clearing, Purging, Destroying.
- **Data Remanence** — Residual data left after deletion.
- **Asset Inventory & Tracking**

**Sanitization Techniques**:
- **Clearing** — Overwriting once (software).
- **Purging** — Stronger sanitization (degaussing, multiple overwrites).
- **Destruction** — Shredding, incineration, pulverizing.

---

## 7.6 Conduct Incident Management

### Incident Response Lifecycle (NIST SP 800-61)
1. **Preparation**
2. **Detection & Analysis**
3. **Containment** (short-term & long-term)
4. **Eradication**
5. **Recovery**
6. **Lessons Learned / Post-Incident Activity**

### Key Concepts
- **Incident vs Event**
- **Playbooks & Runbooks**
- **Communication Plan** (internal + external)
- **Root Cause Analysis (RCA)**

**Exam Tip**: Know all 6 phases deeply and in order.

---

## 7.7 Operate and Maintain Detection and Preventative Measures

### Detection Technologies
- **IDS/IPS** (Host-based & Network-based)
- **SIEM**
- **UEBA** (User and Entity Behavior Analytics)
- **DLP** (Data Loss Prevention)
- **EDR / XDR**

### Preventative Measures
- **Firewalls** (NGFW)
- **Anti-malware / Endpoint Protection**
- **Email Security** (Anti-phishing, DMARC)
- **Web Application Firewalls (WAF)**
- **Sandboxing**

---

## 7.8 Implement and Support Patch and Vulnerability Management

### Key Processes
- **Patch Management Lifecycle**:
  - Discovery → Assessment → Testing → Approval → Deployment → Verification.
- **Vulnerability Management**:
  - Scanning → Prioritization (risk-based) → Remediation → Validation.

### Concepts
- **Zero-Day Vulnerabilities**
- **Compensating Controls** when patching is not immediate.
- **Patch Testing** (very important in production environments).

---

## 7.9 Understand and Participate in Change Management Processes

### Change Management Phases
1. Request
2. Review & Approval
3. Testing
4. Implementation
5. Monitoring & Review
6. Closure

### Types of Changes
- **Standard Changes** (pre-approved, low risk)
- **Normal Changes**
- **Emergency Changes**

**CAB** (Change Advisory Board) — Reviews and approves changes.

**Exam Tip**: Poor change management = major source of outages and security incidents.

---

## 7.10 Implement Recovery Strategies

### Recovery Objectives
- **RTO** — Recovery Time Objective (how quickly to recover).
- **RPO** — Recovery Point Objective (how much data loss is acceptable).
- **MTTR** — Mean Time To Repair.
- **MTBF** — Mean Time Between Failures.

### Recovery Strategies
- **Redundant Sites**:
  - **Hot Site** — Fully operational, immediate failover.
  - **Warm Site** — Equipped but needs configuration.
  - **Cold Site** — Basic facility only.
- **Backup Strategies** (Full, Differential, Incremental).
- **High Availability (HA)**, Clustering, Load Balancing.

---

## 7.11 Implement Disaster Recovery (DR) Processes

- DR Plan development and integration with BCP.
- Failover & Failback procedures.
- Data replication (synchronous vs asynchronous).

---

## 7.12 Test Disaster Recovery Plan (DRP)

### Testing Types
- **Tabletop / Walkthrough** — Discussion-based.
- **Simulation** — Role-playing a scenario.
- **Parallel Test** — Running DR systems alongside primary.
- **Full Interruption / Cutover Test** — Complete switch to DR site (highest risk).

---

## 7.13 Participate in Business Continuity (BC) Planning and Exercises

- **Business Impact Analysis (BIA)** — Identifies critical processes and MTD (Maximum Tolerable Downtime).
- **Continuity of Operations Plan (COOP)**
- Exercises and drills for BC.

---

## 7.14 Implement and Manage Physical Security

### Physical Security Controls
- **Perimeter Security** (fences, gates, guards, lighting).
- **Building Security** (mantraps, access cards, biometrics).
- **Internal Controls** (motion sensors, CCTV, secure cabinets).
- **Environmental Controls** (HVAC, fire suppression, UPS, generators).

**Defense in Depth** in physical layer.

---

## 7.15 Address Personnel Safety and Security Concerns

- **Duress Alarms**
- **Evacuation Procedures**
- **Travel Security**
- **Insider Threat Mitigation**
- **Emergency Management** (active shooter, natural disasters, medical).


**Study Recommendations**:
- Memorize NIST Incident Response phases.
- Understand differences between DRP, BCP, and COOP.
- Know practical operations (patch, change, config management).
