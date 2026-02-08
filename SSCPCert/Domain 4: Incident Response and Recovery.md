# Domain 4: Incident Response and Recovery (14%)

**Domain Weight**: 14%  
**Key Focus**: Support the full lifecycle of handling security incidents, understand basic digital forensics principles, and contribute to business continuity / disaster recovery planning.

This domain tests your ability to minimize damage from incidents, preserve evidence correctly, and help restore normal operations quickly while learning from events.

## 4.1 Understand and support incident response lifecycle  
(e.g., NIST SP 800-61, ISO 27035)

Modern frameworks like **NIST SP 800-61** (r2/r3) and **ISO 27035** define structured phases. SSCP emphasizes practical support of these steps.

### Preparation
Build capabilities **before** an incident occurs.  
- Define roles (Incident Response Team, coordinator, legal, PR)  
- Create policies, procedures, contact lists  
- Deploy tools (SIEM, EDR, backups, forensics kits)  
- Conduct training and tabletop exercises  

**Example**: A company creates an incident response playbook, identifies the CSIRT lead, sets up alerting from firewalls/EDR to a central SIEM, and runs quarterly phishing simulation drills.

### Detection, Analysis, and Escalation
Identify potential incidents, confirm them, understand scope/impact, and escalate appropriately.  
- Sources: SIEM alerts, user reports, AV hits, IDS/IPS, anomalous logs  
- Analysis: triage (true/false positive?), classify severity, determine scope  
- Escalate: notify management, legal, regulators (e.g., GDPR/SEC breach notification)  

**Example**: SIEM detects multiple failed logins followed by successful access from unusual IP → analyst confirms ransomware encryption activity → escalates to CSIRT lead and CISO within 15 minutes.

### Containment
Stop the incident from spreading further. Short-term vs. long-term containment.  
- Short-term: isolate affected systems (pull network cable, disable account, block IP)  
- Long-term: rebuild/reimage, segment network, apply patches  

**Example**: During a ransomware outbreak, the team air-gaps infected servers, blocks C2 domains at the firewall, and disables compromised AD accounts to prevent lateral movement.

### Eradication
Remove the root cause and all artifacts of the attacker.  
- Delete malware, close vulnerabilities, remove backdoors, reset credentials  

**Example**: After containing WannaCry-like ransomware, the team wipes infected machines, removes the EternalBlue exploit patch gap, changes all passwords, and scans the environment with updated EDR signatures.

### Recovery
Safely return to normal operations.  
- Restore from clean backups, monitor closely for re-infection, validate functionality  
- Include incident documentation for insurance/regulatory purposes  

**Example**: Restore file servers from last known good backup (verified offline), enable monitoring rules for the IOCs seen during the incident, and gradually bring systems online while watching for anomalies.

### Lessons Learned / Post-Incident Activities  
(Implementation of new countermeasures, continuous improvement)  
- Conduct root cause analysis (RCA)  
- Hold after-action review (AAR) meeting  
- Update policies, tools, training based on findings  

**Example**: After a phishing breach, the organization adds mandatory MFA, improves email filtering, updates awareness training, and adds new detection rules for the TTPs observed.

## 4.2 Understand and support forensic investigations

### Legal and Ethical Principles
- Civil (lawsuits), criminal (prosecution), administrative (HR/regulatory)  
- Follow chain of custody, avoid spoliation of evidence  
- Ethical: minimize privacy impact, act in good faith  

**Example**: In a criminal insider theft case, evidence must be handled so it is admissible in court — improper handling could lead to evidence suppression.

### Evidence Handling
- **First responder**: secure scene, document everything, avoid altering data  
- **Triage**: prioritize what to collect (volatile data first: memory, running processes)  
- **Chain of custody**: log every person who handles evidence  
- **Preservation of scene**: take forensic images (dd, FTK, EnCase), work on copies  

**Example**: Responder arrives at a compromised workstation → powers it off only after capturing volatile memory (if policy allows), creates hash-verified disk image, documents timestamps and actions in chain-of-custody form.

### Reporting of Analysis
- Clear, factual report: what happened, when, how, impact, recommendations  
- May be used in legal proceedings or insurance claims  

**Example**: Forensic report states: "On 2026-01-15 at 14:32 UTC, malicious PowerShell script executed via email attachment → lateral movement via RDP → data exfiltration to IP 185.XX.XX.XX."

## 4.3 Understand and support Business Continuity Plan (BCP) and Disaster Recovery Plan (DRP) activities

### Emergency Response Plans and Procedures
- Info system contingency plan, natural disaster, pandemic, crisis management  
- Who activates, communication channels, safety first  

**Example**: During a data center flood, activate crisis management team, notify employees via emergency SMS, move to pre-identified alternate site.

### Interim or Alternate Processing Strategies
- Hot site, cold site, warm site, cloud failover, work-from-home  
- Manual processes as fallback  

**Example**: Company uses AWS for hot-site failover — when primary datacenter fails, DNS switch routes traffic to secondary region within minutes.

### Restoration Planning
- **RTO** (Recovery Time Objective): max acceptable downtime  
- **RPO** (Recovery Point Objective): max acceptable data loss  
- **MTD** (Maximum Tolerable Downtime) :  Maximum Tolerable Downtime (MTD) is the maximum amount of time a business process or system can be unavailable after a disruption before the organization suffers unacceptable damage (financial, legal, reputational, or operational).

Example:
If an online banking system has an MTD of 4 hours, the service must be restored within 4 hours after an outage, or the business impact becomes unacceptable.

**Example**: Critical payroll system has RTO = 4 hours, RPO = 15 minutes → frequent snapshots and fast restore from cloud backup.

### Backup and Redundancy Implementation
- 3-2-1 rule (3 copies, 2 media types, 1 offsite)  
- Immutable backups, air-gapped copies for ransomware protection  

**Example**: Daily incremental backups to disk + weekly full to tape stored offsite + immutable cloud copy retained 90 days.

### Testing and Drills
- Playbook walkthrough, tabletop exercises, full simulation  
- Test failover, restore from backup, incident notification  

**Example**: Annual DR drill: simulate primary site loss → failover to secondary datacenter, restore databases, validate application functionality, measure against RTO/RPO.

## Quick Reference Table – Key Metrics & Concepts

| Concept              | Definition                                      | Example Target (Critical System) |
|----------------------|-------------------------------------------------|----------------------------------|
| RTO                  | Max time to restore                             | 2–4 hours                        |
| RPO                  | Max data loss acceptable                        | 5–15 minutes                     |
| MTD                  | Max tolerable downtime (broader than RTO)       | 8 hours                          |
| Chain of Custody     | Documented handling of evidence                 | Required for court admissibility |
| NIST Phases          | Prep → Detect/Analyze → Contain → Eradicate → Recover → Lessons Learned | —                                |

**Study Tips for Domain 4**  
- Memorize NIST phases order and purpose  
- Know difference: **Incident** (security event) vs. **Disaster** (BCP/DRP trigger)  
- Understand volatility order for forensics: CPU registers → RAM → running processes → disk  
- Practice scenarios: ransomware, phishing → data breach, insider threat  

Cross-reference: NIST SP 800-61r2/r3, ISO 27035, (ISC)² SSCP Official Study Guide.

Last updated: January 2026
