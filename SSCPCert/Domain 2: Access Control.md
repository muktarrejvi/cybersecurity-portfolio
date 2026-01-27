# SSCP Domain 2: Access Controls  
**Detailed Study Notes – 2025/2026 Preparation**  
(≈15–16% exam weight | Hands-on operational focus)

Domain 2 focuses on **implementing, maintaining, and supporting authentication, authorization, identity lifecycle, trust architectures, and access control models** in operational environments.

## 2.1 Implement and maintain authentication methods

### Single/Multi-Factor Authentication (MFA)
- **Single-factor** → Only one method (usually password = something you know). Weak against phishing, credential stuffing.
- **Multi-Factor Authentication (MFA)** → Two or more **independent** factors from different categories:
  1. Something you **know** → Password, PIN, security question (avoid questions — easily guessable/social-engineered)
  2. Something you **have** → Hardware token (YubiKey), soft token (Google Authenticator – TOTP), SMS (least secure – SIM swap risk), push notification
  3. Something you **are** → Biometrics (fingerprint, face, iris – must include liveness detection to prevent spoofs)
  4. Somewhere you **are** (emerging/contextual) → Geolocation, IP reputation

**Modern best practices (NIST SP 800-63B 2025-aligned)**:
- Prefer **phishing-resistant MFA** → FIDO2/WebAuthn passkeys, certificate-based, hardware security keys
- Avoid SMS/voice OTP if possible (NIST discourages)
- **Crossover Error Rate (CER)** for biometrics — balance FAR (false accept) vs FRR (false reject)
- Exam trap: Password + knowledge-based question = **NOT MFA** (same factor)

### Single Sign-On (SSO)
- One set of credentials → authenticated session reused across multiple systems/apps
- Reduces password fatigue & reuse → improves security & user experience
- Common implementations:
  - **Kerberos** (Windows AD native – ticket-based)
  - **Active Directory Federation Services (ADFS)** → SAML-based federation for enterprise SSO
  - **SAML 2.0** (enterprise/browser SSO)
  - **OAuth 2.0 + OpenID Connect (OIDC)** (web & mobile – most common today)

**SSO benefits & risks**:
- Benefits: Fewer passwords, centralized policy enforcement
- Risks: Single point of failure/compromise → use MFA + session monitoring

### Device Authentication
- Machines authenticate to each other (not just users)
- Methods:
  - **Certificate-based** (X.509) → Public key + CA-signed → strong (802.1X, VPN, SSH)
  - **SSH key pairs** → Public key on server, private key on client (never share private key)
  - **MAC address** → Easily spoofed → **NOT secure**
  - **TPM/Measured Boot** → Hardware root of trust (modern zero-trust)

### Federated Access
- Identity shared across organizations/domains without duplicating accounts
- Protocols:
  - **SAML 2.0** → XML-based assertions → IdP → SP (enterprise SSO)
  - **OAuth 2.0** → Authorization framework (scopes/tokens) → NOT authentication by itself
  - **OpenID Connect (OIDC)** → Authentication layer on OAuth → ID Token (JWT) with user claims

**Flow comparison**:

| Protocol | Primary Purpose     | Token Format | Common Use Case                  | Phishing Resistant? |
|----------|---------------------|--------------|----------------------------------|----------------------|
| SAML     | SSO / Federation    | XML Assertion| Enterprise apps (Office 365)     | Medium              |
| OAuth 2.0| Authorization       | Access Token | API access (Google APIs)         | Low (unless PKCE)   |
| OIDC     | Authentication      | ID Token (JWT)| Social login (Sign in with Google)| Medium-High         |

## 2.2 Support internetwork trust architectures

### Trust Relationships
- **One-way trust** → Domain A trusts Domain B (not vice versa) → common for resource domains
- **Two-way trust** → Mutual trust → bidirectional access
- **Transitive trust** → A trusts B, B trusts C → A trusts C automatically → risk of unintended access
- **Non-transitive** → Explicit trust required
- **Zero trust** → No implicit trust based on network location → verify every access (identity + device + context)

