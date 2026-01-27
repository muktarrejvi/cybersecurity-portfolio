# Domain 2: Access Controls  
**SSCP (Systems Security Certified Practitioner) – 15% of exam**

## 1. Overview of Access Controls Domain
- Core goal: Ensure only authorized entities can access resources while preventing unauthorized access.
- Key activities: Implement/maintain authentication, support access management lifecycle, administer access control systems, understand internet trust architectures.
- AAA framework: **Authentication** + **Authorization** + **Accounting** (tracking/logging).

## 2. Core Identity & Access Management Concepts

### Entity vs Identity vs Attributes
- **Entity**: Actual person, device, group, server, business unit, etc.
- **Identity**: Role/context an entity uses (e.g., Bob = staff + alumnus + student).
- **Attributes**: Descriptive data tied to an identity (major = Computer Science, graduation year = 2015, donor = Yes).

### Identification vs Authentication vs Authorization
| Step              | Action                              | Example (physical)          | Example (digital)          | Nature          |
|-------------------|-------------------------------------|-----------------------------|----------------------------|-----------------|
| **Identification** | Claim identity                      | “I’m Mike Chapple”          | Username                   | Assertion       |
| **Authentication** | Prove the claim                     | Show driver’s license       | Password, biometrics, token| Proof           |
| **Authorization**  | Determine allowed actions/rights    | Check appointment list      | ACL / RBAC check           | Permission grant|

- **Accounting** → Logging user activity for audit/reconstruction.

## 3. Identification Mechanisms

### Usernames
- Used only for **identification** (not secret).
- Common formats: first initial + last name (mchapple), or with numbers if duplicate.

### Access / Identity Cards
| Type                  | Technology                  | Security Level | Examples                          | Notes                                      |
|-----------------------|-----------------------------|----------------|-----------------------------------|--------------------------------------------|
| Magnetic stripe       | Magnetic stripe             | Low            | Old hotel keys, some ID cards     | Easily cloned/duplicated                   |
| Contact Smart Card    | Embedded chip (contact)     | High           | DoD CAC, chip & PIN credit cards  | Insert into reader                         |
| Contactless / Proximity (Passive) | RFID / NFC – powered by reader | Medium-High   | Many corporate badges             | Very close range, no battery               |
| Contactless (Active)  | Battery + transmitter       | Medium         | Toll transponders (E-ZPass)       | Longer range, battery needs replacement    |

## 4. Registration & Identity Proofing
Four-step process (separation of duties is critical):

1. Request creation of new entity
2. Approve request (different person)
3. Identity proofing (HR / registration authority)
4. Issue credentials (separate issuer)

**Identity Proofing techniques** (NIST guidance):
- Two forms of government-issued photo ID
- Fingerprints (government/high-security)
- Background checks (at least criminal)

## 5. Authentication Factors & Errors

### Three Classic Factors
1. **Something you know**     → Password, passphrase, PIN, password key
2. **Something you are**      → Biometrics (fingerprint, face, iris, voice)
3. **Something you have**     → Token, smart card, smartphone (soft token)

### Error Rates
- **FAR** (False Acceptance Rate) → Unauthorized user accepted (dangerous)
- **FRR** (False Rejection Rate) → Authorized user rejected (inconvenient)
- **Crossover Error Rate (CER)** → Point where FAR = FRR → balanced measure of strength

## 6. Multifactor Authentication (MFA)
- Must use **different factors** (password + token = MFA).
- **Not MFA**: password + security question (both “something you know”).

## 7. Something You Have – Common Implementations

| Method          | Technology                  | Protocol | Notes                                      |
|-----------------|-----------------------------|----------|--------------------------------------------|
| Hardware token  | Key fob                     | HOTP / TOTP | Physical device, expensive to scale        |
| Soft token      | Smartphone app              | TOTP     | Google Authenticator, Microsoft Authenticator |
| Smart Card      | Embedded chip               | —        | DoD CAC, PIV cards                         |

- **HOTP**: event-based (counter), code valid until used
- **TOTP**: time-based (30-second windows), needs clock sync

## 8. Password Authentication Protocols (Remote Access)

| Protocol   | Encryption? | Security Status     | Notes                                      |
|------------|-------------|----------------------|--------------------------------------------|
| PAP        | No          | Insecure             | Sends password in clear text               |
| CHAP       | Challenge-response | Secure (legacy) | Uses hash, no password sent                |
| MS-CHAP    | —           | Broken               | Microsoft version – avoid                      |
| MS-CHAPv2  | —           | Broken               | Improved but still cracked                 |

