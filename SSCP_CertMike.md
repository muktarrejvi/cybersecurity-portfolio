### Chapter 1
## 🛡️ Professional Responsibility

### 🔒 Privacy Compliance
- **PII & PHI**  
  - *Personally Identifiable Information (PII)*: Data linked to an individual.  
  - *Protected Health Information (PHI)*: Healthcare records (regulated under HIPAA).  

- **Generally Accepted Privacy Principles (GAPP)**  
  1. **Management** – Policies and governance for privacy protection.
  2. **Notice** – Inform individuals about data collection and privacy practices.  
  3. **Choice & Consent** – Collect, store, use, and share data only with consent.  
  4. **Collection** – Gather data only for disclosed purposes.  
  5. **Use, Retention & Disposal** – Use only for intended purposes and securely dispose when no longer needed.  
  6. **Access** – Allow individuals to review/update their data.  .
  7. **Disclosure to Third Parties** – Share only with consent and for disclosed purposes.  
  8. **Security** – Protect data from unauthorized access.  
  9. **Quality** – Ensure accuracy, completeness, and relevance.  
  10. **Monitoring & Enforcement** – Monitor compliance and provide dispute resolution. 

- **ISO/IEC 27018**  
  - A code of practice for protecting PII in public cloud environments.  

---

### 👩‍💻 Employee Privacy
- **Minimization Principle** – Collect only necessary information; retain only as long as needed.  
- **Access Limitation** – Restrict access to sensitive data; minimize the number of employees with access.  
- **Encryption & Masking** – Protect sensitive employee data from exposure or unauthorized access.  

---

### ⚖️ Ethics
- **Codes of Professional Ethics**  
  - Information security professionals must follow ethics codes from (ISC)² and other industry organizations.  

- **(ISC)² Code of Ethics**  
  - **Preamble** – Uphold high ethical standards for the safety and welfare of society.  
  - **Four Mandatory Canons**:  
    1. Protect society, the common good, public trust, and infrastructure.  
    2. Act honorably, honestly, justly, responsibly, and legally.  
    3. Provide diligent and competent service to principals.  
    4. Advance and protect the profession.  

- **Consequences of Violations**  
  - Breaches can result in revocation of certification.  
  - Members must report any violations they become aware of.  

---

✅ These principles — Privacy Compliance, Employee Privacy, and Ethics — form the foundation of **trust, professionalism, and accountability** in cybersecurity practice.  
## 🖥️ Physical Asset Management

### Key Points
- **Responsibility** – Cybersecurity teams often oversee the **physical security of technology resources**, as loss/theft can lead to major financial and data breaches.  
- **Inventory Process** – A strong physical security program begins with accurate **hardware inventory**.  
  - Track hardware from ordering → receiving → deployment → reassignment → decommissioning.  
  - Include details like **serial numbers** and **custody changes**.  
- **Integration** – Inventory should be tied to **provisioning and decommissioning processes**.  
- **Asset Management Systems** – Commonly used to track devices; may be standalone or part of **IT service management platforms**.  
- **Automation** – Some systems correlate inventory records with devices active on the network, flagging inconsistencies.  
- **Media Management** – Sensitive data storage media (e.g., disks, tapes) should be tracked and protected, even if not all media can realistically be managed.  

---

✅ Maintaining an accurate, up-to-date asset inventory reduces the risk of **loss, theft, or misuse** of organizational resources.  

## 📜 Software Licensing

### Importance
- Software is valuable **intellectual property**.  
- Protected by **license agreements** that define how it can be used.  

---

### 🔑 License Agreement Types
1. **Enterprise License Agreements (ELAs)**  
   - Negotiated contracts between vendor and customer.  
   - Common for expensive enterprise software.  

2. **End User License Agreements (EULAs)**  
   - Standard agreements shown during software installation/setup.  
   - Users must accept terms before using the software.  

---

### ⏳ License Duration
- **Perpetual License** – One-time fee; use indefinitely (updates/support may cost extra).  
- **Subscription License** – Recurring fee (monthly/annual); usually includes updates & support.  

---

### 👥 User Models
- **Concurrent Use License** – Limits the number of simultaneous users.  
- **Named User License** – Tied to specific individuals (via username/login).  

---