### Internet, Intranet, and Extranet
| Zone       | Trust Level | Access From          | Typical Controls                     | Example                     |
|------------|-------------|----------------------|--------------------------------------|-----------------------------|
| Internet   | None        | Anyone               | Firewall, WAF, DDoS protection       | Public website              |
| Intranet   | High        | Internal employees   | NAC, segmentation, EDR               | Internal file shares        |
| Extranet   | Controlled  | Partners/vendors     | VPN, federation, limited accounts    | Supplier portal             |

### Third-Party Connections
- Vendor portals, APIs, supply-chain integrations
- Risks: API abuse, compromised credentials
- Controls:
  - OAuth/OIDC for delegated access
  - API gateways + rate limiting + auth
  - Vendor risk assessments + SLAs
  - Continuous monitoring (CASB, UEBA)

## 2.3 Participate in the identity management lifecycle

### Proofing (Identity Proofing)
- Verify real-world identity before issuing credentials
- NIST IAL levels:
  - IAL1 → Self-asserted (low assurance)
  - IAL2 → Remote + document + selfie (most enterprise)
  - IAL3 → In-person + biometrics (high-security/gov)

### Provisioning / De-provisioning
- **Provisioning** → Create account + assign roles/entitlements (onboarding)
- **De-provisioning** → Disable/delete account (offboarding/termination)
- Best practice: Automate via HR system integration → immediate disable on termination
- Emergency de-provisioning → Disable first (reversible), then delete

### Maintenance
- Periodic recertification → Managers review entitlements
- Detect privilege creep → Accumulating old permissions
- Disable dormant accounts → After 90–180 days inactivity

### Entitlement
- Permissions/rights tied to role/job function
- Enforce **least privilege** + **separation of duties**

### IAM Systems
- Centralized stores: Active Directory, LDAP, Okta, Azure AD/Entra ID
- Modern: Cloud IAM, SCIM for provisioning, JIT access

## 2.4 Understand and apply access controls

### Mandatory Access Control (MAC)
- OS enforces based on labels (security clearance vs classification)
- Example: SELinux, labeled security (Top Secret, Secret, Confidential)
- Strongest confidentiality → no user override

### Discretionary Access Control (DAC)
- Owner controls permissions
- Example: NTFS ACLs, Unix chmod
- Flexible → but risk of over-sharing

### Role-Based Access Control (RBAC)
- Permissions tied to roles → users assigned roles
- Example: AD Security Groups (HR Clerk, Accounting Supervisor)
- Simplifies management → avoids generic accounts

### Attribute-Based Access Control (ABAC)
- Dynamic policies based on attributes (user, resource, environment)
- Example: “Allow access if user.department = Finance AND time between 9-5 AND location = office”
- Most flexible → used in modern zero-trust & cloud IAM

### Rule-Based Access Control
- Central rules (e.g., firewall ACLs, time-of-day restrictions)

**Comparison Table – Access Models**

| Model    | Who Controls?       | Flexibility | Strength                  | Weakness                     | Typical Use Case            |
|----------|---------------------|-------------|---------------------------|------------------------------|-----------------------------|
| MAC      | OS / Labels         | Low         | Highest security          | Rigid, complex               | Classified gov systems      |
| DAC      | Resource owner      | High        | User-friendly             | Owner can misconfigure       | File shares, Windows NTFS   |
| RBAC     | Admin via roles     | Medium      | Scalable, auditable       | Role explosion               | Enterprise AD environments  |
| ABAC     | Policies + attrs    | Very high   | Contextual, dynamic       | Complex policy writing       | Cloud IAM, zero trust       |

**Key Principles (Exam Favorites)**
- **Least Privilege** → Minimum rights needed
- **Need-to-Know** → Even if cleared, only access required data
- **Separation of Duties** → No single person can complete sensitive transaction
- **Implicit Deny** → Default = block unless explicitly allowed

**Exam Tips**
- Know differences: Identification (claim) vs Authentication (prove) vs Authorization (permissions)
- MFA must use **different factors**
- Zero Trust = verify identity/context — **not** network location
- SAML = enterprise federation; OIDC = modern web/social login
- Privilege creep → regular recertification required

Good luck with your SSCP exam preparation!  
Revise with official ISC2 practice tests + Sybex SSCP Study Guide (3rd ed. or later).