## 9. SSO & Federation

- **Federation** → Sharing identity info across organizations (Google, Facebook login on other sites).
- **Single Sign-On (SSO)** → One login → session persists across systems (often within one org).
- Common implementations:
  - Active Directory + ADFS (Microsoft)
  - Shibboleth (higher education)
- Trust types:
  - One-way vs two-way
  - Transitive vs non-transitive

## 10. Internetwork Trust Architectures

| Zone         | Trust Level | Typical Use                              | Firewall Rules                     |
|--------------|-------------|------------------------------------------|------------------------------------|
| Internet     | Untrusted   | External world                           | Allow outbound, restrict inbound   |
| Intranet     | Trusted     | Internal employee systems                | High trust                         |
| DMZ          | Semi-trusted| Public-facing servers (web, mail, DNS)   | Limited inbound from Internet      |
| Extranet     | Controlled  | Business partners, vendors (VPN access)  | Strict authentication & authorization |

## 11. Zero Trust Architecture
- **Core principle**: Trust **individuals/devices**, **not** the network/location.
- Key technologies:
  - Strong IAM
  - Continuous monitoring (SIEM + SOAR)
  - CASB (Cloud Access Security Broker)
  - EDR (Endpoint Detection & Response)

## 12. Web SSO Protocols

| Protocol          | Purpose          | Main Actors                     | Key Benefit                              |
|-------------------|------------------|----------------------------------|------------------------------------------|
| **SAML**          | SSO (browser)    | Principal, IdP, SP               | True SSO, password never shared          |
| **OAuth 2.0**     | Authorization    | Client, Resource Owner, Auth Server | Grants limited access (not authentication) |
| **OpenID Connect**| Authentication   | Built on OAuth                   | Adds identity layer to OAuth             |

## 13. Device Authentication
- **SSH key-based**: Public-private key pair (private key never shared).
- **Certificate-based**: Public key signed by CA → higher assurance.
- **MAC address**: Easily spoofed → **not secure** for authentication.

## 14. Account & Privilege Management Principles

- **Least Privilege** → Minimum permissions needed for job.
- **Separation of Duties** → Sensitive tasks require 2+ people.
- **Job Rotation** + **Mandatory Vacation** → Deter fraud.
- **Privilege Creep** → Accumulating old permissions → regular recertification needed.

## 15. Password Policies (Modern NIST Guidance vs Legacy)

| Setting                  | Legacy Common Practice       | Current NIST Recommendation (SP 800-63B) |
|--------------------------|-------------------------------|-------------------------------------------|
| Minimum length           | 8–12 characters              | 8+ (user chosen) or 64+ (system gen)     |
| Complexity               | Upper/lower/digit/symbol     | Not required if MFA in place             |
| Expiration               | 90 days                      | Never force periodic changes             |
| Password history         | Remember last 8–24           | Not strongly recommended                 |
| Account lockout          | After 5–10 failed attempts   | Still useful                             |

## 16. Authorization Models

| Model     | Control By          | Flexibility | Example Use Case                     | Typical Implementation |
|-----------|---------------------|-------------|--------------------------------------|------------------------|
| **MAC**   | OS / labels         | Very low    | Classified gov systems               | SELinux                |
| **DAC**   | Resource owner      | High        | File shares, NTFS                    | Windows NTFS ACLs      |
| **RBAC**  | Roles               | Medium      | Job-based permissions                | AD Security Groups     |
| **ABAC**  | Attributes + rules  | Very high   | Conditional / contextual access      | Modern cloud IAM       |

- **Implicit Deny** / **Default Deny** → Anything not explicitly allowed is blocked.

## 17. Monitoring, Reporting & Maintenance

- **Privilege creep** detection → Regular access reviews / attestations.
- **Continuous monitoring** flags:
  - Impossible travel
  - Unusual time / location
  - Abnormal file access patterns
- **Geotagging** & **Geofencing** → Useful for anomaly detection.
- **Service / system accounts** → No interactive login, least privilege.

## 18. Provisioning & Deprovisioning
- **Onboarding**: Create account + assign entitlements.
- **Offboarding**:
  - Planned → Schedule expiration
  - Emergency/termination → Immediate disable → later delete
- Best practice: Disable first (reversible), then delete.

---

**Quick Exam Reminders**
- Know difference: Identification vs Authentication
- MFA requires **different factors**
- PAP = insecure, CHAP = better, MS-CHAPv2 = broken
- Least Privilege ≠ Separation of Duties
- Implicit Deny is foundational
- Zero Trust = trust identity, not network

Good luck with your SSCP preparation!
