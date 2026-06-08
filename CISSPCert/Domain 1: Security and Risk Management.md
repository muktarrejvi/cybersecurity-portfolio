# Chapter 1: Security and Risk Management (Domain 1)

**Domain Weight**: 16% (Highest weighted domain in CISSP)

**Purpose of this Domain**:  
This domain lays the **foundation** for all other domains. It covers the managerial, governance, legal, ethical, and risk aspects of security. It focuses on how security supports **business objectives** rather than just technical controls. CISSP expects you to think like a **security manager/CISO**, not just a technician.

---

## 1.1 Understand, Adhere to, and Promote Professional Ethics

### Key Ethics Codes
- **(ISC)² Code of Ethics** (Most Important for CISSP)
  - **Four Canons** (in priority order):
    1. Protect society, the common good, necessary public trust and confidence in information and systems.
    2. Act honorably, honestly, justly, responsibly, and legally.
    3. Provide diligent and competent service to principals.
    4. Advance and protect the profession.

### Other Ethics Frameworks
- ACM Code of Ethics
- IEEE Code of Ethics
- Organizational ethics (corporate code of conduct)

**Exam Tip**: Always prioritize the **(ISC)² Code of Ethics Canons** in the correct order.

---

## 1.2 Understand and Apply Security Concepts

### The 5 Pillars of Information Security
1. **Confidentiality** — Prevent unauthorized disclosure
2. **Integrity** — Prevent unauthorized modification
3. **Availability** — Ensure timely and reliable access
4. **Authenticity** — Verify identity of subject or object
5. **Non-repudiation** — Prevent denial of actions (usually via digital signatures)

**CIA Triad** = Confidentiality + Integrity + Availability (Most fundamental concept)

### Additional Important Concepts
- **Defense in Depth** (Layered security)
- **Security through Obscurity** (Generally bad — see Kerckhoffs’ Principle)
- **Kerckhoffs’ Principle** — Algorithm can be public; only key must be secret
- **Due Care** vs **Due Diligence**
  - Due Care = Doing what a prudent person would do (day-to-day)
  - Due Diligence = Verifying that due care is being done (periodic checks)

---

## 1.3 Evaluate, Apply, and Sustain Security Governance Principles

### Core Governance Principles
- Alignment of security with **business strategy, goals, mission, and objectives**
- Organizational roles and responsibilities (CISO, DPO, Board, etc.)
- Security control frameworks:
  - **ISO 27001 / 27002**
  - **NIST Cybersecurity Framework (CSF) & SP 800-53**
  - **COBIT** (IT governance)
  - **SABSA** (Enterprise security architecture)
  - **PCI-DSS**
  - **FedRAMP** (Cloud for US government)

### Organizational Processes
- Acquisitions & mergers
- Divestitures
- Governance committees (e.g., Security Steering Committee)

**Exam Tip**: Security must be **business-aligned**, not just a technical function.

---

## 1.4 Understand Legal, Regulatory, and Compliance Issues

### Major Categories
- **Privacy Laws**:
  - GDPR (EU)
  - CCPA / CPRA (California)
  - HIPAA (US Health)
  - PIPEDA (Canada)
- **Intellectual Property**:
  - Copyright, Patents, Trademarks, Trade Secrets
- **Computer Crime Laws**:
  - CFAA (US)
  - Computer Misuse Act (UK)
- **Transborder Data Flow** issues
- **Licensing & Intellectual Property Agreements**

### Compliance vs. Conformance
- **Compliance** = Meeting legal/regulatory requirements
- **Conformance** = Meeting internal standards or frameworks

**Key Concept**: Extraterritoriality (e.g., GDPR applies globally if targeting EU residents)

---

## 1.5 Understand Requirements for Investigation Types

### Investigation Types
| Type              | Purpose                              | Standard of Proof              | Key Feature                     |
|-------------------|--------------------------------------|--------------------------------|---------------------------------|
| Administrative    | Internal policy violations           | Preponderance of evidence      | HR/Disciplinary                 |
| Criminal          | Law violations                       | Beyond reasonable doubt        | Police, Chain of Custody        |
| Civil             | Lawsuits between parties             | Preponderance of evidence      | e-Discovery                     |
| Regulatory        | Regulatory violations                | Varies                         | Industry regulators             |
| Industry Standards| Certification/Compliance audits      | Contractual                    | PCI, ISO, SOC2                  |

**Critical Concepts**:
- **Chain of Custody**
- **Order of Volatility**
- **Legal Hold**

---

## 1.6 Develop, Document, and Implement Security Policy, Standards, Procedures, and Guidelines