### 🌍 Distribution Models
- **Closed Source (Proprietary)** – Licensed for a fee.  
- **Freeware** – Free to use, sometimes with restrictions or reduced features.  
- **Open Source** – Free to use, modify, and distribute (e.g., GPL, MIT License).  
- **Cloud Service Licenses (SaaS)** – Agreements for online platforms (e.g., terms & conditions links).  

---

✅ Understanding licensing models ensures **legal compliance**, controls **software costs**, and supports **security governance**.  


## 🔄 Change and Configuration Management

### 📌 Change Management
- **Purpose**: Ensure IT changes support business objectives without disrupting operations.  
- **Process**: Standardized workflow for requesting, reviewing, approving, and implementing changes.  
- **Request for Change (RFC)** includes:  
  - Description of change  
  - Expected impact  
  - Risk assessment  
  - Rollback plan  
  - People involved  
  - Schedule  
  - Affected configuration items  
- **Approval**:  
  - Minor changes – approved by manager.  
  - Major changes – reviewed by **Change Advisory Board (CAB)**.  
  - Routine/pre-approved changes – automatically approved once RFC is submitted.  
- **Communication**: Notify stakeholders (users, customers, technical staff) at the right time.  
- **Audit Preparedness**: Provides paper trail for demonstrating compliance to auditors.  

---

### ⚙️ Configuration Management
- **Purpose**: Track and control how systems are set up.  
- **Scope**:  
  - Operating system settings  
  - Installed software inventory  
- **Lifecycle**: From provisioning → ongoing updates → disposal.  
- **Baselining**:  
  - Capture a snapshot of a system at a specific point in time.  
  - Compare against baseline to detect unauthorized or unintended changes.  

---

✅ Together, **Change Management** minimizes disruption from IT changes, while **Configuration Management** ensures systems remain secure and consistent throughout their lifecycle.  

## 🔐 Understanding Data Security

### Importance
- Data is often an organization’s **most valuable asset**.  
- Security professionals focus on ensuring **Confidentiality, Integrity, and Availability (CIA)**.  

---

### 📊 Data States & Risks
1. **Data at Rest**  
   - Stored on hard drives, USBs, cloud services, or backups.  
   - Risks: Physical theft, unauthorized logical access.  
   - Protection: File/device encryption, strong access controls.  

2. **Data in Transit**  
   - Moving across networks (e.g., credit card entered on a website).  
   - Risks: Eavesdropping, interception.  
   - Protection: TLS/SSL encryption, secure VPNs.  

3. **Data in Use**  
   - Actively processed in system memory.  
   - Risks: Memory scraping, unauthorized process access.  
   - Protection: Process isolation, memory protection techniques.  

---

### 🛡️ Protection Measures
- **Policies & Procedures** – Define proper use of sensitive data and required controls.  
- **Encryption** –  
  - File/disk encryption for data at rest.  
  - TLS for data in transit.  
- **Access Controls** – File system ACLs to define who can view, modify, or delete data.  

---

### 📈 Big Data Considerations
- Big data = very large datasets unsuitable for traditional relational databases.  
- Uses **NoSQL technologies** (e.g., key-value stores).  
- Security concerns:  
  - Protecting **personally identifiable information (PII)**.  
  - Ensuring proper access controls.  
  - Securing distributed storage and analysis platforms.  

---

✅ A strong **data security strategy** protects sensitive information across all states, while adapting controls to new challenges like **big data environments**.  
## 📝 Data Security Policies

### Role of Policies
- Provide **foundational authority** for security efforts and compliance.  
- Set **clear expectations** for data protection and control usage.  
- Guide **data access processes** for business needs.  
- Define **exception procedures** for unique business requirements.  

---

### 🔑 Key Policy Areas

1. **Data Classification Policies**  
   - Define **sensitivity & criticality levels** of data.  
   - Basis for handling requirements and protection measures.  

2. **Data Storage Policies**  
   - Approved storage locations by classification level.  
   - Access control requirements & enforcement mechanisms.  
   - Encryption requirements (e.g., encryption mandatory for cloud storage or laptops, optional for in-house servers).  

3. **Data Transmission Policies**  
   - Rules for transmitting data across different networks.  
   - Mandatory encryption for sensitive information in transit.  
   - Restrictions on sending sensitive data outside corporate networks.  

