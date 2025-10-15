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

