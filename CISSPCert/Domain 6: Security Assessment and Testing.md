# Chapter 6: Security Assessment and Testing (Domain 6)

**Domain Weight**: 12% of the CISSP Exam (as of 2024/2025 outline)

**Purpose of this Domain**:  
This domain focuses on **validating** that security controls are working effectively. It answers the question: *"Are our protections actually protecting us?"* It covers designing assessments, performing tests, collecting data, analyzing results, and conducting audits.

---

## 6.1 Design and Validate Assessment, Test, and Audit Strategies

### Core Objective
Design, validate, and manage strategies for assessments, tests, and audits to ensure they are effective, comprehensive, and aligned with business and compliance needs.

### Categories / Types

#### 1. **Assessment Types (by Scope/Control)**
- **Internal Assessments** — Performed by teams within the organization's control (e.g., internal red team or security ops).
- **External Assessments** — Performed by parties outside the organization but under contract (e.g., hired consulting firm).
- **Third-Party Assessments** — Performed by independent parties outside enterprise control (e.g., regulators, auditors, cloud providers).

#### 2. **Location-Based Strategies**
- **On-Premises**
- **Cloud**
- **Hybrid**

#### 3. **Assessment Strategies by Purpose**
- **Risk-Driven** — Prioritized by risk assessment results.
- **Compliance-Driven** — Driven by regulations (PCI-DSS, SOX, HIPAA, etc.).
- **Continuous vs. Periodic** — Ongoing monitoring vs. scheduled events.

#### Key Concepts
- **Validation** — Ensuring the assessment method is sound and repeatable.
- **Scoping** — Defining boundaries, rules of engagement (RoE), and limitations.
- **Threat Modeling Integration** — Using STRIDE, PASTA, etc., to guide testing focus.
- **Defense in Depth Validation** — Testing multiple control layers.

**Exam Tip**: Understand when to choose internal vs. external vs. third-party and how location (cloud/hybrid) affects strategy.

---

## 6.2 Conduct Security Controls Testing

This is the **most heavily tested** subdomain in Domain 6.

### Main Categories of Testing

#### 1. **Vulnerability Assessment**
- **Definition**: Systematic identification of weaknesses (does not exploit them).
- **Types**:
  - **Credentialed (Authenticated)** — Deeper view with login rights.
  - **Non-credentialed (Unauthenticated)** — External attacker perspective.
- **Tools**: Nessus, Qualys, OpenVAS, Microsoft Defender for Vulnerability Management.
- **Output**: List of vulnerabilities with severity (CVSS scoring).

#### 2. **Penetration Testing (Pen Testing)**
- **Definition**: Actively exploits vulnerabilities to prove impact (simulates real attacks).
- **Team Exercises**:
  - **Red Team** — Offensive (attackers).
  - **Blue Team** — Defensive (defenders).
  - **Purple Team** — Collaborative (red + blue knowledge sharing).
- **Testing Approaches**:
  - **Black Box** — No prior knowledge (external attacker view).
  - **Gray Box** — Partial knowledge.
  - **White Box** — Full knowledge (source code, architecture).
- **Phases**: Reconnaissance → Scanning → Gaining Access → Maintaining Access → Covering Tracks.

#### 3. **Log Reviews**
- Analysis of security, application, system, and audit logs.
- Focus: Anomalies, failed logins, privilege escalations, etc.

#### 4. **Synthetic Transactions / Benchmarks**
- Simulated user transactions to measure performance and availability of critical systems.

#### 5. **Other Important Testing Types**
- **Code Review and Testing**:
  - Static Application Security Testing (SAST)
  - Dynamic Application Security Testing (DAST)
  - Interactive (IAST) and Runtime (RASP)
- **Misuse Case Testing** — Testing for abuse/misuse scenarios.
- **Interface Testing** — UI, API, Network interfaces.
- **Breach Attack Simulations (BAS)** — Continuous automated attack simulation.
- **Compliance Checks** — Mapping controls to standards.

**Exam Tip**: Know **Vulnerability Assessment vs Penetration Testing** differences clearly.

---

## 6.3 Collect Security Process Data (Technical & Administrative)

Focuses on gathering evidence of control effectiveness over time.

### Key Data Types & Categories

#### 1. **Account Management**
- User account reviews, privilege audits, dormant account cleanup.

#### 2. **Management Review and Approval**
- Evidence of periodic management oversight and sign-off.

#### 3. **Key Performance Indicators (KPIs) & Key Risk Indicators (KRIs)**
- **KPIs** — Measure control performance (e.g., % of systems patched within SLA).
- **KRIs** — Early warning of increasing risk (e.g., rising number of critical vulnerabilities).

#### 4. **Backup Verification Data**
- Backup success rates, restore test results.

#### 5. **Training and Awareness**
- Completion rates, phishing simulation results, effectiveness metrics.

#### 6. **Disaster Recovery (DR) and Business Continuity (BC)**
- Recovery Time Objective (RTO) / Recovery Point Objective (RPO) achievement.
- Tabletop exercises, walkthroughs, full simulations.

**Exam Tip**: These are mostly **operational metrics** used to prove controls are functioning as intended.

---

## 6.4 Analyze Test Output and Generate Report

### Process Flow
1. **Analyze** raw results.
2. **Prioritize** findings (risk rating).
3. **Generate** actionable reports.
4. **Handle exceptions and remediation**.

### Key Elements

#### Report Components
- Executive Summary (for management)
- Technical Details
- Risk Ratings (High/Medium/Low or CVSS)
- Evidence
- Recommendations & Remediation Steps

#### Important Concepts
- **Remediation** — Fixing identified issues with timelines.
- **Exception Handling** — Documenting accepted risks (with business justification and compensating controls).
- **Ethical Disclosure** — Responsible reporting of vulnerabilities (especially in third-party testing).

**Exam Tip**: Reports must be **clear, actionable, and tailored** to the audience (technical vs. executive).

---

## 6.5 Conduct or Facilitate Security Audits

### Audit Types by Party
- **Internal Audits** — Performed by internal audit team.
- **External Audits** — Independent third-party auditors.
- **Third-Party Audits** — Often for compliance (SOC 2, ISO 27001, PCI QSA).

### Audit Categories
- **Compliance Audits** — Against laws, regulations, standards.
- **Operational Audits** — Effectiveness of processes.
- **Financial Audits** (with security component) — SOX, etc.
- **Integrated Audits** — Combines financial + IT/security.

### Audit Frameworks & Standards
- **SOC Reports**:
  - SOC 1 (financial controls)
  - SOC 2 (security, availability, confidentiality, processing integrity, privacy)
  - SOC 3 (public-facing summary)
- **ISO 27001**
- **NIST SP 800-53A**
- **PCI-DSS**

### Audit Process
1. Planning → 2. Fieldwork → 3. Reporting → 4. Follow-up

**Exam Tip**: Understand difference between **Audit** (compliance-focused) vs **Assessment** (broad) vs **Testing** (technical).

---

## Summary Mind Map Style Overview

- **6.1** → Strategy & Planning (Internal/External/Third-party + Location)
- **6.2** → Execution (VA + PT + Logs + Code + etc.)
- **6.3** → Continuous Data Collection (KPIs/KRIs + Account + Backup + Training)
- **6.4** → Analysis & Reporting (Remediation + Exceptions)
- **6.5** → Formal Audits (SOC, ISO, Compliance)

- Understand SOC 1 vs SOC 2.
- Practice writing risk-based findings.