### Hierarchy (from highest to lowest)
1. **Policies** — High-level, mandatory, "what" and "why"
2. **Standards** — Mandatory, specific, "how" (e.g., use AES-256)
3. **Procedures** — Step-by-step instructions
4. **Guidelines** — Recommended, not mandatory (best practices)

**Policy Types**:
- Enterprise Security Policy
- Issue-Specific Policies (Acceptable Use, Password, etc.)
- System-Specific Policies

---

## 1.7 Identify, Analyze, Assess, Prioritize, and Implement Business Continuity (BC) Requirements

- **Business Impact Analysis (BIA)** — Most important activity
  - Identifies critical business functions
  - Determines **Maximum Tolerable Downtime (MTD)**
  - **Recovery Time Objective (RTO)**
  - **Recovery Point Objective (RPO)**

**BC Concepts**:
- Continuity Planning
- Recovery strategies

---

## 1.8 Contribute to and Enforce Personnel Security Policies

### Key Areas
- **Hiring** — Background checks, NDAs
- **Onboarding** — Security awareness training
- **Termination** — Exit interviews, access revocation
- **Job Rotation**
- **Mandatory Vacations**
- **Separation of Duties**
- **Least Privilege**
- **Dual Control / Two-Person Rule**

**Insider Threat Mitigation**

---

## 1.9 Understand and Apply Risk Management Concepts

### Risk Management Process
1. **Identify** risks
2. **Analyze** (Qualitative vs Quantitative)
3. **Assess** (Risk rating)
4. **Prioritize**
5. **Respond** (Treat, Tolerate, Terminate, Transfer)
6. **Monitor**

### Risk Analysis Types
- **Qualitative** — Subjective (High/Med/Low)
- **Quantitative** — Numeric (uses ALE = SLE × ARO)

**Key Formulas**:
- **Single Loss Expectancy (SLE)** = Asset Value × Exposure Factor
- **Annualized Loss Expectancy (ALE)** = SLE × Annualized Rate of Occurrence (ARO)

**Risk Frameworks**: NIST RMF, ISO 31000, OCTAVE, FAIR

---

## 1.10 Understand and Apply Threat Modeling Concepts and Methodologies

### Popular Threat Modeling Methods
- **STRIDE** (Microsoft) — Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege
- **PASTA** (Process for Attack Simulation and Threat Analysis)
- **DREAD** (Older — Damage, Reproducibility, Exploitability, Affected users, Discoverability)
- **Attack Trees**
- **MITRE ATT&CK Framework**

**Threat Modeling Stages**:
1. Decompose the application
2. Identify threats
3. Mitigate threats
4. Validate

---

## 1.11 Apply Supply Chain Risk Management (SCRM) Concepts

### Supply Chain Risks
- Hardware tampering / implants
- Counterfeit products
- Third-party vendor compromises (SaaS, IaaS, suppliers)
- Software Bill of Materials (SBOM)
- Cloud supply chain risks

### Risk Mitigations
- Third-party assessments & monitoring
- Minimum security requirements
- Service Level Agreements (SLAs)
- Silicon Root of Trust / Physically Unclonable Function (PUF)
- Vendor due diligence

**Exam Tip**: Supply chain attacks (SolarWinds, Log4j, MOVEit) made this topic very important.

---

## 1.12 Establish and Maintain a Security Awareness, Education, and Training Program

### Key Elements
- **Awareness** — "What" (reminders, posters)
- **Training** — "How" (skills development)
- **Education** — "Why" (deeper understanding)

### Best Practices
- Role-based training
- Phishing simulations
- Metrics (click rates, completion rates)
- Continuous reinforcement (not just annual)

---

## Domain 1 Summary & High-Yield Topics

**Most Important Topics for Exam**:
- (ISC)² Code of Ethics (Canons order)
- CIA Triad + 5 Pillars
- Due Care vs Due Diligence
- Policy vs Standard vs Procedure vs Guideline
- Risk Management (especially Quantitative formulas)
- BIA, RTO, RPO
- STRIDE Threat Modeling
- Supply Chain Risk Management

**Mindset**: Think like senior management — focus on **governance, risk, compliance, and business alignment**.

---

**Study Recommendations**:
- Memorize ethics canons in order.
- Master risk formulas (SLE, ALE).
- Understand differences between policies, standards, procedures.
- Review real-world supply chain attacks.
Security champions: This involves selecting motivated individuals in each department to act as security advocates and promote best practices. It does not use points or scoring systems.
Social engineering: This is an attack technique (e.g., phishing), not a defensive awareness method.
Awareness training: This is the general category, but too broad. The specific method described (points + rewards + competition) is gamification, which is a specialized technique within awareness programs.
