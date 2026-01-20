# Domain 5 – Cryptography (SSCP)

## Overview
Cryptography is a core security control used to protect data and communications.  
This domain focuses on **why cryptography is needed**, **how cryptographic mechanisms work**, and **how secure protocols and PKI systems are implemented and supported**.

---

## 5.1 Understand Reasons and Requirements for Cryptography

### Confidentiality
- Ensures that information is **only accessible to authorized users**.
- Prevents unauthorized disclosure of sensitive data.
- Commonly achieved using **encryption**.
- Examples:
  - Encrypting data stored on disk
  - Encrypting network communications (TLS, IPsec)

### Integrity
- Ensures data has **not been altered** intentionally or accidentally.
- Protects against tampering and corruption.
- Achieved using:
  - Hashing
  - Message Authentication Codes (MACs)
  - Digital signatures

### Authenticity
- Verifies the **identity of users, systems, or messages**.
- Confirms that data originates from a legitimate source.
- Achieved using:
  - Digital certificates
  - Digital signatures
  - Authentication protocols

### Data Sensitivity
Different types of data require cryptographic protection due to their value and legal implications:
- **Personally Identifiable Information (PII)**  
  - Names, addresses, national IDs, phone numbers
- **Protected Health Information (PHI)**  
  - Medical records, diagnoses, insurance details
- **Intellectual Property (IP)**  
  - Source code, trade secrets, designs

### Regulatory and Industry Best Practices
Cryptography is often **mandatory** to meet compliance requirements:
- **PCI DSS** – Requires encryption of cardholder data
- **ISO/IEC standards** – Define security and cryptographic best practices
- **HIPAA** – Protects health information
- **GDPR** – Requires protection of personal data

---

## 5.2 Apply Cryptography Concepts

### Hashing
- Converts data into a **fixed-length digest**.
- One-way function (cannot be reversed).
- Used for:
  - Password storage
  - Integrity verification
- Examples:
  - SHA-256
  - SHA-512

### Salting
- Adds a **random value** to data before hashing.
- Prevents:
  - Rainbow table attacks
  - Hash reuse across systems
- Especially important for **password security**.

### Symmetric Encryption
- Uses **one shared secret key** for encryption and decryption.
- Fast and efficient.
- Key management is challenging.
- Example:
  - **AES (Advanced Encryption Standard)**

### Asymmetric Encryption
- Uses a **key pair**:
  - Public key (encryption)
  - Private key (decryption)
- Slower than symmetric encryption.
- Used for:
  - Key exchange
  - Digital signatures
- Example:
  - **RSA**

### Elliptic Curve Cryptography (ECC)
- Asymmetric cryptography based on elliptic curves.
- Provides **strong security with smaller keys**.
- More efficient than RSA.
- Common in:
  - Mobile devices
  - Modern TLS implementations

### Non-Repudiation
- Prevents a sender from **denying an action**.
- Ensures accountability.
- Achieved using:
  - Digital signatures
  - Certificates
  - Audit logs
  - HMAC (in some use cases)

### Strength of Encryption Algorithms and Keys
- Security depends on **algorithm choice** and **key length**.
- Common examples:
  - AES-256 – Strong symmetric encryption
  - RSA-2048 – Minimum acceptable asymmetric key size
- Larger keys = stronger security but slower performance.

### Cryptographic Attacks and Countermeasures
- **Cryptanalysis**: Attempts to break cryptographic systems.
- Common threats:
  - Brute-force attacks
  - Weak key usage
  - Poor randomness
- **Quantum computing** threatens traditional algorithms:
  - RSA and ECC are vulnerable
  - Post-quantum cryptography is emerging as a countermeasure

---

## 5.3 Understand and Implement Secure Protocols

### Secure Services and Protocols

#### IPsec
- Secures IP communications at the **network layer**.
- Provides:
  - Encryption
  - Authentication
  - Integrity
- Commonly used in **VPNs**.

#### TLS (Transport Layer Security)
- Secures data in transit.
- Used by:
  - HTTPS
  - Secure email
  - APIs
- Provides confidentiality, integrity, and authentication.

#### S/MIME
- Secures email using encryption and digital signatures.
- Requires certificates.
- Used in enterprise email environments.

#### DKIM
- Used to verify **email authenticity**.
- Prevents email spoofing.
- Ensures email integrity and sender validation.

### Common Use Cases
- Secure web browsing
- Secure email
- Virtual private networks
- Secure system-to-system communication

### Limitations and Vulnerabilities
- Weak configuration (old protocols, weak ciphers)
- Certificate mismanagement
- Man-in-the-middle (MITM) attacks
- Protocol downgrade attacks

---

## 5.4 Understand and Support Public Key Infrastructure (PKI) Systems

### PKI Overview
- Framework that manages **digital certificates and public keys**.
- Enables trust in distributed systems.

### Fundamental Key Management Concepts
- **Key Generation** – Secure creation of keys
- **Storage** – Protecting private keys
- **Rotation** – Periodic key replacement
- **Exchange** – Secure key distribution
- **Revocation** – Invalidating compromised keys
- **Destruction** – Secure key disposal
- **Escrow** – Trusted third-party key storage (controlled use)

### Web of Trust (WoT)
- Decentralized trust model.
- Users validate each other’s keys.

#### Examples
- **PGP (Pretty Good Privacy)**
- **GPG (GNU Privacy Guard)**
- **Blockchain-based trust models**

### Comparison with Traditional PKI
- PKI relies on **Certificate Authorities (CAs)**.
- Web of Trust relies on **peer validation**.
- WoT is flexible but harder to manage at scale.

---

## Key Exam Takeaways
- Understand **why cryptography is required**, not just how it works.
- Memorize **algorithm types**, **key sizes**, and **use cases**.
- Know **secure protocols** and their limitations.
- Be comfortable with **PKI concepts and key management**.
- Expect scenario-based questions on **confidentiality, integrity, and authenticity**.