4. **Data Lifecycle Policies**  
   - **Retention Policies**  
     - Define minimum retention (e.g., 7 years for tax records).  
     - Define maximum retention (e.g., retain card data only until transaction completion).  
   - **Disposal Policies**  
     - Secure wiping of storage media before recycling/disposal.  
     - Techniques include:  
       - Software tools (e.g., DBAN).  
       - Hardware methods (magnetic degaussers, shredders).  
     - Addresses **data remnants** risk (deleted files may still be recoverable).  

---

### ✅ Takeaway
Strong **data security policies**:  
- Ensure consistent data protection.  
- Reduce risk exposure.  
- Provide a solid foundation for regulatory compliance and organizational security.  

## 👥 Data Security Roles

### 📌 Data Governance Model (Four-Tier Structure)
1. **Data Owner (a.k.a. Data Controller under GDPR)**  
   - Senior-level official with overall responsibility for a dataset.  
   - Defines policies and guidelines for data use/security.  
   - Makes final decisions on data handling.  
   - Example: VP of HR = Data Owner for employee data.  

2. **Data Steward**  
   - Implements the policies set by the Data Owner.  
   - Handles day-to-day governance (e.g., who can access data).  
   - Reports to the Data Owner.  
   - Example: Director of HR Information Services.  

3. **Data Custodian**  
   - IT staff/system administrators who manage data storage and processing.  
   - Ensure backups, encryption, access controls, compliance.  
   - Rarely make policy decisions but enforce protections.  

4. **Data User**  
   - Employees (analysts, managers, service staff) who interact with data daily.  
   - Must comply with rules set by owners/stewards.  
   - Responsible for avoiding unauthorized disclosure.  

---

### 🌍 External Roles
- **Data Subjects**  
  - The individuals described in collected data (e.g., employees, customers).  
  - Not part of governance structure but hold privacy rights.  

- **Data Processors**  
  - Third parties handling data on behalf of the organization.  
  - Perform tasks like data entry, analysis, transmission, or destruction.  
  - Must follow policies/security requirements set by Data Owner/Controller.  

---

### ⚠️ Key Distinction
- **System Owner ≠ Data Owner**  
  - Owning IT infrastructure does not mean owning the data stored/processed within it.  
  - Important for internal governance and inter-organizational data sharing.  

---

✅ Strong data governance requires coordination between **owners, stewards, custodians, and users**, while respecting the rights of **data subjects** and enforcing policies with **processors**.  
## 🛡️ Security Control Selection & Implementation – Key Takeaways
- **Purpose of Controls** – Reduce likelihood, minimize impact, or detect security issues.  
- **Types by Purpose**:  
  - Preventive – Stop issues (e.g., firewalls).  
  - Detective – Identify issues (e.g., IDS, alarms).  
  - Corrective – Fix issues (e.g., backups).  
  - Deterrent – Discourage attacks (e.g., warning signs, guard dogs).  
- **Types by Mechanism**:  
  - Technical – Firewalls, anti-malware, DLP, session timeouts.  
  - Administrative – Policies, access reviews, training, audits.  
  - Physical – Locks, cameras, mantraps.  
- **Defense in Depth** – Layer multiple controls for the same objective.  
- **Control Failures**:  
  - False Positive – Alert without a real issue → reduces trust.  
  - False Negative – Missed detection → creates false sense of safety.  


# 🛡️ Control & Risk Frameworks – Detailed Summary

Security control and risk frameworks help organizations design, implement, and manage comprehensive security programs without starting from scratch. They ensure **coverage of risks** and **alignment with business goals**.

---

## 🔑 Major Frameworks

### **COBIT (Control Objectives for Information and Related Technology)**
- Published by ISACA.
- Strong **audit focus** – widely used by auditors.
- Links **business goals ↔ IT/security functions**.
- Governance principles: stakeholder value, holistic approach, dynamic governance, separation of governance & management, tailoring to enterprise, end-to-end coverage.

---

### **ISO Standards**
- **ISO 27001**: Information Security Management Systems (ISMS) – control objectives.  
- **ISO 27002**: Detailed list of security controls (how to achieve 27001 objectives).  
- **ISO 27701**: Privacy management (extension to 27001, privacy controls).  
- **ISO 31000**: Risk management guidance – enterprise risk framework.  
- **Use case**: Common worldwide; often required for compliance and certification.

---

### **NIST Publications**
- **SP 800-53**: *Security and Privacy Controls for Information Systems*.  
  - Mandatory for US federal agencies.  
  - ~500 pages of detailed control catalogs.  
