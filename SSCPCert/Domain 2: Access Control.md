# Access Controls Domain – Key Takeaways

## Overview
- The **Access Controls** domain is the **second** of the seven SSCP domains, accounting for **15% of exam questions**.  
- Focuses on:
  - Implementing and maintaining **authentication methods**  
  - Understanding **Internet trust architectures**  
  - Supporting the **Access Management Lifecycle**  
  - Administering **Access Control Systems**  
- Forms the foundation of **Identity and Access Management (IAM)** in cybersecurity.

---

## Identity and Access Management (IAM)
- **IAM** ensures that systems can correctly identify users and control their access to prevent unauthorized actions.  
- The concept of **identity** includes **entities**, **identities**, and **attributes**:
  - **Entity:** The base unit — can be a **person**, **group**, **device**, or **system**.
  - **Identity:** The *role or representation* of an entity (e.g., staff, student, faculty).
  - **Attributes:** Descriptive data (e.g., major, graduation year, donor status).

### Example: College Campus Scenario
- **Alice:** One identity – *faculty member*.  
- **Bob:** Multiple identities – *staff member, alumnus, student*.  
- Each identity has attributes like:
  - Major: Computer Science  
  - Graduation Year: 2015  
  - Donor: Yes  

**Entities are not always humans** — they can be servers, network segments, or business units.

---

## Identification, Authentication, and Authorization (AAA)
These are the **three essential steps** in access control:

1. **Identification**
   - The user *claims* an identity (e.g., “I am Mike Chapple”).
   - This is **just a claim**, not yet proven.

2. **Authentication**
   - The user **proves** their identity (e.g., presenting an ID or entering a password).
   - Multiple authentication factors can be combined for stronger security.

3. **Authorization**
   - The system determines **what the authenticated user can access**.
   - Typically enforced via **Access Control Lists (ACLs)** or permissions.

### Digital Context
- **Username:** Used for identification.  
- **Password / Biometrics / Tokens:** Used for authentication.  
- **Permissions / Roles:** Define authorization.  

### Accounting
- Records and logs user activity for auditing.  
- Together, these form the **AAA model**:
  - **Authentication**
  - **Authorization**
  - **Accounting**

### Modern Environment
- IAM systems must function across **on-premises** and **cloud infrastructures**, integrating seamlessly in hybrid environments.

---

## Identification Mechanisms: Usernames & Access Cards

### Usernames
- Primary method for digital identification.  
- Should be **unique** and easy to associate with the correct individual (e.g., *jdoe* for John Doe).  
- **Not secret** – usernames are identifiers, not authenticators.

### Access Cards
- Often serve both **identification** and **authentication** purposes.
- Common types:
  - **Magnetic Stripe Cards:** Low security, easily cloned.
  - **Smart Cards:** Contain integrated chips; far more secure.
  - **Contactless / Proximity Cards:** Communicate via antenna; may be **passive** (powered by reader) or **active** (battery-powered).

**Best practice:** Ensure the system can **uniquely identify** every user and that cards are **tamper-resistant**.

---

## Registration and Identity Proofing

### Purpose
- To **create a new entity** in the system and ensure the individual’s **identity is genuine**.

### Four Steps of Registration
1. **Request Creation**
   - Example: A manager requests a new account for a newly hired employee.
2. **Approval**
   - A different authority must approve the request (separation of duties).
3. **Identity Proofing**
   - Verification that the person is who they claim to be.
4. **Credential Issuance**
   - Issuing login credentials or physical ID.

### Separation of Duties
- Four different individuals ideally handle each step:
  - Requester  
  - Approver  
  - Identity Proofer  
  - Credential Issuer  
- Reduces risk of **fraud** or **error**.

### Identity Proofing Methods
- Verification using **two independent photo IDs** (e.g., passport, driver’s license, military ID).  
- Optional **fingerprinting** or **background checks** for high-sensitivity roles.  
- In the U.S., documents must comply with **USCIS** guidelines; in other countries, use local government standards.

### Outcome
- Once proofing is complete, the organization can **safely issue credentials**, ensuring high confidence in user identity.

---

## Summary
- The Access Controls domain focuses on ensuring **only legitimate entities** can access systems through **robust identification, authentication, and authorization** mechanisms.  
- **IAM frameworks** unify people, processes, and technology to maintain security integrity.  
- Proper **registration** and **identity proofing** are critical first steps in safeguarding organizational assets.

