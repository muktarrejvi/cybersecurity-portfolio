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
  6. **Access** – Allow individuals to review/update their data.  
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