- **Cybersecurity Framework (CSF)**:  
  - 6 Core Functions → **Govern, Identify, Protect, Detect, Respond, Recover**.  
  - 22 Categories → Asset management, risk assessment, etc.  
  - Provides a **common language** for security discussions.  
- **SP 800-37 (Risk Management Framework – RMF)**:  
  - Integrates security/privacy into the **system development lifecycle**.  
  - Risk management is **ongoing, adaptive, and iterative**.

---

### **FedRAMP (Federal Risk and Authorization Management Program)**
- US Government cloud security certification program.  
- Centralized certification for **cloud service providers (CSPs)**.  
- Marketplace lists approved vendors.  
- Saves time by reusing certifications across agencies.

---

### **SABSA (Sherwood Applied Business Security Architecture)**
- Less common but business-oriented.  
- **Top-down approach** – start with business requirements → security strategy → operational tactics.  
- Ensures **security supports business goals**.  
- Includes risk management to ensure proportional controls.

---

## 🧩 Control Types in Frameworks
- **Preventive**: Stop attacks (e.g., firewall).  
- **Detective**: Identify incidents (e.g., IDS/alarms).  
- **Corrective**: Fix issues (e.g., restore from backup).  
- **Deterrent**: Discourage attacks (e.g., warning signs, guards).  
- **Mechanisms**: Technical, Administrative, Physical.  
- **Defense-in-depth**: Multiple overlapping controls reduce risk of failure (false positives/negatives).

---

## 📊 Comparison Table

| Framework  | Focus Area | Typical Use |
|------------|------------|-------------|
| **COBIT**  | Governance & audit | Align IT/security with business; audit assessments |
| **ISO 27001/27002** | Security management & controls | Global certification, enterprise ISMS |
| **ISO 27701** | Privacy management | GDPR & privacy compliance |
| **ISO 31000** | Risk management | Enterprise-wide risk programs |
| **NIST 800-53** | Security & privacy controls | US government, also private orgs |
| **NIST CSF** | Cyber risk mgmt (6 functions) | Common language, high-level strategy |
| **NIST 800-37** | Risk Management Framework | Integrate risk/security into lifecycle |
| **FedRAMP** | Cloud service certification | US Gov CSP approval |
| **SABSA** | Business-driven security | Aligning security architecture with strategy |

---

✅ **Key Point**: Frameworks provide structure, consistency, and assurance that risks are covered across confidentiality, integrity, and availability. They also support compliance, audits, and business alignment.
# 📘 Security Policy Framework

Security professionals use a 4-part framework to provide clear guidance: **Policies, Standards, Guidelines, Procedures**.

---

## 🔑 Document Types

### **1. Policies**
- **Foundation** of the security program.
- High-level, carefully written, approved by senior leadership.
- Compliance = **mandatory**.
- Should be **timeless** (avoid overly specific tech/location references).
  - Example (Bad): "Encrypt with AES-256."
  - Example (Good): "Encrypt sensitive data using IT-approved methods."

---

### **2. Standards**
- Specific **technical/operational requirements**.
- Derive authority from policies.
- Compliance = **mandatory**.
- Examples: Approved encryption protocols, storage locations, config parameters.
- Often based on **CIS Benchmarks**, vendor configuration guides.

---

### **3. Guidelines**
- **Best practices & recommendations**.
- Compliance = **optional**.
- Example: "Use encrypted Wi-Fi when possible, or use VPN as backup."

---

### **4. Procedures**
- **Step-by-step instructions** for tasks.
- Compliance: **depends on organization/procedure** (may be mandatory or optional).
- Example: Incident response activation steps (text alert, start video conference, inform leadership).

---

## ✅ Exam Tip
- **Policies & Standards** → Always mandatory.  
- **Guidelines** → Always optional.  
- **Procedures** → May be mandatory or optional.  

# 🚀 DevOps and DevSecOps

## 🔑 DevOps
- **Goal**: Bridge gap between **developers** (rapid releases) & **operations** (stability).  
- **Philosophy**: Collaboration, open communication, automation.  
- **Tied to**: Agile & **Continuous Integration (CI)** → frequent code releases (daily or even hundreds/day).  

### Core Concept: **Infrastructure as Code (IaC)**
- Servers/configurations managed via **scripts**, not manual changes.
- **Advantages**:
  - Scalability: Spin up many servers quickly.
  - Reduced errors: Immutable servers (no manual login/config changes).
  - Easy testing: Test environments spun up/destroyed easily.