---

**Next Steps in Study:**
- Understand **multi-factor authentication (MFA)** mechanisms.  
- Learn about **role-based access control (RBAC)** and **discretionary access control (DAC)** models.  
- Review **identity lifecycle management** processes.




# Authentication and Access Control Key Takeaways

## 1. Authentication Factors

| Factor | Description | Examples | Notes |
|--------|-------------|---------|-------|
| Something you know | Knowledge-based authentication | Passwords, passphrases, password keys | Strong passwords: mix upper/lowercase, digits, symbols; passphrases are memorable & secure |
| Something you are | Biometric traits | Fingerprint, face, iris, voice | Measures physical characteristics |
| Something you have | Physical possession | Smartphone, hardware token, key fob, smart card | OTP codes, smart card chips; adds strong security layer |

**Authentication Errors:**

| Error Type | Description | Measurement | Impact |
|------------|-------------|------------|-------|
| False Acceptance (FAR) | Unauthorized user granted access | FAR | High security risk |
| False Rejection (FRR) | Authorized user denied access | FRR | Affects availability |
| Crossover Error Rate (CER) | FAR = FRR | CER | Balanced measure of authentication strength |

---

## 2. Multifactor Authentication (MFA)

- Combines **two or more factors** from different categories.
- **Examples:**
  - Password (something you know) + Smart Card (something you have)
  - Fingerprint (something you are) + PIN (something you know)
- **Important:** Combining two techniques from the **same factor** (e.g., password + security question) is **not MFA**.
- **Benefit:** Reduces risk of account compromise.

---

## 3. Something You Have – Implementation

| Method | Description | Example | Protocol |
|--------|-------------|---------|---------|
| Hardware Token | Small device generates code | Key fob token | HOTP (counter-based) |
| Soft Token | Smartphone app generates OTP | Google Authenticator | TOTP (time-based; synchronized clocks) |
| Smart Card | Embedded chip verified by reader | US DoD CAC card | - |

- **OTPs (One-Time Passwords):** Used in both hardware & soft tokens.
- **Security Benefit:** Adds strong layer to password authentication.

---

## 4. Password Authentication Protocols

| Protocol | Description | Security Considerations |
|----------|-------------|------------------------|
| PAP | Username/password sent to server | No encryption; vulnerable to interception |
| CHAP | Challenge-response with shared secret | Password not sent over network; secure |
| MS-CHAP / MS-CHAPv2 | Microsoft version of CHAP | Broken; insecure, avoid use |

---

## 5. Single Sign-On (SSO) and Federation

- **Federated Identity Management:** Shared identity info across systems.
  - Example: Login with Google, Facebook, or Twitter accounts.
- **Single Sign-On:** Authenticated session shared across multiple systems.
  - Example: Active Directory + ADFS in enterprises.
  - Users log in once; session lasts for set period (e.g., business day).
- **Trust Relationships:**
  - **Direction:** One-way or two-way
  - **Transitivity:** Transitive (trust extends automatically) or nontransitive (manual trust needed)

---

## 6. Internetwork Trust Architectures

| Network Zone | Purpose | Notes |
|--------------|---------|-------|
| Border Firewall | Connects internet to intranet & DMZ | Blocks unauthorized inbound; allows outbound per policy |
| Intranet Zones | Internal networks | Segments: endpoints, wireless, guest, data center |
| DMZ (Demilitarized Zone) | Public-facing servers | Isolates high-risk systems from intranet |
| Extranet | Third-party access | Limited access via VPN; strict authentication & authorization |

**Key Principle:** Network segmentation reduces risk; compromise of one zone does not expose entire network.

# Authentication and Access Control Key Takeaways

## 7. Third-Party Connections

- **Interfaces for External Systems:**
  - APIs, app extensions, middleware.
  - Enable communication but introduce security challenges.
- **Security Practices:**
  - Secure coding, authentication & authorization mechanisms.
  - Input validation and encryption of data in transit.
  - Regular auditing and monitoring of APIs and middleware.
- **Vendor Management:**
  - Conduct due diligence before integrating third-party systems.
  - Assess security practices, incident response, compliance.
  - Include security expectations in contracts and SLAs.
- **Goal:** Proactive management reduces risks and strengthens overall security posture.

---

## 8. Zero-Trust Network Architecture

