
# Microsoft Entra ID — A Comprehensive Tutorial

> A practical, lab-driven guide to Microsoft's cloud identity and access management platform.
> Written for security analysts, cloud admins, and students preparing for SC-300 / SC-900 / AZ-104.

**Last reviewed:** September 2026 · **Level:** Beginner → Advanced · **Est. time:** 8–12 hours with labs

---

## Table of Contents

1. [What Entra ID Actually Is](#1-what-entra-id-actually-is)
2. [Setting Up a Free Lab Tenant](#2-setting-up-a-free-lab-tenant)
3. [Core Objects and the Tenant Model](#3-core-objects-and-the-tenant-model)
4. [Licensing: Free, P1, P2, Governance, Suite](#4-licensing-free-p1-p2-governance-suite)
5. [Authentication](#5-authentication)
6. [Authorization: Roles, Scope, and PIM](#6-authorization-roles-scope-and-pim)
7. [Conditional Access](#7-conditional-access)
8. [Identity Protection](#8-identity-protection)
9. [Identity Governance](#9-identity-governance)
10. [Hybrid Identity](#10-hybrid-identity)
11. [Application Integration and SSO](#11-application-integration-and-sso)
12. [External Identities (B2B and External ID)](#12-external-identities-b2b-and-external-id)
13. [Global Secure Access](#13-global-secure-access)
14. [Workload and Agent Identities](#14-workload-and-agent-identities)
15. [Monitoring, Logging, and Reporting](#15-monitoring-logging-and-reporting)
16. [Automation with Microsoft Graph](#16-automation-with-microsoft-graph)
17. [Attack Scenarios and Defences](#17-attack-scenarios-and-defences)
18. [Hardening Checklist](#18-hardening-checklist)
19. [2025–2026 Breaking Changes and Deadlines](#19-20252026-breaking-changes-and-deadlines)
20. [Hands-On Labs](#20-hands-on-labs)
21. [Certification Mapping](#21-certification-mapping)
22. [Glossary](#22-glossary)
23. [Further Reading](#23-further-reading)

---

## 1. What Entra ID Actually Is

Microsoft Entra ID is a cloud-based identity provider (IdP) and directory service. It is the identity plane for Microsoft 365, Azure, and tens of thousands of third-party SaaS applications.

It was renamed from **Azure Active Directory (Azure AD)** in 2023. The product, the P1/P2 tiers, and the APIs are all the same — only the branding changed. You will still encounter `AzureAD` in older docs, PowerShell modules, Terraform providers, and licensing agreements.

### What it is not

A very common misconception is that Entra ID is "Active Directory in the cloud." It is not. The two solve overlapping problems with completely different architectures:

| | Windows Server Active Directory (AD DS) | Microsoft Entra ID |
|---|---|---|
| Protocols | Kerberos, NTLM, LDAP | OAuth 2.0, OpenID Connect, SAML 2.0, WS-Fed, SCIM |
| Structure | Hierarchical — forests, domains, OUs | Flat directory + administrative units |
| Group Policy | Yes (GPO) | No — use Intune/Endpoint Manager |
| Trust model | Forest/domain trusts | Cross-tenant access settings, B2B |
| Query interface | LDAP | Microsoft Graph REST API |
| Designed for | LAN-attached Windows domain members | Internet-facing apps and devices anywhere |
| Ships with | Windows Server licence | Every Microsoft 365 / Azure subscription |

If you try to map OUs onto Entra ID, you will be frustrated. Think in terms of **groups, administrative units, and policy scope** instead.

### The layered mental model

Work through Entra ID in this order — each layer depends on the one before it:

```
┌─────────────────────────────────────────────────────┐
│  6. Governance    access reviews, lifecycle, PIM    │
├─────────────────────────────────────────────────────┤
│  5. Protection    risk detection, CAE, remediation  │
├─────────────────────────────────────────────────────┤
│  4. Access policy Conditional Access                │
├─────────────────────────────────────────────────────┤
│  3. Authorization roles, scope, app permissions     │
├─────────────────────────────────────────────────────┤
│  2. Authentication methods, MFA, passwordless       │
├─────────────────────────────────────────────────────┤
│  1. Directory     users, groups, devices, apps      │
└─────────────────────────────────────────────────────┘
```

Most real-world breaches happen because someone built layer 4 without properly understanding layers 1–3.

---

## 2. Setting Up a Free Lab Tenant

You cannot learn this from reading. Get a tenant.

### Option A — Microsoft 365 Developer Program

Historically the best option: a renewable E5 sandbox tenant with 25 licensed users. Availability and eligibility criteria have changed several times, so check the current terms before relying on it.

### Option B — Azure free account + Entra ID P2 trial

1. Create an Azure free account (requires a credit card for identity verification).
2. Sign in to the Microsoft Entra admin center at `entra.microsoft.com`.
3. Create a new tenant: **Identity → Overview → Manage tenants → Create**.
4. Activate the **Entra ID P2 trial** — 30 days, 100 licences. This is what unlocks PIM, Identity Protection, and access reviews for lab work.

### Option C — Trial via the Microsoft 365 admin center

A Business Premium or E5 trial gives you P1 or P2 respectively for 25–30 days.

### Lab hygiene rules

- **Never test in production.** Conditional Access can lock every administrator out of a tenant in one click.
- **Create two break-glass accounts immediately** (see [Lab 1](#lab-1--tenant-baseline)).
- Use a throwaway domain or the default `*.onmicrosoft.com` domain.
- Set a calendar reminder for the trial expiry so a lab tenant doesn't silently downgrade mid-exercise.

---

## 3. Core Objects and the Tenant Model

### The tenant

A **tenant** is a dedicated, isolated instance of Entra ID representing one organisation. It has:

- A **tenant ID** — an immutable GUID. This is what you use in scripts and app configuration.
- One or more **verified domains** — `contoso.com`, plus the default `contoso.onmicrosoft.com`.
- A single **directory** of objects.

One tenant can be linked to many Azure subscriptions. One Azure subscription trusts exactly one tenant. This distinction trips people up constantly: **Entra ID roles and Azure RBAC roles are separate systems** (more in §6).

### Users

Three creation paths, and the difference matters for troubleshooting:

| Type | `onPremisesSyncEnabled` | Where you edit it | Notes |
|---|---|---|---|
| Cloud-only | `false` / null | Entra ID | Fully managed in the cloud |
| Synced from AD | `true` | On-premises AD | Most attributes are read-only in the cloud |
| Guest (B2B) | n/a | Home tenant | `userType = Guest`, `#EXT#` in UPN |

Key attributes to know: `userPrincipalName` (the sign-in name), `mail`, `objectId`, `accountEnabled`, `userType`, `usageLocation` (required before assigning most licences — a frequent cause of "licence assignment failed" errors).

### Groups

| Group type | Membership | Used for |
|---|---|---|
| Security | Assigned or dynamic | Access control, licensing, CA policy targeting |
| Microsoft 365 | Assigned or dynamic | Collaboration — carries a mailbox, SharePoint site, Teams team |

**Dynamic groups** use a membership rule expressed in a query language:

```
(user.department -eq "Engineering") and (user.country -eq "AU") and (user.accountEnabled -eq true)
```

Dynamic membership requires **P1**. Rules evaluate asynchronously — expect minutes, not seconds, and never build a break-glass exclusion on a dynamic group.

**Group-based licensing** (P1) assigns licences via group membership rather than per user. This is the only sane way to manage licensing beyond about 50 users.

### Devices

| Join type | Scenario | Sign-in |
|---|---|---|
| Entra registered | BYOD, personal devices | Personal account, work access added |
| Entra joined | Corporate cloud-only | Work account signs into Windows |
| Hybrid joined | Corporate with on-prem AD | Joined to both AD DS and Entra ID |

Device state is a Conditional Access signal — "require a compliant device" is one of the strongest controls available, but it depends on Intune supplying the compliance verdict.

### Applications: the two-object model

This is the single most misunderstood part of Entra ID.

- **Application registration** (`application` object) — the global definition of an app. Lives in the tenant where the developer created it. Defines redirect URIs, requested permissions, certificates and secrets.
- **Service principal** (`servicePrincipal` object) — the local instance of that app *in your tenant*. This is what actually gets permissions, role assignments, and sign-in log entries.

For a multi-tenant app like Salesforce, there is one app registration in Salesforce's tenant and one service principal in each customer tenant. When you audit "which apps have access to my data," you are auditing **service principals**, not app registrations.

### Administrative units (AU)

An AU is a container that scopes *role assignments* — not a security boundary for data. Assign a User Administrator over the "Melbourne" AU and they can reset passwords only for users in that AU. Requires **P1**. Restricted management AUs, which prevent tenant-wide admins from modifying the contained objects, require **P2**.

---

## 4. Licensing: Free, P1, P2, Governance, Suite

Licensing determines what you can build, so learn it early. Prices below are USD list, per user per month, annual commitment.

| Plan | Price | Key capabilities |
|---|---|---|
| **Free** | $0 | SSO, basic MFA via security defaults, SSPR for cloud users, 500k objects |
| **P1** | ~$6 | Conditional Access, granular MFA control, dynamic groups, group-based licensing, self-service password reset with on-prem writeback, Application Proxy, Cloud Sync |
| **P2** | ~$9 | Everything in P1 **plus** Identity Protection (risk-based CA), Privileged Identity Management, access reviews |
| **ID Governance** | add-on | Entitlement management, lifecycle workflows, advanced access reviews |
| **Entra Suite** | ~$12 | ID Protection + full ID Governance + Internet Access + Private Access + Verified ID premium. Requires a P1 base |

Where they're bundled:

- **Microsoft 365 E3, F1, F3, Business Premium, EM+S E3** → include P1
- **Microsoft 365 E5, EM+S E5** → include P2
- **Microsoft 365 E7** (~$99/user/month, generally available since 1 May 2026) → the first M365 SKU to include the complete Entra Suite, bundling E5 + Copilot + Agent 365 + Entra Suite

Two practical notes:

1. **Check before you buy.** A very large share of standalone P1/P2 purchases are wasted because the organisation already holds them inside E3 or E5.
2. **Right-size P2.** In a 500-user org with 15 admins, PIM is only meaningful for those 15. But risk-based Conditional Access applies per licensed user, and Microsoft's licensing terms expect every user who benefits from a feature to be licensed for it — so scoping P2 to admins only is defensible for PIM, less so for Identity Protection covering the whole workforce. Decide deliberately, and document the decision.

Licensing is no longer a simple three-way choice. As of 2026 you need to check feature-level licensing across P1/P2, ID Governance, the Entra Suite, M365 E7, and Agent 365 before enabling Conditional Access, governance, PIM, Global Secure Access, or agent controls.

---

## 5. Authentication

### Authentication methods, ranked

From weakest to strongest:

| Method | Phishing-resistant | Notes |
|---|---|---|
| Password only | ❌ | Should never be the only factor |
| SMS / voice call | ❌ | Vulnerable to SIM swap and interception. Deprecate it |
| Third-party OATH TOTP | ❌ | Better than SMS, still phishable |
| Microsoft Authenticator (push + number matching) | ❌ | Good baseline; number matching defeats MFA fatigue |
| Windows Hello for Business | ✅ | Device-bound biometric/PIN |
| Passkeys (FIDO2) | ✅ | Hardware key or platform passkey. The target state |
| Certificate-based authentication (CBA) | ✅ | Smart cards, PIV/CAC — common in government |

The **authentication methods policy** (Entra admin center → Protection → Authentication methods) is where you enable, disable, and target methods to groups. Migrate off the legacy per-user MFA settings and the legacy SSPR method configuration; they are superseded by this policy.

As of 2026, passkey policy has its own dedicated 20 KB allocation in the authentication methods policy rather than sharing one budget with all other methods, and tenants can define up to 10 passkey profiles instead of 3 — which makes targeted rollout by group far more practical.

### MFA is now mandatory — this is not optional

Microsoft's Secure Future Initiative made MFA compulsory for Microsoft's own management surfaces, in phases:

- **From October 2024:** MFA required for any create/read/update/delete operation in the Azure portal, Entra admin center, and Intune admin center. Phase 1 completed March 2025.
- **From February 2025:** enforcement began rolling out for the Microsoft 365 admin center.
- **From 1 October 2025:** enforcement extended to Azure CLI, Azure PowerShell, the Azure mobile app, IaC tools, and control-plane REST API endpoints for create/update/delete. Read operations are exempt.
- **From 9 February 2026:** sign-in to the Microsoft 365 admin center is blocked outright without MFA.
- **1 July 2026:** the final deadline for postponement requests. Microsoft has stated there are no further extensions.

Important scoping details:

- The enforcement is server-side at Azure Resource Manager. Anything hitting `https://management.azure.com` is in scope, whatever the client.
- **Service principals, managed identities, and workload identities are excluded** — they don't sign in interactively. This is the strongest possible argument for migrating user-account-based automation to service principals or managed identities.
- **Break-glass accounts are in scope** and must have MFA registered. Plan for this — a break-glass account you can't sign into is worse than no break-glass account.

To find your gaps before enforcement finds them for you, use the **Multifactor Authentication Gaps workbook** in Entra ID, or `Export-MsIdAzureMfaReport` from the `MSIdentityTools` module.

### Self-Service Password Reset (SSPR)

Three settings that matter:

- **Number of methods required to reset** — set to 2.
- **Require users to re-confirm authentication information** — 180 days is reasonable.
- **Password writeback** — writes cloud resets back to on-premises AD. Requires P1 and Entra Connect.

### Password protection

- **Global banned password list** — Microsoft-maintained, always on.
- **Custom banned password list** — add your organisation name, local sports teams, product names. Up to 1,000 terms.
- **On-premises password protection** — deploy the DC agent and proxy to extend the ban list to AD DS password changes. Run it in audit mode first.

### Token lifetimes and Continuous Access Evaluation

Access tokens default to roughly one hour. The old advice of shortening token lifetimes has been replaced by **Continuous Access Evaluation (CAE)**: resource providers such as Exchange Online, SharePoint, and Microsoft Graph subscribe to critical events and revoke sessions in near real time when a user is disabled, a password is reset, or risk is elevated — instead of waiting for token expiry.

CAE is the single most effective mitigation for stolen refresh tokens. Enable it. Microsoft has scheduled a CAE requirement for October 2026, so this is becoming table stakes.

---

## 6. Authorization: Roles, Scope, and PIM

### Two separate RBAC systems

| | Entra ID roles | Azure RBAC |
|---|---|---|
| Controls | Directory objects — users, groups, apps, policies | Azure resources — VMs, storage, networks |
| Scope | Tenant, administrative unit, or single application | Management group, subscription, resource group, resource |
| Managed in | Entra admin center → Roles and administrators | Azure portal → IAM blade |
| Example role | User Administrator, Conditional Access Administrator | Contributor, Storage Blob Data Reader |

A **Global Administrator** can elevate themselves to **User Access Administrator** at the Azure root scope — which is how a directory-level compromise becomes a full Azure compromise. Treat that toggle as a monitored, alertable event.

### Roles worth knowing cold

| Role | What it can do | Risk |
|---|---|---|
| Global Administrator | Everything | Extreme — keep under 5, ideally under 3 |
| Privileged Role Administrator | Assign any role, manage PIM | Equivalent to GA in practice |
| Application Administrator | Manage all app registrations, add credentials | Can add a secret to a privileged SP → privilege escalation |
| Privileged Authentication Administrator | Reset credentials for *any* user including GAs | Effective GA |
| User Administrator | Manage users, reset non-admin passwords | Moderate |
| Conditional Access Administrator | Create/modify CA policies | Can disable your entire security perimeter |
| Security Reader | Read-only security data | Good default for analysts |
| Global Reader | Read-only everything | The correct role for auditors |

Least-privilege rule of thumb: if the task is *investigating*, use Global Reader or Security Reader. Global Administrator is for tenant configuration only, never for daily work.

Note that Microsoft has been expanding the **Security Administrator** role to include identity response actions for non-privileged users — disabling and re-enabling accounts, revoking active sessions — so SOC analysts can respond without an over-broad role.

### Privileged Identity Management (PIM) — P2

PIM converts standing privilege into just-in-time privilege. Instead of being a permanent Global Administrator, you are **eligible** and activate the role for a bounded window.

Configure per role:

- **Activation maximum duration** — 1–4 hours for high-privilege roles.
- **Require MFA on activation** — always. Prefer phishing-resistant.
- **Require justification** — always. This is your audit trail.
- **Require approval** — for Global Administrator and Privileged Role Administrator.
- **Require ticket information** — ties activation to a change record.

PIM also covers **Azure resource roles** and **PIM for Groups**, which lets you make membership of a privileged group itself just-in-time.

**Access reviews** (P2) close the loop: schedule a recurring review where a manager or the user themselves confirms continued need, with automatic removal when nobody responds.

---

## 7. Conditional Access

Conditional Access (CA) is the policy engine at the heart of Zero Trust in the Microsoft stack. It requires **P1**. Everything in this section assumes P1 or above.

### The evaluation model

```
        SIGNALS                DECISION              ENFORCEMENT
  ┌──────────────────┐    ┌──────────────┐     ┌────────────────────┐
  │ User / group     │    │              │     │ Grant access       │
  │ Application      │    │   Evaluate   │     │ Require MFA        │
  │ Device state     │───▶│  assignments │────▶│ Require compliant  │
  │ Location / IP    │    │      +       │     │ Require app protect│
  │ Client app       │    │  conditions  │     │ Limit session      │
  │ Sign-in risk     │    │              │     │ BLOCK              │
  │ User risk        │    │              │     │                    │
  └──────────────────┘    └──────────────┘     └────────────────────┘
```

Policies are evaluated on **every** sign-in. All matching policies apply, and **block always wins** over grant.

### Policy anatomy

**Assignments** — who and what the policy applies to:
- Users and groups (include / exclude)
- Target resources: cloud apps, user actions (e.g. registering security info), or authentication context
- Conditions: device platform, location, client app, device filter, sign-in risk, user risk, insider risk

**Access controls** — what happens:
- *Grant*: block, or grant with requirements (MFA, compliant device, hybrid joined, approved client app, app protection policy, terms of use, password change). Choose "require all" vs "require one."
- *Session*: sign-in frequency, persistent browser session, app-enforced restrictions, Conditional Access App Control (Defender for Cloud Apps), CAE, token protection.

### The baseline policy set

Start here. Build every one of these in **report-only** mode first.

1. **Block legacy authentication** — POP, IMAP, SMTP AUTH, older Office clients. Legacy protocols cannot do MFA, so they are the preferred path for password spray. This is the highest-value single policy.
2. **Require MFA for all administrators** — target the privileged role directory objects, not a group.
3. **Require MFA for all users** — with your break-glass accounts excluded.
4. **Require MFA to register security information** — closes the gap where an attacker with a stolen password enrols their own MFA method.
5. **Block access from unsupported device platforms.**
6. **Require compliant or hybrid-joined device for desktop access.**
7. **Block access from countries you never operate in** — a blunt but useful control.
8. **Require phishing-resistant MFA for privileged roles** — the target state.
9. **Sign-in frequency + no persistent browser for unmanaged devices.**
10. **Require MFA for Azure management** (the `Windows Azure Service Management API` app).

### Operational discipline

- **Always exclude break-glass accounts** from every policy. Two accounts, cloud-only, `*.onmicrosoft.com` domain, very long random passwords split across sealed envelopes, monitored with an alert on any sign-in.
- **Report-only mode** logs what *would* have happened without enforcing. Run for at least a week and read the workbook before enabling.
- **What If tool** simulates a specific user/app/condition combination against your live policy set.
- **Version control your policies.** Export them via Graph and store the JSON in Git. See §16.
- **Name policies systematically:** `CA00x — [Users] — [Apps] — [Control] — [State]`.

Microsoft also ships **Conditional Access templates** for common patterns, and has been changing them over time — review any template-derived policy after a template update rather than assuming it still says what you think.

---

## 8. Identity Protection

Requires **P2**. Identity Protection applies machine learning to score risk, then lets Conditional Access act on that score.

### Two risk types

**Sign-in risk** — the probability that a specific authentication request wasn't the legitimate user:

| Detection | Meaning |
|---|---|
| Anonymous IP address | Sign-in from Tor or an anonymising proxy |
| Atypical travel | Two sign-ins from geographically impossible locations |
| Malware-linked IP | Source IP associated with a known bot network |
| Unfamiliar sign-in properties | Deviates from the learned baseline for that user |
| Token issuer anomaly | SAML token appears forged |
| Suspicious browser / impossible token | Session anomalies |

**User risk** — the probability that the identity itself is compromised:

| Detection | Meaning |
|---|---|
| Leaked credentials | Credentials found in a breach dump or paste site |
| Threat intelligence | Microsoft's threat intel flags the account |
| Anomalous user activity | Behavioural deviation over time |

### Recommended response

| Risk level | Sign-in risk response | User risk response |
|---|---|---|
| High | Block, or require phishing-resistant MFA | Require secure password change |
| Medium | Require MFA | Require secure password change |
| Low | Monitor | Monitor |

**Important migration note:** the legacy sign-in-risk and user-risk policies configured inside Identity Protection are being retired. Recreate them as **Conditional Access policies** with risk as a condition — the Identity Protection UI for these two policies is scheduled to be retired on **1 October 2026**. Do this migration now if you haven't; the CA versions are more flexible anyway.

The **Risky Users report** was redesigned in 2026 with richer timelines and better searchability, which makes triage considerably faster than the old flat list.

---

## 9. Identity Governance

Answers the question *"who should have access to what, and for how long?"*

### Entitlement management

**Access packages** bundle everything a role needs — groups, applications, SharePoint sites — into one requestable unit with a defined policy: who may request, who approves, how long it lasts, and what happens at expiry.

```
Access Package: "Contractor — Data Analyst"
├── Resources
│   ├── Group: DataAnalysts-AU
│   ├── App:   Power BI Pro
│   └── Site:  SharePoint /analytics
└── Policy
    ├── Who can request: users in connected organisation "Acme"
    ├── Approval: hiring manager, then data governance lead
    ├── Duration: 90 days
    └── On expiry: remove all resources
```

**Connected organisations** let you extend access packages to external partners. Admins can now assign external users to an access package directly by email address — they are invited as guests and governed from that point.

### Access reviews

Scheduled recertification for group membership, application assignments, role assignments (including PIM-eligible roles), and guest access. Configure reviewers as the resource owner, the user's manager, self-review, or a named group. Set `Apply results automatically` and decide what happens when a reviewer doesn't respond — "remove access" is the safe default; "no change" quietly defeats the whole exercise.

### Lifecycle workflows

Automate joiner-mover-leaver:

- **Joiner** — 7 days before the hire date: generate a temporary access pass, add to groups, send a welcome email.
- **Mover** — on attribute change: recalculate group membership, trigger an access review.
- **Leaver** — on the last working day: disable the account, revoke all refresh tokens, remove from groups, remove licences, hand the mailbox to the manager.

Lifecycle workflows require an ID Governance licence. Tenants get up to 50 workflows and up to 100 custom task extensions.

### Directory backup

Microsoft Entra now takes automatic daily backups of critical directory objects — users, groups, applications, service principals, managed identities, Conditional Access policies, named locations, agent IDs, and authentication/authorization policies — retained for 7 days with a P1 or P2 licence, on by default. You can view snapshots, diff changes, and run recovery jobs. This is a genuine safety net against a bad policy push, but 7 days is not an archive: keep your own exported policy JSON in Git regardless.

---

## 10. Hybrid Identity

Most enterprises run on-premises AD DS alongside Entra ID. The sync tool and the authentication method are two independent choices.

### Sync tooling

| | Entra Connect Sync | Entra Cloud Sync |
|---|---|---|
| Runs on | A Windows server you maintain | A lightweight agent; config lives in the cloud |
| Complex transforms | Yes | Limited |
| Multiple disconnected forests | Complex | Native, straightforward |
| Device writeback / hybrid join | Yes | Partial |
| Exchange hybrid writeback | Yes | No |
| High availability | Staging server | Multiple agents |
| Direction of travel | Legacy | Microsoft's strategic tool |

For greenfield or simple topologies, use Cloud Sync. For Exchange hybrid or heavy attribute manipulation, you still need Connect Sync.

### Authentication method

| Method | How it works | Trade-off |
|---|---|---|
| **Password Hash Sync (PHS)** | A hash-of-the-hash of the AD password syncs to Entra ID; the cloud authenticates | Simplest, most resilient, survives on-prem outage. Enables leaked-credential detection. **Recommended default** |
| **Pass-through Authentication (PTA)** | Cloud passes the credential to an on-prem agent that validates against a DC | No password material in the cloud; depends on agent availability |
| **Federation (AD FS)** | Entra ID redirects to your AD FS farm | Maximum control, maximum operational burden and attack surface |

Even if you use PTA or federation, **enable PHS as a backup**. It costs nothing and lets you fail over if the on-prem path breaks — a lesson many organisations learned expensively during AD FS outages.

### Source of authority

Entra ID now supports converting the **source of authority** of a synced on-premises user to a cloud-managed user. This is the mechanism for gradually decommissioning AD DS without a big-bang cutover. Note that hard-match behaviour changed in mid-2026, so check current guidance before running a large conversion.

### Hybrid gotchas

- The **`ms-DS-ConsistencyGuid`** anchor is what ties an AD object to its cloud object. Break it and you get duplicate accounts.
- **Filter before you sync.** Never sync service accounts, disabled OUs, or built-in privileged AD groups into the cloud.
- **Never sync on-premises Domain Admins into a cloud-privileged group.** This creates a bidirectional escalation path between the two environments — the classic "AD compromise becomes cloud compromise" chain.

---

## 11. Application Integration and SSO

### Protocol choice

| Protocol | Use when | Token |
|---|---|---|
| **OpenID Connect** | Modern apps, mobile, SPAs | ID token (JWT) + access token |
| **OAuth 2.0** | API authorization (not authentication) | Access token (JWT) |
| **SAML 2.0** | Established enterprise SaaS | SAML assertion (XML) |
| **WS-Federation** | Legacy .NET apps | SAML 1.1 assertion |
| **Password-based SSO** | Apps with no federation support | Credential vaulting, not real SSO |
| **Header-based SSO** | Legacy on-prem apps behind App Proxy | HTTP headers |

A rule that catches out many developers: **OAuth 2.0 is an authorization framework, not an authentication protocol.** If you're proving *who the user is*, you want OpenID Connect on top of it.

### App registration essentials

- **Redirect URIs** must match exactly. Wildcards are not permitted, and loose redirect URI handling is a classic token-theft vector.
- **Client secrets vs certificates** — always prefer certificates. Secrets expire and get pasted into repos.
- **Delegated vs application permissions:**
  - *Delegated* — the app acts **as the signed-in user**; effective access is the intersection of the app's permission and the user's own rights.
  - *Application* — the app acts **as itself**, with no user. `Mail.Read` as an application permission means every mailbox in the tenant. Audit these ruthlessly.
- **Admin consent** — required for high-privilege scopes. Configure a **consent policy** so users can only consent to low-risk permissions from verified publishers, and enable the **admin consent workflow** so requests are routed rather than silently blocked.

### Provisioning (SCIM)

Entra ID can push user lifecycle changes into SaaS apps over SCIM 2.0, so a leaver in Entra ID becomes a deactivated user in Salesforce automatically. Always start in **provision on demand** mode against a single test user before enabling scope-wide sync.

### Application Proxy

Publishes an internal web app to the internet through a connector running inside your network, with pre-authentication at Entra ID and Conditional Access applied. No inbound firewall ports. Requires P1 or P2. It is increasingly superseded by **Entra Private Access** (§13) for anything beyond simple HTTP apps.

---

## 12. External Identities (B2B and External ID)

### B2B collaboration

Invite a partner's identity into your tenant as a guest. They authenticate against **their** home tenant; you control what they can reach in yours. No new password to manage, and when their home org disables them, their access to you dies too.

**Cross-tenant access settings** are the modern control plane for this:

- **Inbound** — which external tenants' users may come in, and whether you trust their MFA and device compliance claims (trusting them avoids double-prompting).
- **Outbound** — which external tenants your users may access.
- **Tenant restrictions v2** — blocks your users from signing into *foreign* tenants from your network or managed devices. This is the control that stops data exfiltration to a personal or attacker-controlled tenant.

Guests are billed on a **Monthly Active User (MAU)** basis rather than per licence.

Since mid-2025, security defaults no longer force MFA registration on B2B guests, which removed a long-standing friction point in file-sharing scenarios.

### Entra External ID

The successor to Azure AD B2C — a customer identity and access management (CIAM) platform for consumer- and citizen-facing apps, with custom-branded sign-up/sign-in journeys, social identity providers, and self-service. Treat it as a separate product with its own tenant type; don't mix workforce and customer identities in one directory.

---

## 13. Global Secure Access

Microsoft's Security Service Edge (SSE) offering. Two products, both licensed via the Entra Suite (or standalone on a P1 base):

**Entra Private Access** — Zero Trust Network Access for on-premises and private-cloud apps. Replaces VPN with per-application, Conditional-Access-driven, least-privilege access. No code changes to the app, and, unlike a VPN, no lateral movement across the whole network from a single compromised endpoint.

**Entra Internet Access** — a secure web gateway: web content filtering, cloud firewall, threat inspection, and token-theft protection for Microsoft 365 traffic.

Recent additions worth knowing:

- **Remote network connectivity** — branch offices connect over IPsec tunnels from a firewall or router, so security controls apply without deploying the client to every endpoint.
- **File-type content filtering** — block or restrict transfers of documents, spreadsheets and PDFs to generative AI and SaaS apps. Network-layer DLP.
- **AI Gateway with prompt injection protection** — real-time protection for enterprise generative AI applications, agents, and language models.
- **MCP Firewall** — visibility and Zero Trust enforcement over Model Context Protocol traffic between AI agents and remote MCP servers. It can discover shadow MCP servers, allow or block individual servers, tools, resources or prompts, and enforce protocol-version and transport requirements without modifying clients or servers.
- **External user support and BYOD support** in the Windows client.

---

## 14. Workload and Agent Identities

### Service principals and managed identities

| | Managed identity | Service principal with secret/cert |
|---|---|---|
| Credential management | Azure handles it entirely | You rotate it |
| Where it works | Azure-hosted resources only | Anywhere |
| Types | System-assigned (tied to a resource lifecycle), user-assigned (standalone, reusable) | n/a |

**Use a managed identity whenever the workload runs in Azure.** There is no credential to leak, and — as noted in §5 — managed identities and service principals are out of scope for interactive MFA enforcement, which makes them the correct migration target for any automation currently running under a user account.

**Workload Identity Premium** extends Conditional Access, risk detection, and access reviews to service principals — worth it, because non-human identities now vastly outnumber human ones in most tenants and are far less monitored.

### Entra Agent ID

Entra Agent ID gives each AI agent a unique, consistent identity across tools and environments, with the usual identity functions: authentication, authorization, and lifecycle management. That means Conditional Access, least-privilege enforcement, and activity monitoring apply to agents in the same way they apply to users.

Management has consolidated: the Agent registry and Agent collections blades in the Entra admin center were retired on 1 May 2026, with **Agent 365** in the Microsoft 365 admin center becoming the single catalogue. Agent ID and Agent 365 retain the full access and governance capability.

Licensing for agents follows the human model: P1 for Conditional Access for agents, P2 for ID Protection for agents, ID Governance for agent governance, and Internet Access for network controls — available standalone for customers not on E5 or E7.

**Security angle worth internalising:** agent identities are non-human, often over-permissioned, and rarely reviewed. Blueprint reuse across tenants and shadow MCP servers are both active research areas. Apply the same access reviews and least-privilege discipline you would to any privileged service account.

---

## 15. Monitoring, Logging, and Reporting

### The log types

| Log | Contains | Default retention (Free / P1–P2) |
|---|---|---|
| Sign-in logs | Interactive, non-interactive, service principal, managed identity sign-ins | 7 days / 30 days |
| Audit logs | Every directory change — who did what to which object | 7 days / 30 days |
| Provisioning logs | SCIM sync activity | 30 days |
| Identity Protection | Risk detections, risky users, risky sign-ins | 7 days / 30–90 days |

**30 days is not enough for incident response.** Route diagnostic settings to a **Log Analytics workspace**, a storage account for cheap long-term retention, or Microsoft Sentinel. Do this on day one of any deployment.

### Sign-in log fields that matter in an investigation

`correlationId` · `userPrincipalName` · `appDisplayName` · `resourceDisplayName` · `ipAddress` · `location` · `clientAppUsed` (this is how you spot legacy auth) · `conditionalAccessStatus` · `authenticationRequirement` · `riskLevelDuringSignIn` · `deviceDetail` · `authenticationDetails` · `status.errorCode`

Error codes worth memorising:

| Code | Meaning |
|---|---|
| 50126 | Invalid username or password — mass occurrences = password spray |
| 50053 | Account locked (smart lockout) |
| 50055 | Expired password |
| 50074 | Strong authentication required — user didn't complete MFA |
| 50076 / 50079 | MFA required / MFA registration required |
| 53003 | Blocked by Conditional Access |
| 53004 | User must enrol in MFA |
| 500121 | MFA request denied or timed out — often the user rejecting an attacker's push |
| 700016 | Application not found in directory |

A spike in **500121** across many users is one of the clearest indicators of an active MFA-fatigue campaign.

### Useful KQL

```kusto
// Password spray: many users, one source IP, all failing with 50126
SigninLogs
| where TimeGenerated > ago(24h)
| where ResultType == "50126"
| summarize FailedAttempts = count(), TargetedUsers = dcount(UserPrincipalName)
    by IPAddress, tostring(LocationDetails.countryOrRegion)
| where TargetedUsers > 10
| order by TargetedUsers desc
```

```kusto
// Legacy authentication still in use
SigninLogs
| where TimeGenerated > ago(30d)
| where ClientAppUsed in ("IMAP4", "POP3", "SMTP", "Other clients",
                          "Exchange ActiveSync", "Authenticated SMTP")
| summarize Attempts = count(), Apps = make_set(AppDisplayName)
    by UserPrincipalName, ClientAppUsed
| order by Attempts desc
```

```kusto
// Privileged role assignments in the last 7 days
AuditLogs
| where TimeGenerated > ago(7d)
| where OperationName has "Add member to role"
| extend Role = tostring(TargetResources[0].displayName)
| extend Actor = tostring(InitiatedBy.user.userPrincipalName)
| extend Target = tostring(TargetResources[2].userPrincipalName)
| project TimeGenerated, Actor, Target, Role, Result
| order by TimeGenerated desc
```

```kusto
// Break-glass account usage — should alert on ANY hit
SigninLogs
| where UserPrincipalName in ("breakglass1@contoso.onmicrosoft.com",
                              "breakglass2@contoso.onmicrosoft.com")
| project TimeGenerated, UserPrincipalName, IPAddress, AppDisplayName, ResultType
```

```kusto
// New credentials added to service principals — a persistence technique
AuditLogs
| where OperationName has_any ("Update application", "Update service principal")
| where TargetResources has "KeyDescription"
| project TimeGenerated, InitiatedBy, TargetResources, Result
```

### Built-in workbooks

Entra ID ships workbooks for sign-in analysis, Conditional Access gaps, MFA gaps, legacy authentication, and sensitive operations. The **Conditional Access Insights and Reporting** workbook is the one to use when evaluating report-only policies.

---

## 16. Automation with Microsoft Graph

### Module situation

The `MSOnline` and `AzureAD` / `AzureAD-Preview` PowerShell modules are **retired** — they stopped working from mid-October 2025. Everything below uses **Microsoft Graph PowerShell**. If you find a script online using `Connect-MsolService` or `Connect-AzureAD`, it is dead code.

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
Connect-MgGraph -Scopes "User.Read.All","Group.ReadWrite.All",
                        "Policy.Read.All","Directory.Read.All",
                        "RoleManagement.Read.Directory"
Get-MgContext
```

### Everyday operations

```powershell
# Create a user
$password = @{
    Password                      = "<generate-a-strong-one>"
    ForceChangePasswordNextSignIn = $true
}
New-MgUser -DisplayName "Ada Lovelace" `
           -UserPrincipalName "ada@contoso.onmicrosoft.com" `
           -MailNickname "ada" `
           -AccountEnabled `
           -UsageLocation "AU" `
           -PasswordProfile $password

# Dynamic group
New-MgGroup -DisplayName "AU Engineering" `
            -MailEnabled:$false `
            -MailNickname "au-eng" `
            -SecurityEnabled `
            -GroupTypes "DynamicMembership" `
            -MembershipRule '(user.department -eq "Engineering") and (user.country -eq "AU")' `
            -MembershipRuleProcessingState "On"

# Who holds Global Administrator?
$role = Get-MgDirectoryRole -Filter "displayName eq 'Global Administrator'"
Get-MgDirectoryRoleMember -DirectoryRoleId $role.Id |
    ForEach-Object { (Get-MgUser -UserId $_.Id).UserPrincipalName }
```

### Auditing your own tenant

```powershell
# Users with no MFA method registered
Get-MgReportAuthenticationMethodUserRegistrationDetail -All |
    Where-Object { -not $_.IsMfaRegistered } |
    Select-Object UserPrincipalName, IsAdmin, IsSsprRegistered |
    Export-Csv .\mfa-gaps.csv -NoTypeInformation

# Service principals with credentials expiring in the next 60 days
Get-MgServicePrincipal -All -Property "id,displayName,passwordCredentials,keyCredentials" |
    ForEach-Object {
        $sp = $_
        @($sp.PasswordCredentials) + @($sp.KeyCredentials) |
            Where-Object { $_.EndDateTime -and
                           $_.EndDateTime -lt (Get-Date).AddDays(60) } |
            Select-Object @{n='App';e={$sp.DisplayName}},
                          @{n='Expires';e={$_.EndDateTime}}
    }

# Application permissions granted tenant-wide (the dangerous ones)
Get-MgServicePrincipal -All | ForEach-Object {
    $sp = $_
    Get-MgServicePrincipalAppRoleAssignment -ServicePrincipalId $sp.Id -ErrorAction SilentlyContinue |
        Select-Object @{n='Client';e={$sp.DisplayName}}, AppRoleId, ResourceDisplayName
}
```

### Conditional Access as code

```powershell
# Export every CA policy to JSON — commit this to Git
$stamp = Get-Date -Format "yyyy-MM-dd"
New-Item -ItemType Directory -Path ".\ca-policies\$stamp" -Force | Out-Null

Get-MgIdentityConditionalAccessPolicy -All | ForEach-Object {
    $safeName = $_.DisplayName -replace '[\\/:*?"<>|]', '_'
    $_ | ConvertTo-Json -Depth 12 |
        Out-File ".\ca-policies\$stamp\$safeName.json" -Encoding utf8
}
```

Committing this on a schedule gives you a diffable history of your security perimeter — invaluable both for change control and for answering "when did this policy change?" during an incident.

### Raw Graph calls

```http
GET https://graph.microsoft.com/v1.0/users?$filter=accountEnabled eq true&$select=displayName,userPrincipalName,userType&$top=999
GET https://graph.microsoft.com/v1.0/auditLogs/signIns?$filter=status/errorCode eq 50126&$top=50
GET https://graph.microsoft.com/beta/identity/conditionalAccess/policies
GET https://graph.microsoft.com/v1.0/directoryRoles
```

Use **Graph Explorer** (`developer.microsoft.com/graph/graph-explorer`) to prototype before scripting. Note the `v1.0` vs `beta` distinction — plenty of identity features are still beta-only, and beta endpoints can change without notice, so don't put them in production automation without a plan.

A newer `groupAnalytics` API surfaces group member counts, owner counts, and expiration status directly, replacing the custom scripts people used to write for group hygiene reporting.

---

## 17. Attack Scenarios and Defences

| Attack | How it works | Primary defence |
|---|---|---|
| **Password spray** | One common password against thousands of accounts, staying under lockout thresholds | Block legacy auth, smart lockout, banned password list, MFA |
| **Adversary-in-the-middle (AiTM)** | A reverse proxy (Evilginx, EvilProxy) relays the real login page and captures the **session cookie** after MFA succeeds | Phishing-resistant MFA (passkeys/CBA), token protection, compliant-device requirement, CAE |
| **MFA fatigue / push bombing** | Repeated push notifications until the user approves one | Number matching, additional context in Authenticator, alert on error 500121 |
| **Device code phishing** | Victim is convinced to enter an attacker-generated device code at a legitimate Microsoft URL | CA policy blocking the device code flow where it isn't needed |
| **Illicit consent grant** | Malicious multi-tenant app requests OAuth scopes; user consents; attacker retains access without any password | Restrict user consent to verified publishers and low-risk scopes, admin consent workflow, audit `Consent to application` events |
| **Service principal credential abuse** | Attacker with Application Administrator adds a new secret to a privileged SP and authenticates as it | Treat Application Administrator as tier-0, alert on credential-add audit events, prefer certificates |
| **Golden SAML** | Compromise of AD FS token-signing key lets the attacker mint arbitrary tokens | Move to PHS/cloud auth, protect AD FS as tier-0, monitor for token issuer anomaly detections |
| **On-prem → cloud pivot** | Compromised AD account is synced into a cloud-privileged group | Never sync privileged AD groups; separate cloud-only admin accounts |
| **Over-permissioned agent/workload identity** | Non-human identity with tenant-wide application permissions, never reviewed | Workload Identity Premium, access reviews on SPs, least-privilege scopes, MCP Firewall |

Microsoft's 2025 Digital Defense Report found that around 80% of MFA-bypass breaches involved session-token theft via adversary-in-the-middle attacks. That single statistic is the argument for phishing-resistant methods: traditional MFA stops credential replay, but it does not stop cookie theft.

---

## 18. Hardening Checklist

### Tier 0 — do these first

- [ ] Two break-glass accounts, cloud-only, excluded from all CA policies, MFA registered, credentials physically secured, alert on any sign-in
- [ ] Fewer than 5 permanent Global Administrators (target: 2 break-glass + PIM-eligible for everyone else)
- [ ] Cloud-only admin accounts, never synced from on-premises AD
- [ ] Block legacy authentication tenant-wide
- [ ] MFA required for all users and all admins
- [ ] Diagnostic settings exporting logs to Log Analytics / Sentinel

### Identity hygiene

- [ ] Password hash sync enabled (even as backup under PTA or federation)
- [ ] Custom banned password list populated with org-specific terms
- [ ] SSPR enabled with two required methods
- [ ] SMS and voice deprecated as MFA methods
- [ ] Passkey / FIDO2 rollout under way for privileged users
- [ ] User consent restricted to verified publishers and low-risk permissions
- [ ] Admin consent workflow enabled
- [ ] Guest user permissions restricted; tenant restrictions v2 configured
- [ ] Users cannot register applications (unless there is a deliberate reason)

### Policy and governance

- [ ] All CA policies named systematically and exported to Git
- [ ] CA policies tested in report-only before enforcement
- [ ] PIM configured for every privileged role with MFA, justification, and approval
- [ ] Quarterly access reviews on privileged roles and guest accounts
- [ ] Lifecycle workflows handling the leaver process
- [ ] Service principal credentials inventoried with expiry alerting
- [ ] Application permissions (not delegated) reviewed and justified

### Detection

- [ ] Alert on break-glass sign-in
- [ ] Alert on Global Administrator role assignment
- [ ] Alert on new credentials added to a service principal
- [ ] Alert on Conditional Access policy modification or deletion
- [ ] Alert on the Azure "elevate access" toggle being used
- [ ] Risk-based CA policies live (P2), migrated off the legacy Identity Protection policies

---

## 19. 2025–2026 Breaking Changes and Deadlines

| Date | Change | Action |
|---|---|---|
| Oct 2024 | MFA enforced for Azure portal, Entra and Intune admin centers (Phase 1; completed Mar 2025) | Done — verify no gaps |
| Feb 2025 | MFA enforcement begins for Microsoft 365 admin center | Verify |
| Jul 2025 | Security defaults stop requiring MFA registration from B2B guests (new tenants) | Informational |
| Mid-Oct 2025 | `AzureAD` and `AzureAD-Preview` PowerShell modules retired and non-functional | Migrate all scripts to Microsoft Graph PowerShell |
| 1 Oct 2025 | MFA enforcement extends to Azure CLI, Azure PowerShell, mobile app, IaC tools, control-plane REST APIs for create/update/delete | Move automation to service principals or managed identities |
| 9 Feb 2026 | Sign-in to Microsoft 365 admin center blocked without completed MFA | Confirm every admin has a working method |
| ~May 2026 | Passkey policy gets a dedicated 20 KB allocation; up to 10 passkey profiles per tenant | Revisit passkey targeting strategy |
| 1 May 2026 | Agent registry and Agent collections blades retired from Entra admin center; Agent 365 becomes the catalogue | No action required; update runbooks |
| 1 May 2026 | Microsoft 365 E7 generally available with the full Entra Suite | Licensing review |
| Jun 2026 | Hard-match behaviour change for synced objects | Check guidance before bulk SoA conversions |
| 13 Jul 2026 | Enforcement completes for MFA on passwordless credential registration | Verify CA policies targeting that user action |
| 1 Jul 2026 | Final deadline for MFA enforcement postponement requests — no further extensions | Nothing left to defer |
| 1 Oct 2026 | Identity Protection UI for the legacy risk policies retired | Migrate risk policies into Conditional Access now |

Verify each of these against Microsoft's official release notes before acting — dates in this space move, and sovereign clouds run on a separate schedule.

---

## 20. Hands-On Labs

Each lab is self-contained. Run them in a lab tenant, in order.

### Lab 1 — Tenant baseline

**Goal:** a tenant you can safely experiment in.

1. Add a custom domain (or note the default `.onmicrosoft.com`).
2. Create `breakglass1@<tenant>.onmicrosoft.com` and `breakglass2@...`. Assign Global Administrator permanently. Generate 64-character random passwords. Register an MFA method on each — required under current enforcement.
3. Create a group `CA-Exclusion-BreakGlass` and add both.
4. Create 10 test users across two departments and two countries.
5. Create your own admin account (separate from your daily user) and make it PIM-eligible for Global Administrator.

**Verify:** `Get-MgDirectoryRoleMember` shows exactly your two break-glass accounts as permanent GAs.

### Lab 2 — Groups and licensing

1. Create a dynamic security group with the rule `(user.department -eq "Engineering")`.
2. Watch the membership populate. Time it — this is why dynamic groups can't be used for break-glass.
3. Assign a licence to the group and confirm inherited assignment on a member.
4. Change a user's department and observe removal from the group and reclamation of the licence.

**Verify:** licence assignment shows as inherited, not direct.

### Lab 3 — Conditional Access, safely

1. Create **CA001 — Block legacy authentication**, targeting all users, excluding `CA-Exclusion-BreakGlass`, condition `Client apps = Exchange ActiveSync + Other clients`, grant = Block. **Report-only.**
2. Create **CA002 — Require MFA for admins**, targeting directory roles, excluding break-glass, grant = require MFA. **Report-only.**
3. Use **What If** to simulate: your test user, Office 365 Exchange Online, from a foreign IP, using a legacy client.
4. Sign in as a test user from a browser and check the sign-in log's Conditional Access tab for the report-only result.
5. Only then flip CA001 to On.

**Verify:** the Conditional Access Insights workbook shows what would have been blocked.

### Lab 4 — PIM

1. Enable PIM for Global Administrator: maximum 2 hours, require MFA, require justification, require approval.
2. Assign your admin account as **Eligible** (not Active).
3. Activate the role. Note the justification prompt and the approval flow.
4. Attempt a privileged action before activating and after. Compare.
5. Review the PIM audit history.

**Verify:** the activation appears in the audit log with your justification text.

### Lab 5 — Identity Protection (P2)

1. Create a CA policy: sign-in risk = High → Block; sign-in risk = Medium → require MFA.
2. Create a second: user risk = High → require secure password change.
3. Generate a low-risk detection by signing in over Tor or a commercial VPN with a test account.
4. Investigate in the Risky Sign-ins report. Trace the detection type and the CA outcome.
5. Dismiss the risk and confirm the user's risk state clears.

**Verify:** the sign-in log entry shows `riskLevelDuringSignIn` and the CA policy that fired.

### Lab 6 — App registration and Graph

1. Register an application. Add the `User.Read.All` **application** permission. Grant admin consent.
2. Upload a self-signed certificate instead of creating a client secret.
3. Authenticate as the app and list users:

```powershell
$cert = Get-ChildItem Cert:\CurrentUser\My\<thumbprint>
Connect-MgGraph -ClientId "<app-id>" -TenantId "<tenant-id>" -Certificate $cert
Get-MgUser -Top 10 | Select-Object DisplayName, UserPrincipalName
```

4. Find the app's sign-in in the **service principal sign-ins** log — a different tab from interactive sign-ins, and one many analysts forget exists.

**Verify:** you can enumerate users with no user context at all. Reflect on what an over-permissioned app registration means.

### Lab 7 — Access reviews and entitlement management

1. Create an access package bundling one group and one app.
2. Set an approval policy requiring manager approval, 30-day duration.
3. Request access as a test user; approve as the manager.
4. Create an access review on the same group with self-review and `remove access` on no response.
5. Let it complete without responding and confirm the removal.

**Verify:** the user loses group membership automatically.

### Lab 8 — Detection engineering

1. Enable diagnostic settings → Log Analytics for SigninLogs and AuditLogs.
2. Simulate a password spray: 15 failed sign-ins against different test users from one source.
3. Run the KQL from §15 and confirm the detection fires.
4. Build an alert rule on break-glass sign-in and trigger it.

**Verify:** you receive the alert and can trace the full event chain.

---

## 21. Certification Mapping

| Section | SC-900 | SC-300 | AZ-104 |
|---|---|---|---|
| §1–3 Concepts and objects | ✅✅ | ✅✅ | ✅✅ |
| §4 Licensing | ✅ | ✅ | ✅ |
| §5 Authentication | ✅✅ | ✅✅✅ | ✅ |
| §6 Roles and PIM | ✅ | ✅✅✅ | ✅✅ |
| §7 Conditional Access | ✅✅ | ✅✅✅ | ✅ |
| §8 Identity Protection | ✅ | ✅✅✅ | — |
| §9 Governance | ✅ | ✅✅✅ | — |
| §10 Hybrid identity | ✅ | ✅✅✅ | ✅✅ |
| §11 Applications and SSO | ✅ | ✅✅✅ | ✅ |
| §12 External identities | ✅ | ✅✅ | ✅ |
| §15 Monitoring | ✅ | ✅✅ | ✅✅ |

**SC-300 (Identity and Access Administrator)** is the flagship exam for this material. **SC-900** is the fundamentals-level entry point. **AZ-104** covers Entra ID only as one domain among several.

---

## 22. Glossary

| Term | Definition |
|---|---|
| **AiTM** | Adversary-in-the-middle — proxy-based phishing that steals the post-MFA session cookie |
| **CAE** | Continuous Access Evaluation — near-real-time token revocation on critical events |
| **CBA** | Certificate-Based Authentication |
| **Claim** | An assertion about a subject inside a token (name, role, group membership) |
| **Consent** | A user or admin authorising an app to act with specified permissions |
| **Delegated permission** | App acts as the signed-in user; effective rights are the intersection of both |
| **Application permission** | App acts as itself, tenant-wide, with no user context |
| **Entra Connect / Cloud Sync** | The two tools for syncing on-premises AD to Entra ID |
| **MAU** | Monthly Active User — the billing model for external identities |
| **Managed identity** | An Azure-managed service principal with no credential for you to handle |
| **PHS / PTA** | Password Hash Sync / Pass-through Authentication |
| **PIM** | Privileged Identity Management — just-in-time role activation |
| **Service principal** | The local instance of an application inside your tenant |
| **SCIM** | System for Cross-domain Identity Management — the user-provisioning standard |
| **SoA** | Source of Authority — which directory owns an object |
| **SSE** | Security Service Edge — Global Secure Access's product category |
| **Tenant** | An isolated instance of Entra ID representing one organisation |
| **Token protection** | Binds a refresh token to a device, defeating token replay |
| **UPN** | User Principal Name — the sign-in identifier |
| **ZTNA** | Zero Trust Network Access — per-app access replacing VPN |

---

## 23. Further Reading

**Official**
- Microsoft Entra documentation — `learn.microsoft.com/entra`
- Microsoft Entra blog, "What's new" monthly series — `techcommunity.microsoft.com/category/microsoft-entra`
- Microsoft Entra release notes and known issues
- Microsoft Graph API reference — `learn.microsoft.com/graph`
- Microsoft Digital Defense Report — annual threat data

**Community tooling**
- **Maester** — pester-based, automated Entra ID security configuration testing. Run it against your tenant on a schedule
- **MSIdentityTools** PowerShell module — including `Export-MsIdAzureMfaReport`
- **Graph X-Ray** browser extension — shows the Graph call behind any portal action
- **Entra Exporter** — full tenant configuration export for backup and diffing

**Blogs worth following**
- Merill Fernando (entra.news)
- Practical 365
- Jan Bakker (janbakker.tech)
- Cloud Brothers (Fabian Bader)
- Thomas Naunheim on identity security architecture

---

## Contributing

Corrections and additions welcome. Entra ID changes monthly, so if you find something stale, open an issue with a link to the current Microsoft documentation.

## Licence

Released under CC BY 4.0. Microsoft, Entra, and Azure are trademarks of Microsoft Corporation; this is an independent guide and is not affiliated with or endorsed by Microsoft.
