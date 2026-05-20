# Chapter 2: Asset Security (Domain 2)

**Domain Weight**: 10% of the CISSP Exam (2024/2025/2026 outline)

**Core Purpose**:  
This domain focuses on **identifying, classifying, protecting, and managing information and assets** throughout their entire lifecycle — from creation to secure disposal. It ensures that assets receive protection **commensurate with their value and sensitivity**.

---

## 2.1 Identify and Classify Information and Assets

### Key Concepts
- **Asset Identification**: Creating and maintaining a complete inventory of all valuable items (tangible and intangible).
- **Classification**: Labeling assets based on sensitivity, criticality, and business impact.

### Asset Types / Categories
- **Information / Data Assets** — Databases, documents, intellectual property, PII, PHI, financial records.
- **Physical Assets** — Hardware (servers, laptops, mobile devices), buildings, equipment.
- **Intangible Assets** — Software, licenses, reputation, brand, processes.
- **Digital Assets** — Cloud resources, VMs, containers, APIs.
- **Supporting Assets** — Networks, facilities, personnel.

### Data Classification Schemes

#### 1. **Commercial / Private Sector** (Most Common in CISSP)
- **Confidential** — Highest sensitivity (trade secrets, M&A data).
- **Private / Sensitive** — Internal use (employee data, financials).
- **Restricted** — Limited internal distribution.
- **Public** — No harm if disclosed.

#### 2. **Government / Military**
- **Top Secret**
- **Secret**
- **Confidential**
- **Unclassified** (sometimes with **Sensitive But Unclassified - SBU**)

### Classification Criteria
- **Sensitivity** — Potential damage from disclosure (Confidentiality).
- **Criticality** — Importance to business operations (Availability).
- **Value** — Monetary or strategic worth.
- **Regulatory Requirements** — GDPR, HIPAA, PCI-DSS, etc.

**Roles in Classification**:
- **Data Owner** — Business owner, decides classification and protection level.
- **Data Custodian** — Implements and maintains controls (IT/Security team).
- **Data Processor** — Processes data on behalf of controller (e.g., cloud providers).
- **Data User / Subject** — End users who access data.

**Exam Tip**: Classification must be **done at creation** and reviewed periodically.

---

## 2.2 Establish Information and Asset Handling Requirements

### Handling Requirements by Classification
Procedures for **labeling, storing, transmitting, and destroying** assets based on their classification.

#### Media Handling
- **Marking & Labeling** — Clear, durable labels indicating classification.
- **Storage** — Physical (locked cabinets) vs Digital (encryption, access controls).
- **Transmission** — Encryption in transit (TLS, IPsec), secure file transfer.
- **Destruction** — Shredding, degaussing, pulverizing, cryptographic erase.

#### Key Principles
- **Need-to-Know** — Access granted only when required for job function.
- **Least Privilege** — Minimum permissions necessary.
- **Separation of Duties** — Prevent single person from controlling entire process.

**Handling Procedures** include:
- Secure transport (tamper-evident packaging).
- Chain of custody for sensitive media.
- Clear desk / clear screen policies.

---

## 2.3 Provision Information and Assets Securely

### Core Activities
- **Asset Ownership** — Assign accountability (Data Owner / System Owner).
- **Asset Inventory** — Comprehensive, up-to-date list (CMDB tools).
- **Asset Management** — Tracking, maintenance, and lifecycle oversight.

### Secure Provisioning Practices
- **Secure Baselines** — Hardened configurations before deployment.
- **Change Management** — Controlled introduction of new assets.
- **Configuration Management** — Maintaining known-good states.
- **Secure Supply Chain** — Vendor assessments, trusted sourcing.

**Exam Tip**: Ownership = **accountability**. Custodians = **responsibility** for implementation.

---

## 2.4 Manage Data Lifecycle

### Data Lifecycle Phases (Common Model)