---

## 🔐 DevSecOps
- Extends DevOps by embedding **security into every phase** ("Security as Code").
- **Security automation**: Testing, monitoring, compliance integrated into CI/CD pipeline.
- Ensures stability, scalability, and **built-in security**.

---

## ✅ Exam Tip
- **DevOps** = Dev + Ops collaboration, automation, IaC.  
- **DevSecOps** = Same, but with **security integrated** into workflows.  



# 📊 Security Process Data, Reviews, Metrics, Audits & Control Management

## 1. Collecting Security Process Data
- **Types of data**:
  - **Technical Data**: Logs from servers, firewalls, IDS/IPS, access control systems, etc.  
    → Usually collected & analyzed via **SIEM systems**.  
  - **Process Data**: Documentation supporting security processes (e.g., backup tests, account reviews, vulnerability scans).
- **Why it matters**:
  - Enables **regular evaluation** of security processes.  
  - Provides **evidence for audits** (not just verbal assurances).  
- **Example**: Tracking quarterly user account reviews in a Google Sheet with version history → prevents falsified records.

---

## 2. Management Review
- **Purpose**:
  - Double-check employee work for accuracy & completeness.  
  - Reduce fraud/malfeasance via oversight.  
- **Key areas of focus**:
  - **Privileged Access Review**:  
    - Monitor admin/system engineer actions.  
    - Require RFCs (Request for Change) & VP approval for exceptions.  
    - Manager verifies via logs (100% or sample-based).  
  - **Account Management Review**:  
    - Verify active accounts belong to current staff.  
    - Check permissions are role-appropriate.  
    - Validate changes (escalations, creations, revocations).  

---

## 3. Security Metrics
- **Purpose**: Evaluate program effectiveness & risks over time.  
- **Types**:
  - **KPIs (Key Performance Indicators)** → Look backwards (past performance).  
    - Examples: % decrease in breaches, time to implement new controls, # of security trainings conducted.  
  - **KRIs (Key Risk Indicators)** → Look forward (future risk level).  
    - Criteria (per ISACA): Business impact, Implementation effort, Reliability, Sensitivity.  
- **Framework Reference**: ITIL framework (offers 9 suggested KPIs).  
- **Key Use**: Provides leadership with clear visibility into program health.

---

## 4. Audits and Assessments
- **Similarities**: Both evaluate security controls & recommend improvements.  
- **Differences**:  
  - **Assessment**: Informal, initiated by IT/security staff (self-check).  
  - **Audit**: Formal, requested by execs/regulators, follows strict standards.  
- **Examples**:
  - **PCI DSS audit**:  
    - Requirement: Encrypt/truncate/hash card numbers.  
    - Auditor must:  
      1. Examine documentation.  
      2. Review data repositories/logs.  
      3. Verify controls prevent reconstruction of card data.  
- **Auditors**:
  - **Internal**: Employed by org, but independent of audited unit.  
  - **External**: Independent firms (Big 4: PwC, EY, Deloitte, KPMG).  
- **Common Deliverables**:
  - **Gap analysis** → roadmap for remediation.  
  - **Attestation** → formal statement that controls are adequate & effective.  
- **Routine Use**: Regular audits & assessments build trust & compliance readiness.

---

## 5. Control Management
- **Routine Activities**:
  - **Control Testing**: Continuous/automated checks (e.g., monitor firewall port changes).  
  - **Exception Management**:  
    - Formal process to request exceptions (documented justification, risks, mitigations).  
    - Example: State of Washington exception request form.  
  - **Remediation Plans**: Document corrective steps for failed/missing controls.  
  - **Compensating Controls**: Alternative measures when exceptions are granted.  
    - Must:  
      1. Meet intent & rigor of original control.  
      2. Provide equal defense level.  
      3. Be **above & beyond** other controls (no double-counting).  
    - Example: PCI DSS detailed compensating control process.  

---

## ✅ Key Takeaways
- **Data collection** → enables evidence-based security validation.  
- **Management reviews** → prevent errors & insider misuse.  
- **Metrics (KPIs/KRIs)** → give measurable insight into performance & risk.  
- **Audits/assessments** → ensure compliance & identify gaps.  
- **Control management** → ensures security controls remain effective, exceptions are justified, and risks are managed with compensating measures.  
