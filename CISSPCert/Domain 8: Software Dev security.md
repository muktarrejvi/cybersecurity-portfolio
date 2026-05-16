# CISSP Domain 8: Software Development Security
> A comprehensive deep-dive into all subdomains with subcategories and real-world examples.

---

## Table of Contents
- [8.1 Understand and Integrate Security into the SDLC](#81-understand-and-integrate-security-into-the-sdlc)
- [8.2 Identify and Apply Security Controls in Software Development Ecosystems](#82-identify-and-apply-security-controls-in-software-development-ecosystems)
- [8.3 Assess the Effectiveness of Software Security](#83-assess-the-effectiveness-of-software-security)
- [8.4 Assess Security Impact of Acquired Software](#84-assess-security-impact-of-acquired-software)
- [8.5 Define and Apply Secure Coding Guidelines and Standards](#85-define-and-apply-secure-coding-guidelines-and-standards)

---

## 8.1 Understand and Integrate Security into the SDLC

The Software Development Life Cycle (SDLC) is a structured process for planning, creating, testing, and delivering software. Integrating security at **every phase** — rather than bolting it on at the end — is the foundation of secure software development.

> **Key Principle:** Security should be a design requirement, not an afterthought.

---

### 8.1.1 SDLC Models

Different development models handle security integration differently.

#### Waterfall Model
A sequential, linear approach where each phase must be completed before the next begins.

| Phase | Security Activity |
|---|---|
| Requirements | Define security requirements |
| Design | Threat modelling |
| Implementation | Secure coding standards |
| Testing | Penetration testing, code review |
| Maintenance | Patch management |

**Example:** A bank building a core banking system uses Waterfall because requirements are well-defined and changes are costly. Security reviews happen at each gate before the next phase begins.

**Risk:** Security flaws discovered late (in testing) are expensive to fix — the later the discovery, the higher the cost.

---

#### Agile Model
Iterative, sprint-based development with continuous delivery. Security must be embedded into every sprint.

- **Scrum** — sprints of 2–4 weeks; security stories added to the backlog
- **Kanban** — continuous flow; security tasks treated as first-class work items

**Example:** A SaaS startup building a web app uses Agile. Each sprint includes a security story such as "Implement input validation on the registration form." Security is never deferred to the end.

---

#### DevSecOps
An extension of DevOps that integrates security as a **shared responsibility** throughout the pipeline.

```
Plan → Code → Build → Test → Release → Deploy → Operate → Monitor
  ↑                                                            ↓
  └──────────────── Security at every stage ──────────────────┘
```

**Key tools in DevSecOps:**
- **SAST** (Static Application Security Testing) — scans code before it runs (e.g., SonarQube, Checkmarx)
- **DAST** (Dynamic Application Security Testing) — tests running applications (e.g., OWASP ZAP, Burp Suite)
- **SCA** (Software Composition Analysis) — checks third-party libraries (e.g., Snyk, Black Duck)
- **IaC scanning** — checks infrastructure code for misconfigurations (e.g., Checkov, tfsec)

**Example:** A DevSecOps pipeline at a fintech company automatically runs SAST on every pull request. A developer submits code with a SQL injection vulnerability — the pipeline flags it before it ever reaches code review.

---

#### Spiral Model
Risk-driven model combining Waterfall and prototyping. Each loop = a risk assessment cycle.

**Security focus:** Risk analysis is built into every spiral iteration.

**Example:** NASA uses spiral development for mission-critical software — each iteration assesses security and safety risks before committing to the next phase.

---

#### RAD (Rapid Application Development)
Prioritises speed and user feedback over heavy planning. Security risk: corners may be cut.

**Mitigation:** Enforce security gates and mandatory code reviews before release.

---

### 8.1.2 Security in Each SDLC Phase

#### Phase 1: Requirements
- Define **security requirements** alongside functional requirements
- Identify regulatory obligations (GDPR, HIPAA, PCI-DSS)
- Establish misuse cases (not just use cases)

**Example:** A healthcare app must store patient data. Security requirement: "All PII must be encrypted at rest using AES-256." This is defined here, not discovered in testing.

---

#### Phase 2: Design
- **Threat Modelling** — identify potential threats early
  - **STRIDE** (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege)
  - **DREAD** (Damage, Reproducibility, Exploitability, Affected Users, Discoverability)
  - **PASTA** (Process for Attack Simulation and Threat Analysis)
- Apply **secure design principles** (least privilege, defence in depth, fail-safe defaults)
- Design authentication and authorisation architecture

**Example:** Using STRIDE on a login module, the team identifies "Spoofing" as a risk. They design multi-factor authentication (MFA) into the system before a single line of code is written.

---

#### Phase 3: Implementation (Coding)
- Follow **secure coding standards** (OWASP, CERT, SANS)
- Use approved, vetted libraries
- Avoid dangerous functions (e.g., `strcpy` in C, which enables buffer overflows)
- Peer code reviews with a security focus

**Example:** A developer uses parameterised queries instead of string concatenation for database calls, preventing SQL injection.

---

#### Phase 4: Testing
- **Unit testing** — tests individual components
- **Integration testing** — tests how components interact
- **Regression testing** — ensures new code doesn't break existing security controls
- **Security-specific testing** — SAST, DAST, fuzzing, pen testing

**Example:** After adding a new API endpoint, the team runs DAST and discovers an authentication bypass. It's caught before release.

---

#### Phase 5: Deployment / Release
- Use **change management** processes
- Verify code integrity (code signing, checksums)
- Harden deployment environments
- Conduct final security sign-off

**Example:** Before deploying to production, the security team verifies that no debug features are enabled, all secrets are stored in a vault (not hardcoded), and TLS 1.2+ is enforced.

---

#### Phase 6: Maintenance & Operations
- **Patch management** — apply security patches promptly
- **Vulnerability disclosure** — process for handling reported bugs
- Monitor for new threats against existing software
- Plan for **end-of-life (EOL)** — software with no vendor support = unpatched vulnerabilities

**Example:** Log4Shell (2021) — organisations running Apache Log4j had to immediately patch or mitigate. Those with good patch management processes responded in hours; others took weeks and were exploited.

---

### 8.1.3 Maturity Models

#### CMMI (Capability Maturity Model Integration)
Measures how mature an organisation's software development processes are.

| Level | Name | Description |
|---|---|---|
| 1 | Initial | Chaotic, ad hoc, unpredictable |
| 2 | Managed | Basic project management in place |
| 3 | Defined | Standardised processes across org |
| 4 | Quantitatively Managed | Metrics-driven management |
| 5 | Optimising | Continuous improvement focus |

**Example:** A Level 1 org has no consistent security testing. A Level 5 org tracks defect escape rates and continuously improves its secure SDLC.

---

#### SAMM (Software Assurance Maturity Model) — OWASP
Specifically focused on security maturity in software development. Covers:
- Governance
- Design
- Implementation
- Verification
- Operations

---

## 8.2 Identify and Apply Security Controls in Software Development Ecosystems

The development ecosystem includes all the tools, environments, people, and processes involved in building software. Each element is a potential attack surface.

---

### 8.2.1 Development Environments

#### IDE Security (Integrated Development Environment)
IDEs like Visual Studio Code, IntelliJ, and Eclipse are common entry points for supply chain attacks.

**Risks:**
- Malicious plugins/extensions
- Hardcoded secrets in local config files
- Auto-complete suggesting insecure code patterns

**Controls:**
- Approved plugin lists
- Secret scanning tools (e.g., GitGuardian, truffleHog)
- Developer security training

**Example:** A developer installs a VS Code extension from an untrusted source. The extension exfiltrates environment variables (including AWS keys) to an attacker's server.

---

#### Source Code Repositories
Platforms: GitHub, GitLab, Bitbucket, Azure DevOps

**Security controls:**
- **Branch protection rules** — prevent direct pushes to main/master
- **Signed commits** — verify developer identity (GPG keys)
- **Secret scanning** — automatically detect API keys, passwords committed to repos
- **Access control** — least privilege; developers only access repos they need
- **Audit logging** — track who changed what and when

**Example:** A developer accidentally commits an AWS secret key to a public GitHub repo. GitHub's secret scanning detects it and alerts within seconds. AWS automatically invalidates the key.

---

#### CI/CD Pipeline Security
Continuous Integration / Continuous Delivery pipelines automate building, testing, and deploying code.

**Attack surface:**
- Compromised build servers
- Malicious dependencies injected mid-pipeline
- Insecure pipeline configuration (overly permissive service accounts)

**Controls:**
- Sign build artifacts
- Use ephemeral (disposable) build environments
- Scan dependencies at build time (SCA)
- Limit pipeline permissions using least privilege

**Famous example:** **SolarWinds attack (2020)** — attackers compromised the build pipeline and injected malicious code into the Orion software update. This is a supply chain attack via the CI/CD pipeline.

---

### 8.2.2 Software Libraries and Dependencies

#### Third-Party Libraries
Modern software relies heavily on open-source libraries. Each library is a potential vulnerability.

**Risks:**
- Known vulnerabilities in outdated libraries (CVEs)
- Typosquatting — fake packages with similar names (e.g., `colourama` vs `colorama`)
- Dependency confusion attacks — injecting malicious packages into private feeds

**Controls:**
- **SCA tools** — Snyk, OWASP Dependency-Check, Black Duck
- **Software Bill of Materials (SBOM)** — a complete inventory of all components
- Pin dependency versions (don't use wildcards like `>=1.0`)
- Regularly audit and update dependencies

**Example:** The **event-stream npm package** incident (2018) — a popular npm package was handed over to a malicious actor who injected code to steal Bitcoin wallet credentials. Millions of projects were affected.

---

#### SBOM (Software Bill of Materials)
An SBOM is a formal, machine-readable inventory of all software components in an application.

Think of it like **nutritional information on food packaging** — but for software.

**Why it matters:**
- When a vulnerability like Log4Shell is discovered, organisations with an SBOM can immediately identify which applications are affected
- US Executive Order 14028 (2021) now requires SBOMs for software sold to the US federal government

---

### 8.2.3 APIs and Web Services Security

#### API Security Controls
- **Authentication** — OAuth 2.0, API keys, JWT tokens
- **Authorisation** — ensure users can only access their own data (IDOR prevention)
- **Rate limiting** — prevent abuse and DoS attacks
- **Input validation** — validate all API inputs, even from trusted sources
- **TLS enforcement** — all API traffic over HTTPS

**Example:** An e-commerce API has an endpoint `/api/orders/{id}`. Without proper authorisation checks, a user can change the `id` parameter to view another customer's order. This is an **Insecure Direct Object Reference (IDOR)** — a top OWASP API vulnerability.

---

#### OWASP API Security Top 10
Key risks to know:
1. Broken Object Level Authorisation (IDOR)
2. Broken Authentication
3. Broken Object Property Level Authorisation
4. Unrestricted Resource Consumption
5. Broken Function Level Authorisation
6. Unrestricted Access to Sensitive Business Flows
7. Server Side Request Forgery (SSRF)
8. Security Misconfiguration
9. Improper Inventory Management
10. Unsafe Consumption of APIs

---

### 8.2.4 Database Security Controls

- **Parameterised queries / prepared statements** — prevent SQL injection
- **Stored procedures** — limit direct SQL execution
- **Least privilege** — app DB user should only have the permissions it needs (no `DROP TABLE` rights)
- **Encryption** — encrypt sensitive columns; use TDE (Transparent Data Encryption) for the whole DB
- **Database activity monitoring (DAM)** — log and alert on suspicious queries

**Example:** An application connects to its database with a superuser account. When an attacker exploits a SQL injection flaw, they gain full control of the database server — including the ability to read all data and run OS commands.

---

## 8.3 Assess the Effectiveness of Software Security

Testing and assessing software security is not a one-time event — it's a continuous process.

---

### 8.3.1 Static Application Security Testing (SAST)

Analyses **source code, bytecode, or binaries** without executing the application. Also called "white-box testing."

**How it works:** Scans code for patterns matching known vulnerability signatures.

**Tools:** SonarQube, Checkmarx, Veracode, Semgrep, Fortify

**Pros:**
- Catches issues early (shift left)
- Can scan 100% of the codebase
- No running environment needed

**Cons:**
- High false-positive rate
- Can't detect runtime/logic flaws
- Language-specific tools needed

**Example:** SAST scans a Java application and flags a line using `Runtime.exec()` with user-controlled input — a potential OS command injection.

---

### 8.3.2 Dynamic Application Security Testing (DAST)

Tests the **running application** from the outside, like an attacker would. Also called "black-box testing."

**How it works:** Sends crafted inputs to the app and analyses responses for vulnerabilities.

**Tools:** OWASP ZAP, Burp Suite, Nikto, Acunetix

**Pros:**
- Finds runtime vulnerabilities
- Language-agnostic
- Closer to real attacker perspective

**Cons:**
- Can't see inside the code
- May miss issues in untested code paths
- Can cause issues in production environments

**Example:** DAST sends SQL injection payloads to a login form and receives a database error in the response — confirming the vulnerability.

---

### 8.3.3 Interactive Application Security Testing (IAST)

Combines SAST and DAST — instruments the application with **sensors/agents** that monitor it from the inside while it runs.

**Tools:** Contrast Security, Seeker, HCL AppScan

**Pros:**
- Low false positives
- Real-time feedback
- Sees both code and runtime behaviour

**Cons:**
- Requires agent deployment
- Language-specific agents

---

### 8.3.4 Penetration Testing

A **simulated attack** by skilled testers (ethical hackers) to identify exploitable vulnerabilities.

#### Types:
| Type | Knowledge Level | Description |
|---|---|---|
| Black Box | None | Tester has no prior knowledge — simulates external attacker |
| White Box | Full | Tester has full access to code, architecture, credentials |
| Grey Box | Partial | Tester has some knowledge — simulates insider or privileged attacker |

#### Phases of a Pen Test:
1. **Reconnaissance** — gather information (passive/active)
2. **Scanning** — identify open ports, services, vulnerabilities
3. **Exploitation** — attempt to exploit vulnerabilities
4. **Post-exploitation** — assess impact, pivot, escalate privileges
5. **Reporting** — document findings with risk ratings and remediation advice

**Example:** A grey-box pen test on a banking app reveals that session tokens are predictable. An attacker could hijack another user's session without knowing their credentials.

---

### 8.3.5 Fuzz Testing (Fuzzing)

Sends **random, malformed, or unexpected inputs** to an application to find crashes and unexpected behaviour.

**Types:**
- **Dumb fuzzing** — random data, no knowledge of format
- **Smart/mutation fuzzing** — mutates valid inputs based on protocol knowledge
- **Coverage-guided fuzzing** — uses code coverage feedback to guide input generation (e.g., AFL, libFuzzer)

**Example:** Google's **Project Zero** uses fuzzing extensively. Fuzzing Chrome's JavaScript engine has discovered hundreds of serious vulnerabilities.

---

### 8.3.6 Code Review

Manual or automated examination of source code by security-aware reviewers.

**Types:**
- **Peer review** — developer reviews another developer's code
- **Security-focused review** — security engineer reviews for specific vulnerability classes
- **Formal inspection (Fagan inspection)** — structured, multi-stage review process

**Example:** During a code review, a reviewer notices that password reset tokens are not expired after use — a logic flaw that automated tools would miss.

---

### 8.3.7 Security Regression Testing

Ensures that **previously fixed vulnerabilities** don't re-appear in new releases.

**Example:** A SQL injection bug was fixed in version 2.1. Security regression tests include specific payloads targeting that exact flaw — ensuring it doesn't resurface in version 2.2.

---

## 8.4 Assess Security Impact of Acquired Software

Not all software is built in-house. Organisations regularly purchase, license, or use open-source software. Each acquisition carries security risk.

---

### 8.4.1 Commercial Off-the-Shelf (COTS) Software

Pre-built software purchased from a vendor (e.g., Microsoft Office, SAP, Salesforce).

**Security concerns:**
- You can't see or modify the source code
- Dependent on vendor for patches
- May have undisclosed vulnerabilities or backdoors
- Licensing issues affecting security updates

**Controls:**
- Vendor security assessments before procurement
- Review CVE databases for known vulnerabilities
- Ensure vendor has a published vulnerability disclosure/patch process
- Monitor for security bulletins and apply patches promptly

**Example:** An organisation deploys an unpatched version of Microsoft Exchange Server. Attackers exploit a known vulnerability (like ProxyLogon) to gain access to internal emails.

---

### 8.4.2 Open-Source Software (OSS)

Freely available software with publicly accessible source code.

**Pros:** Transparency, community scrutiny, free
**Cons:** May be poorly maintained, no formal support, supply chain risks

**Security assessment:**
- Check project activity (last commit date, number of maintainers)
- Review issue tracker for unresolved security bugs
- Use SCA tools to check for known CVEs
- Review the licence for compliance obligations
- Generate an SBOM to track all OSS components

**Example:** An organisation uses an unmaintained npm package with 3 known CVEs. Because no patches will be released, they must fork and patch it themselves or replace it.

---

### 8.4.3 Third-Party / Vendor-Developed Software

Custom software built by an external vendor on behalf of the organisation.

**Controls:**
- Include **security requirements in contracts** (SLAs, patch timelines)
- Require **source code escrow** — if the vendor goes out of business, you get the source code
- Conduct **security acceptance testing** before deployment
- Require vendors to follow your secure coding standards
- Right-to-audit clauses

**Example:** A company commissions a vendor to build a customer portal. The contract includes a clause requiring OWASP Top 10 compliance and the right to conduct penetration testing before go-live.

---

### 8.4.4 Supply Chain Risk Management

The software supply chain includes all the people, processes, and technology involved in delivering software.

**Key risks:**
- Compromised vendor (SolarWinds-style attack)
- Malicious insiders at vendor organisations
- Counterfeit or tampered software components

**Controls:**
- **Vendor risk assessments** — security questionnaires, certifications (ISO 27001, SOC 2)
- **Software provenance verification** — code signing, checksums, SBOMs
- **Zero-trust approach to third-party software** — don't automatically trust vendor-supplied updates
- **NIST SP 800-161** — supply chain risk management guidance

---

### 8.4.5 Cloud-Based / SaaS Software

Software delivered over the internet (e.g., Google Workspace, Slack, Salesforce).

**Shared responsibility model:** The vendor secures the platform; the customer secures their data and configuration.

**Security considerations:**
- Data residency and sovereignty (where is data stored?)
- Access controls and identity management (SSO, MFA)
- API security between SaaS apps
- Data loss prevention (DLP)
- Right to audit / compliance certifications (SOC 2, ISO 27001, FedRAMP)

**Example:** An organisation uses a SaaS HR platform. They must ensure SSO is configured, MFA is enforced, and that the vendor holds a SOC 2 Type II report confirming their security controls.

---

## 8.5 Define and Apply Secure Coding Guidelines and Standards

Secure coding is the practice of writing software in a way that guards against security vulnerabilities being unintentionally introduced.

---

### 8.5.1 OWASP Top 10

The most critical web application security risks, updated regularly by the Open Web Application Security Project.

**Current OWASP Top 10 (2021):**

| # | Vulnerability | Example |
|---|---|---|
| A01 | Broken Access Control | User accesses admin panel without admin rights |
| A02 | Cryptographic Failures | Storing passwords in plaintext |
| A03 | Injection | SQL injection, command injection |
| A04 | Insecure Design | No rate limiting on login (no lockout after failed attempts) |
| A05 | Security Misconfiguration | Default admin credentials left unchanged |
| A06 | Vulnerable & Outdated Components | Using a library with known CVEs |
| A07 | Identification & Authentication Failures | Weak session tokens, no MFA |
| A08 | Software & Data Integrity Failures | CI/CD pipeline not verifying update signatures |
| A09 | Security Logging & Monitoring Failures | No alerting on failed login attempts |
| A10 | Server-Side Request Forgery (SSRF) | App fetches attacker-controlled URL, accessing internal services |

---

### 8.5.2 Injection Attacks & Prevention

#### SQL Injection
Attacker injects SQL code into an input field to manipulate the database query.

**Vulnerable code (Python):**
```python
query = "SELECT * FROM users WHERE username = '" + username + "'"
```

**Attack input:** `' OR '1'='1` → returns all users

**Secure code (parameterised query):**
```python
query = "SELECT * FROM users WHERE username = %s"
cursor.execute(query, (username,))
```

#### Command Injection
Attacker injects OS commands through application input.

**Vulnerable code:**
```python
os.system("ping " + user_input)
```

**Attack:** `user_input = "google.com; rm -rf /"`

**Prevention:** Never pass user input to OS commands. Use safe APIs.

#### Other injection types:
- **LDAP injection** — manipulates LDAP queries
- **XML/XPath injection** — manipulates XML/XPath queries
- **NoSQL injection** — targets MongoDB, CouchDB, etc.

---

### 8.5.3 Cross-Site Scripting (XSS)

Attacker injects malicious scripts into content viewed by other users.

**Types:**
- **Reflected XSS** — script is in the URL, reflected back in the response
- **Stored XSS** — script is stored in the database and served to all users
- **DOM-based XSS** — script executes via client-side JavaScript

**Example attack:** A stored XSS payload in a comment field steals session cookies from every user who views the comment.

**Prevention:**
- Encode all output (HTML entity encoding)
- Use Content Security Policy (CSP) headers
- Validate and sanitise input
- Use frameworks that auto-escape output (React, Angular)

---

### 8.5.4 Authentication & Session Management

**Common flaws:**
- Weak passwords allowed
- No account lockout after failed attempts
- Session tokens in URLs (logged in server logs)
- Sessions not invalidated on logout
- Predictable session token values

**Secure practices:**
- Enforce strong password policies
- Implement MFA
- Use cryptographically random session tokens (at least 128 bits)
- Set `Secure`, `HttpOnly`, and `SameSite` flags on cookies
- Invalidate sessions on logout and after timeout
- Re-authenticate before sensitive operations (password change, payment)

---

### 8.5.5 Cryptography in Code

**Common mistakes:**
- Using MD5 or SHA-1 for password hashing (broken — use bcrypt, Argon2, or scrypt)
- Hardcoding encryption keys in source code
- Using ECB mode for block ciphers (reveals patterns in plaintext)
- Generating weak random numbers using `rand()` instead of a CSPRNG

**Best practices:**
- Use well-established, maintained cryptographic libraries (don't roll your own crypto)
- Use AES-256 for symmetric encryption
- Use RSA-2048+ or ECC for asymmetric encryption
- Store secrets in a secrets manager (HashiCorp Vault, AWS Secrets Manager)
- Use TLS 1.2 or 1.3 for all communications

**Example:** A developer uses `Math.random()` in JavaScript to generate password reset tokens. `Math.random()` is not cryptographically secure — an attacker can predict token values. Fix: use `crypto.getRandomValues()`.

---

### 8.5.6 Error Handling & Logging

#### Insecure Error Handling
Detailed error messages reveal system internals to attackers.

**Example:** A stack trace returned to the user reveals the database type, table names, and server paths — a goldmine for attackers.

**Secure practice:**
- Display generic error messages to users ("An error occurred. Please try again.")
- Log detailed errors server-side in a secure log
- Never log sensitive data (passwords, credit card numbers, tokens)

#### Secure Logging
Logs should capture:
- Authentication events (success and failure)
- Authorisation failures
- Input validation failures
- Admin actions
- System errors

**Log protection:**
- Store logs on a separate, hardened server
- Implement log integrity controls (WORM storage, signing)
- Alert on suspicious patterns (many failed logins, data exfiltration volumes)

---

### 8.5.7 Secure Design Principles

#### Least Privilege
Every component, user, and process should have only the minimum access needed.

**Example:** A web application's database account has only `SELECT`, `INSERT`, and `UPDATE` rights — not `DROP TABLE` or `GRANT`.

#### Defence in Depth
Multiple layers of security so that if one fails, others compensate.

**Example:** An attacker bypasses the WAF but is stopped by input validation in the application layer, then stopped again by parameterised queries at the database layer.

#### Fail-Safe Defaults
Default to denying access. Access must be explicitly granted.

**Example:** A new user account has no permissions by default. Administrators must explicitly grant access to each resource.

#### Separation of Duties (SoD)
No single person should be able to complete a critical action alone.

**Example:** A developer cannot both write code and approve it for deployment to production.

#### Open Design
Security should not rely on secrecy of the design (security through obscurity is not a valid control).

**Example:** Encryption algorithms (AES, RSA) are publicly known but secure because the security depends on the key, not the algorithm.

#### Economy of Mechanism
Keep security mechanisms as simple as possible. Complexity breeds vulnerability.

#### Complete Mediation
Every access to every resource must be checked — don't cache access decisions.

---

### 8.5.8 Memory Management and Buffer Overflows

A **buffer overflow** occurs when a program writes more data to a buffer than it can hold, overwriting adjacent memory.

**Consequence:** Arbitrary code execution, system crashes, privilege escalation.

**Vulnerable code (C):**
```c
char buffer[10];
strcpy(buffer, user_input); // No bounds checking!
```

**Prevention:**
- Use memory-safe languages (Rust, Go, Java, Python) where possible
- In C/C++: use safe functions (`strncpy`, `strncat`) with bounds checking
- Enable compiler protections: stack canaries, ASLR, DEP/NX
- Use fuzzing to detect overflow conditions

**Famous example:** The **Morris Worm (1988)** exploited a buffer overflow in `fingerd`. Buffer overflows have been exploited for decades and remain a top vulnerability class.

---

### 8.5.9 Race Conditions and TOCTOU

A **race condition** occurs when the output of a process depends on the sequence of uncontrollable events.

**TOCTOU (Time of Check to Time of Use):** The state of a resource changes between when it was checked and when it was used.

**Example:** 
1. App checks if a file is safe to open (Time of Check)
2. Attacker replaces the file with a malicious one
3. App opens the (now malicious) file (Time of Use)

**Prevention:**
- Use atomic operations
- Implement proper file locking
- Use transactions in database operations

---

## Quick Reference Summary

| Subdomain | Key Concepts | Key Tools/Standards |
|---|---|---|
| 8.1 SDLC Security | Waterfall, Agile, DevSecOps, CMMI, SAMM | OWASP SAMM, NIST SP 800-64 |
| 8.2 Ecosystem Controls | CI/CD, repositories, APIs, DBs | SBOM, SCA, signed commits |
| 8.3 Security Assessment | SAST, DAST, IAST, fuzzing, pen testing | Burp Suite, ZAP, Checkmarx |
| 8.4 Acquired Software | COTS, OSS, supply chain, SaaS | SOC 2, CVE, NIST SP 800-161 |
| 8.5 Secure Coding | OWASP Top 10, injection, crypto, memory | CERT, SANS, OWASP |

---

## Key Standards and Frameworks to Know

| Standard | Description |
|---|---|
| **OWASP Top 10** | Most critical web application security risks |
| **CERT Secure Coding Standards** | Language-specific secure coding rules (C, Java, etc.) |
| **NIST SP 800-64** | Security considerations in the SDLC |
| **NIST SP 800-161** | Supply chain risk management |
| **ISO/IEC 27034** | Application security framework |
| **OWASP SAMM** | Software assurance maturity model |
| **BSIMM** | Building Security In Maturity Model |
| **PCI-DSS** | Payment card industry secure coding requirements |

---

*Last updated: May 2026 | CISSP Domain 8 Study Reference*
