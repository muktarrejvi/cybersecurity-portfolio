# SSCP Domain 3: Risk Identification, Monitoring, and Analysis  
**Detailed Study Notes – 2025/2026 Preparation**  
(≈15% exam weight | Hands-on risk ID, monitoring, analysis & vulnerability ops)

Domain 3 emphasizes **operational risk practices**: identifying threats/vulnerabilities, assessing/prioritizing risks, continuous monitoring, log/event analysis, and reporting/escalation in real-world IT environments.

## 3.1 Understand the risk management process

### Risk Visibility and Reporting
- **Risk Register** → Centralized document/database tracking identified risks (risk ID, description, owner, likelihood, impact, status, mitigation actions, residual risk).
  - Used for prioritization, tracking remediation, audit evidence.
- **Sharing Threat Intelligence / Indicators of Compromise (IoC)** → Structured sharing (e.g., STIX/TAXII, MISP) of malware hashes, malicious IPs, URLs, TTPs.
  - Enhances collective defense (e.g., ISACs, CISA alerts).
- **Common Vulnerability Scoring System (CVSS)** → Standardized scoring (v4.0 current in 2025+):
  - Base Score (exploitability + impact) 0–10
  - Temporal (patch availability, exploit code maturity)
  - Environmental (modified by org assets/context)
  - Example: CVSS 9.8 = Critical → prioritize patching

### Risk Management Concepts
- **Impact Assessments** → Quantify consequences (financial, reputational, legal, operational downtime).
  - Qualitative (High/Med/Low) vs Quantitative (e.g., ALE = SLE × ARO).
- **Threat Modeling** → Identify threats early (STRIDE, PASTA, DREAD, attack trees).
  - Example: STRIDE — Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege.

### Risk Management Frameworks
| Framework       | Focus / Key Steps                                                                 | Best For                     | SSCP Relevance |
|-----------------|-----------------------------------------------------------------------------------|------------------------------|----------------|
| **NIST RMF** (SP 800-37 Rev 2) | 7 steps: Prepare → Categorize → Select → Implement → Assess → Authorize → Monitor | Federal systems, enterprises | Very high      |
| **ISO 31000**   | Principles → Framework → Process (Context, Assess, Treat, Monitor, Communicate)   | General/org-wide risk        | High           |
| **NIST CSF**    | Identify → Protect → Detect → Respond → Recover                                   | Voluntary, flexible          | Medium         |

- NIST RMF is lifecycle-based; ISO 31000 is process-oriented.

### Risk Tolerance (Appetite)
- **Risk Appetite** → Broad level of risk org willing to accept (strategic).
- **Risk Tolerance** → Specific thresholds (e.g., no risks > $100k impact without mitigation).
- **Risk Capacity** → Maximum risk org can bear before failure.

### Risk Treatment Options
| Option     | Description                                      | When to Use                              | Residual Risk |
|------------|--------------------------------------------------|------------------------------------------|---------------|
| **Accept** | Acknowledge & live with risk                     | Low impact/likelihood, cost > benefit    | Unchanged     |
| **Transfer** | Shift risk (insurance, outsourcing, contracts) | High financial impact, transferable      | Reduced       |
| **Mitigate** | Reduce likelihood/impact (controls, patching)   | Most common — cost-effective reduction   | Reduced       |
| **Avoid**  | Eliminate activity causing risk                  | Unacceptable high risk                   | Eliminated    |
| **Ignore** | Not an official option — poor practice           | Never — leads to negligence claims       | Full          |

**Exam Trap**: "Ignore" is **not** a valid treatment strategy.

## 3.2 Understand legal and regulatory concerns
- **Jurisdiction** → Which laws apply? (data location, citizenship, cloud provider location).
  - Example: GDPR (EU), CCPA/CPRA (California), HIPAA (US healthcare).
- **Limitations** → Export controls (ITAR/EAR), data sovereignty (Schrems II invalidation of Privacy Shield).
- **Privacy** → Principles: Consent, minimization, purpose limitation, rights (access, deletion).
  - Regulations: GDPR (Art. 5), Australian Privacy Act, PIPEDA (Canada).

**SSCP Focus**: Operational impacts (e.g., data residency in cloud, breach notification timelines).

## 3.3 Participate in security assessment and vulnerability management activities

### Security Testing
- Types: Vulnerability scanning, penetration testing, red teaming, code review.
- Tools: Nessus/OpenVAS (scanning), Metasploit/Burp (pentest).

### Risk Review
- Internal → Self-assessments, audits.
- Supplier/Third-party → Vendor risk assessments, SOC 2 reports.
- Architecture → Design reviews (threat modeling on new systems).

### Vulnerability Management Lifecycle (5–6 steps, cyclical)
1. **Discovery/Identification** → Scanning (authenticated/unauthenticated), asset inventory.
2. **Prioritization** → CVSS + exploitability + business criticality + threat intel.
3. **Assessment** → Validate (false positives?), root cause analysis.
4. **Remediation** → Patch, mitigate (WAF rule), accept/document.
5. **Verification** → Re-scan to confirm fix.
6. **Reporting & Lessons Learned** → Metrics (MTTR, vulnerability aging), process improvement.

**Modern Emphasis**: Continuous/automated vuln management (e.g., vulnerability orchestration tools).

## 3.4 Operate and monitor security platforms (continuous monitoring)

### Source Systems
- Applications, security appliances (firewalls, IDS/IPS), network devices, hosts/endpoints (EDR), cloud logs.

### Events of Interest
- Anomalies (behavioral deviations)
- Intrusions (signature + anomaly-based)
- Unauthorized changes (file integrity monitoring)
- Compliance monitoring (policy violations)

### Log Management
- Centralized logging (SIEM: Splunk, ELK, Azure Sentinel)
- Retention (compliance-driven, e.g., 1–7 years)
- Normalization, parsing, indexing

### Event Aggregation and Correlation
- Aggregate → Collect from many sources.
- Correlate → Link events (e.g., failed logins + file access = brute force + exfil attempt).
- Rules/alerts → SOAR for automation.

## 3.5 Analyze monitoring results

### Security Baselines and Anomalies
- Baseline → Normal behavior (user activity, traffic patterns).
- Anomalies → Deviations → investigate (e.g., UEBA detects impossible travel).

### Visualizations, Metrics, and Trends
- Dashboards (Kibana, Splunk), timelines (attack chain reconstruction).
- Key metrics: MTTD/MTTR, false positive rate, alert volume, patch compliance %.

### Event Data Analysis
- Triage → Prioritize alerts.
- Root cause → IOC hunting.
- Forensics → Chain of custody if incident.

### Document and Communicate Findings
- Escalate → Severity-based (e.g., critical → CISO immediately).
- Reports → Executive summary + technical details.
- Risk register updates.

**Key Principles (Exam Favorites)**
- **Continuous Monitoring** → NIST RMF step 6 — ongoing authorization.
- **Risk-Based Prioritization** → Not all vulns are equal.
- **Threat Intelligence Integration** → Enrich alerts with IOCs.
- **False Positive Reduction** → Tune rules, use context.

**Exam Tips**
- Know NIST RMF 7 steps cold.
- Risk treatment = accept/transfer/mitigate/avoid (ignore is wrong).
- CVSS = scoring, not patching decision alone.
- Vulnerability lifecycle = discover → prioritize → remediate → verify.
- Continuous monitoring ≠ one-time scan.