- **Concept:** Trust **individuals**, not networks.
- **Shift from Traditional Security:** Traditional perimeter-based security relies on network location; zero trust relies on strong authentication per user.
- **Key Components:**
  - Identity and Access Management (IAM) as cornerstone.
  - Continuous monitoring of user and network activity.
  - SIEM systems for log aggregation & anomaly detection.
  - SOAR platforms for automated incident response.
  - Cloud Access Security Brokers (CASB) for consistent cloud security policies.
  - Endpoint Detection & Response (EDR) for endpoint monitoring and automatic remediation.
- **Benefit:** Minimizes risk from compromised endpoints and enforces consistent security across users and devices.

---

## 9. SAML (Security Assertion Markup Language)

| Actor | Role |
|-------|------|
| Principal | End user requesting access |
| Identity Provider (IdP) | Verifies user's identity |
| Service Provider (SP) | Provides requested service |

**SAML Workflow:**
1. User requests access to SP resource.
2. SP checks for logged-in session; if none, redirects to IdP.
3. User authenticates to IdP (e.g., username/password, MFA).
4. IdP issues security assertion for SP.
5. SP validates assertion, establishes security context, and grants access.

**Benefits:**
- True Single Sign-On (SSO) experience.
- SP authenticates user without accessing user password.

---

## 10. OAuth and OpenID Connect

- **OAuth:** Authorization protocol, grants access permissions between services.
- **OpenID Connect (OIDC):** Authentication layer on top of OAuth; allows user identity verification.
- **Common Usage:** Logging into websites using Google, Facebook, LinkedIn, Amazon accounts.
- **Example Workflow:**
  1. User clicks "Sign in with LinkedIn" on third-party site.
  2. OAuth session redirects to identity provider (LinkedIn).
  3. User authenticates (username/password + MFA).
  4. User redirected back to third-party site with access granted.
- **Benefit:** Provides secure federated SSO without sharing passwords.

---

## 11. Device Authentication

- **Digital Certificates:**
  - Act as “something you have” factor.
  - Authenticate users, devices, servers.
  - Used in SSH connections, PKI smart cards, IEEE 802.1x network authentication.
- **Key-Based Authentication (Public/Private Keys):**
  - Private key kept secret; public key shared with server.
  - SSH authentication: server sends challenge → user encrypts with private key → server verifies with public key.
  - Allows automated server-to-server authentication without passwords.
- **Certificate-Based Authentication:**
  - Public key signed by trusted certificate authority.
  - Confirms both possession of key and user/device identity.
- **MAC Address Authentication:**
  - Uses hardware MAC address for identification.
  - **Limitation:** Easily spoofed; not considered secure.
- **Practical Example (SSH on AWS EC2):**
  - Generate key pair (public/private).
  - Store public key on server, private key locally.
  - Use SSH with private key to authenticate.
  - Set restrictive permissions on private key for security (`chmod 0600`).

## 12. Account and Privilege Management

### Account Management Principles
- **Least Privilege:** Users get only the permissions needed for their role.
- **Separation of Duties:** Sensitive actions require collaboration between multiple individuals.
- **Job Rotation & Mandatory Vacation:** Reduces fraud risk by rotating roles and enforcing absence.
- **Naming Conventions:** Standardized account names help tie accounts to real identities.
- **Account Lifecycle Management:**
  - Provisioning: Grant new users correct access.
  - Modifying: Adjust permissions when roles change.
  - Recertification: Review and remove unnecessary access.
  - Deprovisioning: Remove access of terminated users.

---

### Account Policies
- **Group Policy Objects (GPOs) in Windows:**
  - Apply security and configuration settings across domains.
  - Example: Enforce password-protected screensavers, set timeout limits, prevent user changes.
- **Benefits:** Centralized, consistent policy enforcement.

---

### Password Policies
- **Requirements:**
  - Minimum length (≥8 characters recommended).
  - Complexity (uppercase, lowercase, digits, symbols; evolving with MFA usage).
  - History & reuse prevention.
  - Expiration policies (NIST recommends avoiding forced changes if MFA is enabled).
  - Account lockout after repeated failed logins.
- **Self-service:** Automated password recovery to reduce helpdesk load.
- **Windows GPO Implementation:**
  - Minimum password length = 8
  - Password history = 8 previous passwords
  - Maximum password age = 90 days, minimum = 30 days
  - Password complexity = enabled

