# Chapter 3: Security Architecture and Engineering (Domain 3)

**Domain Weight**: 13% of the CISSP Exam (2024/2025 outline)

**Purpose of this Domain**:  
This domain focuses on **designing, building, and evaluating secure systems** from the ground up. It combines theoretical security models, secure design principles, cryptography, system hardware/software capabilities, and physical facility security. It is highly technical and conceptual.

---

## 3.1 Research, Implement, and Manage Engineering Processes Using Secure Design Principles

### Core Secure Design Principles
- **Defense in Depth** (Layered controls)
- **Least Privilege**
- **Economy of Mechanism** (Keep design simple)
- **Fail-Safe Defaults** (Default to deny)
- **Separation of Duties**
- **Complete Mediation** (Check every access)
- **Open Design** (Kerckhoffs' Principle — algorithm public, key secret)
- **Least Common Mechanism** (Minimize shared resources)
- **Psychological Acceptability** (User-friendly security)
- **Work Factor** (Make attack more expensive than value gained)

### Additional Principles
- **Secure by Design**, **Secure by Default**, **Secure by Deployment**
- **Zero Trust Architecture**
- **Threat Modeling** (STRIDE, PASTA, DREAD)

**Exam Tip**: Be able to name and explain at least 6–8 principles with real-world examples.

---

## 3.2 Understand the Fundamental Concepts of Security Models

### Confidentiality Models
- **Bell-LaPadula (BLP) Model**
  - **Rule**: No Read Up (Simple Security Property), No Write Down (*-Property)
  - Focus: **Confidentiality**
  - Used in military/government classified systems

### Integrity Models
- **Biba Model**
  - **Rule**: No Read Down, No Write Up
  - Focus: **Integrity** (prevents low-integrity data from contaminating high-integrity data)
- **Clark-Wilson Model**
  - Focus: Commercial integrity, well-formed transactions, Separation of Duties

### Other Important Models
- **Brewer-Nash Model** (Chinese Wall) — Prevents conflicts of interest
- **Graham-Denning Model** — Access rights and operations
- **Harrison-Ruzzo-Ullman (HRU) Model** — Theoretical access matrix
- **Non-interference Model** — Prevents one system from affecting another

**Exam Tip**: Know the primary goal of each model (Confidentiality vs Integrity) and their key rules.

---

## 3.3 Select Controls Based Upon System Security Requirements

### Control Selection Process
- **Security Requirements** → Derived from risk assessment, regulations, and business needs
- Use frameworks: **NIST SP 800-53**, **ISO 27001**, **CIS Controls**, **COBIT**

### Control Types (by Function)
- **Preventive**, **Detective**, **Corrective**, **Deterrent**, **Compensating**, **Recovery**

### Control Categories
- **Administrative** (Policies, procedures)
- **Technical** (Firewalls, encryption)
- **Physical** (Locks, fences)

**Exam Tip**: Controls must be **appropriate**, **cost-effective**, and **proportionate** to risk.

---

## 3.4 Understand Security Capabilities of Information Systems

### Hardware Security Capabilities
- **Trusted Platform Module (TPM)** — Hardware root of trust, secure boot, key storage
- **Hardware Security Module (HSM)** — High-security cryptographic key generation and storage
- **Trusted Execution Environment (TEE)** / **Secure Enclave**
- **Memory Protection**:
  - Address Space Layout Randomization (ASLR)
  - Data Execution Prevention (DEP/NX bit)
  - Memory segmentation and paging

### Processor Security Features
- **Intel SGX**, **AMD SEV**
- **Secure Boot** and **Measured Boot**

### Software Security Capabilities
- **Virtualization** and **Hypervisors** (Type 1 & Type 2)
- **Container Security**
- **Sandboxing**

---

## 3.5 Assess and Mitigate Vulnerabilities of Security Architectures, Designs, and Solution Elements

### Common Vulnerabilities
- **TOCTOU** (Time-of-Check to Time-of-Use)
- **Covert Channels**:
  - Storage channels
  - Timing channels
- **Side-Channel Attacks** (Power analysis, timing attacks)
- **Object Reuse** issues
- **Buffer Overflows**, **Race Conditions**, **Improper Error Handling**

### Architecture Vulnerabilities
- Single points of failure
- Insecure design in Cloud, IoT, Mobile, Embedded systems
- Distributed systems issues (consensus, Byzantine faults)

**Mitigation Strategies**: Input validation, secure coding, code reviews, threat modeling.

---

## 3.6 Select and Determine Cryptographic Solutions

### Cryptographic Types
- **Symmetric** (AES, ChaCha20) — Fast, single key
- **Asymmetric** (RSA, ECC, Diffie-Hellman) — Public/private key pairs
- **Hashing** (SHA-256, SHA-3) — One-way, integrity
- **Digital Signatures** — Non-repudiation + integrity
- **Key Exchange** (ECDHE, RSA)

### Key Management (Very Important)
- Generation, Distribution, Storage, Rotation, Destruction (Crypto Shredding)
- **Key Escrow**, **M-of-N Control**

### Use Cases
- Data at Rest, Data in Transit, Data in Use
- PKI (Certificates, CA, CRL, OCSP)
- Quantum Cryptography & Post-Quantum Algorithms

---

## 3.7 Understand Methods of Cryptanalytic Attacks

### Attack Types
- **Brute Force** — Try all possible keys
- **Known-Plaintext Attack**
- **Chosen-Plaintext Attack**
- **Chosen-Ciphertext Attack**
- **Differential Cryptanalysis**
- **Linear Cryptanalysis**
- **Side-Channel Attacks** (Timing, Power, Electromagnetic)
- **Frequency Analysis** (Classic ciphers)
- **Rainbow Table Attacks** (against hashes)
- **Birthday Attack** (Hash collisions)

**Exam Tip**: Understand which attacks apply to symmetric vs asymmetric vs hashing.

---

## 3.8 Apply Security Principles to Site and Facility Design

### CPTED (Crime Prevention Through Environmental Design)
- Natural Surveillance, Territorial Reinforcement, Natural Access Control

### Site Selection Considerations
- Location, natural hazards, crime rate, proximity to emergency services
- Visibility and perimeter control

### Facility Design Principles
- Defense in Depth (perimeter, building, room, object)
- Zoning (public, semi-public, restricted, highly restricted)

---

## 3.9 Design Site and Facility Security Controls

### Physical Controls
- **Perimeter**: Fences, gates, bollards, lighting, CCTV
- **Building**: Mantraps, turnstiles, access control systems (badge + biometric)
- **Internal**: Motion sensors, door locks, secure cabinets
- **Environmental Controls**: HVAC, fire suppression (FM-200, Inergen), UPS, generators
- **Water, Gas, and Power Protection**

### Key Concepts
- **Fail-Safe vs Fail-Secure** locks
- **Tailgating / Piggybacking** prevention

---

## 3.10 Manage the Information System Lifecycle

### System Development Life Cycle (SDLC)
1. **Requirements**
2. **Acquisition / Design**
3. **Development / Implementation**
4. **Testing / Validation**
5. **Operation / Maintenance**
6. **Disposal / Decommissioning** (Secure sanitization)

### Software Development Security
- Secure SDLC (SSDLC)
- DevSecOps
- OWASP Top 10 integration

**Exam Tip**: Security must be integrated at every phase of the lifecycle.

---

## Domain 3 Summary & High-Yield Topics

**Most Important Areas**:
- Secure Design Principles (especially Defense in Depth & Fail-Safe)
- Security Models (Bell-LaPadula vs Biba)
- Cryptography (Symmetric vs Asymmetric, Key Management, Attacks)
- TPM / HSM / Secure Boot
- Physical Security & CPTED
- SDLC Integration

**Key Mindset**: Security Architecture is about **building systems that are secure by design**, not just adding controls later.

**Study Recommendations**:
- Memorize Bell-LaPadula and Biba rules clearly.
- Understand cryptographic strengths/weaknesses.
- Practice mapping security models to real scenarios.