| Phase              | Description                                      | Key Security Activities                     |
|--------------------|--------------------------------------------------|---------------------------------------------|
| **Creation / Collection** | Data is generated or acquired                   | Classify immediately, validate input        |
| **Storage**        | Data is saved (databases, files, backups)       | Encryption at rest, access controls         |
| **Usage / Processing** | Data is actively used                           | Monitoring, DLP, least privilege            |
| **Sharing / Transmission** | Data is moved internally or externally     | Encryption in transit, secure channels      |
| **Archiving**      | Data moved to long-term storage                  | Review retention needs                      |
| **Destruction / Disposal** | Data is permanently removed                | Secure erase, cryptographic wipe            |

### Important Concepts
- **Data Remanence** — Residual data left after normal deletion (magnetic residue, etc.).
- **Data Location** — Know where data resides (especially in cloud/multi-jurisdictional environments).
- **Data Maintenance** — Ongoing integrity checks, patching, backups.
- **Data Roles** — Owner, Controller, Custodian, Processor, User.

**Methods to Counter Data Remanence**:
- Overwriting (multiple passes).
- Degaussing (for magnetic media).
- Physical destruction (shredding, incineration).
- Cryptographic Erase (key destruction).

---

## 2.5 Ensure Appropriate Asset Retention (EOL / EOS)

### Retention Concepts
- Retain data/assets **only as long as needed** for business, legal, or regulatory reasons.
- Over-retention increases risk and cost.
- Under-retention creates compliance and legal issues.

### Key Terms
- **End of Life (EOL)** — Manufacturer no longer sells or produces the product.
- **End of Support (EOS / EOSL)** — No more security patches or technical support.
- **End of Service** — Vendor stops providing services.

### Retention Strategies
- **Retention Schedules** — Tied to classification and regulations (e.g., 7 years for financial data).
- **Legal Hold** — Suspend normal destruction for litigation.
- **Secure Disposal** at end of retention period.

**Risks of Poor Retention**:
- Increased attack surface (unsupported systems).
- Regulatory fines.
- Higher storage costs.

---

## 2.6 Determine Data Security Controls and Compliance Requirements

### Data Security Controls Categories
- **Technical** — Encryption, DLP, access controls, masking, tokenization, anonymization.
- **Administrative** — Policies, procedures, training, NDAs.
- **Physical** — Facility controls, media storage, secure disposal.

### Common Data Protection Techniques
- **Encryption** (at rest & in transit).
- **Data Loss Prevention (DLP)**.
- **Data Masking / Redaction**.
- **Tokenization**.
- **Anonymization / Pseudonymization** (important for GDPR).
- **Access Controls** (RBAC, ABAC).

### Compliance Requirements
- Map controls to regulations: GDPR, CCPA, HIPAA, PCI-DSS, SOX, etc.
- **Scoping vs Tailoring** controls to organizational needs.

**Exam Tip**: Controls must be **commensurate with risk and classification level**.

---

## Summary Mind Map

- **2.1** → Identify + Classify (What is it? How sensitive?)
- **2.2** → Handling Requirements (How should we treat it?)
- **2.3** → Secure Provisioning + Ownership + Inventory
- **2.4** → Full Data Lifecycle Management
- **2.5** → Retention + EOL/EOS + Secure Disposal
- **2.6** → Appropriate Controls + Compliance

**Key CISSP Mindset for Domain 2**:
- "Protect the asset according to its **value and sensitivity**."
- Classification drives **everything** else (handling, controls, retention).
- Security follows the **data** wherever it goes (lifecycle).

**High-Yield Exam Topics**:
- Data Owner vs Custodian responsibilities
- Commercial vs Government classification levels
- Data Remanence & Destruction methods
- Need-to-Know + Least Privilege
- Data Lifecycle phases

---

**Study Recommendations**:
- Memorize classification levels and roles.
- Understand differences between destruction methods.
- Practice scenarios: "A company is merging — how should they classify and handle new data?"
- Review NIST SP 800-53 and ISO 27001 controls related to assets.