---

### Role Management
- **Roles simplify permissions management:**
  - Group permissions together and assign to multiple users.
  - Reduces need for shared generic accounts.
- **Windows Example:**
  - Create security groups for HR, Accounting.
  - Assign users to groups; permissions automatically inherited.
  - Folder access example: Assign “Human Resources” group full control to sensitive folders.

---

### Monitoring, Reporting, and Maintenance
- **Detect Inaccurate Permissions:**
  - Identify privilege creep (users retain old permissions after job changes).
  - Perform regular user account audits with management.
- **Detect Unauthorized Access:**
  - Continuous monitoring of account activity.
  - Watch for unusual logins: geographic anomalies, impossible travel, unusual hours, unusual file access.
- **Geolocation Tools:**
  - Geotagging: Log geographic location of logins.
  - Geofencing: Alerts when devices leave defined boundaries.
- **Account Types to Monitor:**
  - Standard user accounts
  - Administrator accounts
  - System/managed service accounts (follow least privilege, no interactive logins)

---

### Provisioning and Deprovisioning
- **Provisioning:** 
  - Create accounts for new users.
  - Grant authentication credentials and job-specific authorizations.
- **Deprovisioning:**
  - Remove access when users leave (resign, retire, or terminated).
  - Timely action prevents unauthorized access and mitigates risks.
- **Workflows:**
  - Routine: Triggered by HR notification; automated account expiration.
  - Emergency: Immediate termination coordination for adverse situations.
- **Windows Example:**
  - Disable account first (temporary safeguard).
  - Delete account or schedule future expiration for planned departures.
- **Benefit:** Ensures timely access revocation and reduces security risks.


## 13. Authorization

### Authorization Principles
- **Definition:** Determines what resources and privileges a user has after authentication.
- **Least Privilege:** Users get only the minimum permissions needed for their job.
  - Limits damage from insider attacks.
  - Restricts external attackers who compromise low-privilege accounts.
- **Separation of Duties:** Sensitive actions require at least two individuals.
  - Reduces fraud risk (e.g., vendor setup vs. issuing checks in accounting).
- **Privilege Creep:** Users accumulate permissions from previous roles, violating least privilege and separation of duties.
  - Regular manual or automated account reviews are essential to prevent this.

---

### Access Control Models

#### Mandatory Access Control (MAC)
- Most stringent model; enforced by the operating system.
- Users **cannot** change permissions.
- Access decisions based on labels:
  - Example: US government classifications (Top Secret > Secret > Confidential)
  - Users with higher clearance can access lower-classified documents.
- Common implementation: **SELinux** (Linux kernel module).

#### Discretionary Access Control (DAC)
- Resource owners can assign permissions to other users.
- Flexible, common in organizations.
- Example: NTFS file system on Windows allows owners to grant read, write, modify, or full control.
- Users with appropriate permissions can delegate access to others.

---

### Access Control Lists (ACLs)
- **Definition:** Table mapping users/groups to permissions for a resource.
- Common NTFS permissions:
  - **Full Control:** All actions.
  - **Modify:** Read, write, execute, delete.
  - **Read & Execute:** Read and run programs.
  - **Read:** View contents only.
  - **Write:** Create/add data.
- Example setup:
  - Alice (owner) → Full Control
  - Bob → Full Control
  - Carol → Read/Write
  - Tracy → Read only

---

### Advanced Authorization Concepts

#### Implicit Deny / Default Deny
- Anything not explicitly allowed is denied.
- Common example: Firewalls block requests unless a rule permits them.

#### Role-Based Access Control (RBAC)
- Permissions assigned to roles; users inherit permissions by role.
- Simplifies management when users join, leave, or need additional permissions.
- Example: Alice assigned "Accounting Clerk" and "Supervisor" roles → inherits all associated permissions.

#### Attribute-Based Access Control (ABAC)
- Policies defined based on user, object, and environment attributes.
- Supports conditional access:
  - Example: Manager can access salary info only after executive approval and only for their team.
- Can include **time** and **location** restrictions (e.g., only in office, during business hours).

#### Implementation Example: Time-Based Restrictions in Windows
- Active Directory → User Properties → Logon Hours
- Restrict access to specific days or hours (e.g., weekdays 8 AM–6 PM).
- Enhances security by preventing after-hours unauthorized actions.

