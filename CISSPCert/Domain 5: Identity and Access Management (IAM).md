# Chapter 5: Identity and Access Management (IAM)
**Domain 5** — Weight: **13%**

Identity and Access Management (IAM) is one of the most critical domains in CISSP. It focuses on **who** can access **what**, **when**, **how**, and **why**.

---

## Subdomains

### 5.1 Control physical and logical access to assets
- **Physical Access**: Controlling entry to buildings, rooms, data centers, and hardware (e.g., badge systems, biometrics, mantraps, guards).
- **Logical Access**: Controlling access to systems, networks, applications, and data.
- **Key Objective**: Ensure only authorized subjects (people, devices, services) can access assets.

### 5.2 Design identification and authentication strategy
- **Identification**: Claiming an identity (e.g., username, user ID, email).
- **Authentication**: Proving the claimed identity (verifying "you are who you say you are").
- **Authentication Factors**:
  - **Type 1** — Something you **know** (password, PIN, passphrase)
  - **Type 2** — Something you **have** (token, smart card, mobile device)
  - **Type 3** — Something you **are** (biometrics: fingerprint, iris, face)
  - **Type 4** — Somewhere you **are** (location-based, GPS)
- **Multifactor Authentication (MFA)**: Using two or more different types of factors.
- **Passwordless Authentication**: Passkeys, WebAuthn, FIDO2.

### 5.3 Federated identity with a third-party service
- **Federation**: Allowing users to use one identity across multiple systems or organizations.
- **Common Protocols**:
  - **SAML 2.0** — Security Assertion Markup Language (mostly enterprise SSO)
  - **OAuth 2.0** — Authorization framework (gives access without sharing password)
  - **OpenID Connect (OIDC)** — Authentication layer on top of OAuth 2.0
  - **WS-Federation**
- **Identity Providers (IdP)** vs **Service Providers (SP)**
- **Use Cases**: Single Sign-On (SSO), Cross-organization access (B2B, B2C)

### 5.4 Implement and manage authorization mechanisms
- **Authorization**: Determining **what** an authenticated user is allowed to do.
- **Common Models**:
  - **DAC** (Discretionary Access Control) — Owner decides (most common in OS)
  - **MAC** (Mandatory Access Control) — System enforces based on labels (e.g., SELinux, classified systems)
  - **RBAC** (Role-Based Access Control) — Most widely used in enterprises
  - **ABAC** (Attribute-Based Access Control) — Most flexible (uses attributes)
  - **Rule-Based Access Control**
- **Principle of Least Privilege (PoLP)**
- **Separation of Duties (SoD)**
- **Need-to-Know**

### 5.5 Manage the identity and access provisioning lifecycle
- **Joiner – Mover – Leaver (JML)** process
- **Provisioning**: Creating accounts and access rights
- **Account Review & Certification** (attestation)
- **De-provisioning**: Removing access (critical for security)
- **Access Recertification**
- **Privilege Creep** prevention

### 5.6 Implement authentication systems
- **Single Sign-On (SSO)**
- **Kerberos** (Ticket-based authentication)
- **LDAP / Active Directory**
- **RADIUS** & **TACACS+** (for network access)
- **Diameter**
- **CHAP, PAP, EAP**
- **Certificate-based authentication**
- **Biometric systems** (FRR, FAR, CER)
- **Context-aware authentication**

---

## Key IAM Concepts

- **IAAA**:
  - Identification
  - Authentication
  - Authorization
  - Accountability (Auditing)

- **Zero Trust Model**:
  - Never trust, always verify
  - Continuous authentication & authorization

- **Identity as a Service (IDaaS)**

- **Privileged Access Management (PAM)**

- **Just-In-Time (JIT) Access**

---

## Common Exam Tips

- Strongest authentication = **MFA** using different factor types.
- Federation is about **trust relationships** between organizations.
- RBAC is most commonly implemented in real-world enterprises.
- De-provisioning (removing access when someone leaves) is a frequent exam scenario.
- Least Privilege + Separation of Duties are core security principles.

---

**Cross-References**:
- Chapter 1: Security Governance & CIA Triad
- Chapter 6 & 7: Cryptography (used in authentication)
- Chapter 8: Software Development Security
- Chapter 15: Security Assessment & Testing
