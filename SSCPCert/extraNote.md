
## RSA Key Length Comparison

- **1024-bit** ❌ Insecure (deprecated)  
- **2048-bit** ✅ Current standard minimum (good for today)  
- **3072-bit** ✅ Stronger long-term protection with reasonable performance  
- **4096-bit** 🔒 Very strong but heavier performance impact  

According to modern cryptographic guidance (e.g., NIST), **RSA 3072-bit** provides security comparable to **128-bit symmetric encryption** and is considered suitable for long-term protection.

### Containerization (C)

Containerization effectively isolates corporate applications and data from personal applications on the same device.

This separation:
- Prevents corporate data leakage
- Maintains security boundaries
- Allows users to continue personal use of the device

It is commonly used in BYOD (Bring Your Own Device) environments to protect organizational data while preserving user privacy

### Key Metric: Number of Reported Data Breaches

The number of data breaches reported since implementation is a key metric used to evaluate the effectiveness of a new data encryption protocol.  

This metric directly indicates whether the protocol is successfully protecting sensitive data.

**Rationale:**
- Fewer breaches after implementation may suggest improved protection.
- An increase or no change in breaches may indicate weaknesses in configuration, implementation, or complementary controls.
- Should be evaluated alongside other security metrics for a comprehensive assessment.

Implementing **digital certificates** provides a **secure** and **robust** method for **device authentication**. **Certificates** can uniquely **identify** and **verify** **authorized devices** by **cryptographically binding** them to a specific **identity**.

Using a **redundant array of independent disks (RAID)** configuration provides **redundancy** and **fault tolerance**, ensuring **high availability** of the **shared storage**. If one **disk fails**, others can continue to provide **data access** without interruption.

**Minimization of harm** is an ethical principle guiding the investigator to avoid unnecessary damage to individuals' **reputations**, **privacy**, and **well-being**, especially in **non-criminal matters**.

# RFID Badge Access and Logging

Utilizing **RFID badges** with **access logs** provides the most **comprehensive solution** as it not only **controls access** but also **records detailed logs** of **who has entered and exited the server rooms**, which is crucial for **auditing** and **security purposes**.

# Virtual Machine Performance Degradation

The most likely cause of **performance degradation** in this scenario is **insufficient physical RAM** for the **virtual machines**. When the **hypervisor** is **overcommitted**, it means more virtual resources (such as **RAM**) are allocated to **VMs** than are physically available. This results in **memory swapping** and increased use of **disk storage** as virtual memory, which can **significantly slow down** the virtual environment.

# Mobile Application Management (MAM)

**Mobile Application Management (MAM)** is designed to **manage** and **secure corporate applications**, enabling organizations to enforce **policies** and **controls** specifically on **work-related apps** while **safeguarding personal data** and **personal applications** on the same device.


# TLS Downgrade Attack

**Transport Layer Security (TLS)** can be susceptible to **downgrade attacks**, where an **attacker** forces a connection to use an **older, less secure protocol version**, such as **SSL** or earlier TLS versions. This exposes the communication to known **vulnerabilities** and **security risks**.

# Transport Layer Overview

The **Transport Layer** is responsible for **end-to-end communication** between devices on a network. It ensures **reliable data delivery** and can employ protocols like **TLS (Transport Layer Security)** to provide **encryption** and maintain **data integrity** during transmission.

# Virtual Appliance Performance Issue

The most likely cause of **underperformance** is **insufficient virtual CPU (vCPU) resources** allocated to the **appliance**. **Virtual appliances** rely on adequate **CPU resources** to efficiently **process traffic** and execute their **tasks**. Without proper allocation, the appliance may experience **delays**, **packet drops**, or overall **performance degradation**.

> **Note:** Always ensure that the **vCPU allocation** matches the appliance's **recommended specifications**. Monitoring **CPU usage** and scaling resources appropriately can prevent **bottlenecks** and maintain **optimal performance**.

# Automated Threat Mitigation in Ransomware Attacks

**Automated threat mitigation** plays a crucial role during a potential **ransomware attack**, allowing an **Endpoint Detection and Response (EDR) system** to **swiftly isolate**, **contain**, and **neutralize threats**, thereby **minimizing operational and data damage**.

**Keywords:** `automated threat mitigation`, `ransomware attack`, `EDR system`, `isolate`, `neutralize threats`, `minimizing damage`

> **Paraphrased Insight:**  
> Using **automated defenses** in EDR solutions ensures that ransomware is **detected and contained quickly**, reducing the risk of widespread **data loss** or disruption. This approach enhances the organization's **incident response effectiveness** and **business continuity**.

# Phishing vs Spear Phishing

- **Phishing**: A **generic** attack that targets a **large group of people**, usually via **mass emails**, aiming to trick recipients into revealing **sensitive information** such as passwords, financial details, or login credentials.

- **Spear Phishing**: A **targeted** and **personalized** form of phishing that focuses on a **specific individual or organization**. Attackers often **impersonate trusted contacts** like a **CEO, IT administrator, or colleague** to increase the chances of success.
