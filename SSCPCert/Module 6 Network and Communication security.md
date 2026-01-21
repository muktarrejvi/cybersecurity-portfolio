
# SSCP – Domain 6: Network and Communications Security

This document provides **human-style detailed key takeaways**, explanations, and **practical examples** for **SSCP Domain 6**. The content is written as a learner would summarize after watching lectures or reading study material.

---

## Domain 6.0: Network and Communications Security – Overview

Network and Communications Security focuses on protecting **data in transit**, **network infrastructure**, and **communication channels** from unauthorized access, misuse, modification, or disruption.  
This domain emphasizes **network fundamentals, attacks, access controls, segmentation, security devices, and wireless security**.

---

## 6.1 Understand and Apply Fundamental Concepts of Networking

### Key Concepts
- **Network**: A group of connected devices that communicate using agreed protocols.
- **Protocols**: Rules for communication (e.g., TCP/IP, UDP).
- **OSI Model**: Conceptual 7-layer model used to understand how data flows.
- **TCP/IP Model**: Practical 4-layer model used on the internet.

### Example
When a user opens a website:
- Application Layer → HTTP request
- Transport Layer → TCP ensures reliable delivery
- Network Layer → IP routes packets
- Data Link & Physical → Ethernet/Wi-Fi transmits bits

### Key Takeaway
> Understanding networking fundamentals helps security professionals identify **where attacks occur** and **which controls to apply**.

---

## 6.2 Understand Network Attacks and Countermeasures

### Common Network Attacks

#### 1. Distributed Denial of Service (DDoS)
- Overwhelms a server or network with massive traffic.
- Often launched using botnets.

**Example**:  
A shopping website crashes during a sale due to millions of fake requests.

**Countermeasure**:
- Content Delivery Networks (CDNs)
- Rate limiting
- Traffic filtering

---

#### 2. Man-in-the-Middle (MITM)
- Attacker secretly intercepts communication.
- Common in unsecured Wi-Fi networks.

**Example**:  
Attacker captures login credentials at a public café Wi-Fi.

**Countermeasure**:
- Encryption (HTTPS, TLS)
- VPN usage
- Certificate validation

---

#### 3. DNS Poisoning
- Corrupts DNS records to redirect users to malicious sites.

**Example**:  
Typing `bank.com` redirects to a fake banking website.

**Countermeasure**:
- DNSSEC
- Secure DNS resolvers
- Monitoring DNS changes

---

### Key Takeaway
> Most network attacks exploit **trust, lack of encryption, or availability weaknesses**.

---

## 6.3 Manage Network Access Controls

### Network Access Control (NAC)

Controls **who can access** the network and **what they can access**.

---

### Standards and Protocols

#### IEEE 802.1X
- Port-based network access control.
- Requires authentication before access is granted.

**Example**:
Employees must authenticate before connecting to office Wi-Fi.

---

#### RADIUS
- Centralized authentication protocol.
- Commonly used for VPNs and Wi-Fi.

**Key Feature**:
- Authentication and authorization.

---

#### TACACS+
- Similar to RADIUS but more granular.
- Separates authentication, authorization, and accounting.

**Used for**:
- Network device administration (routers, switches).

---

### Remote Access Operation

#### Virtual Private Network (VPN)
- Encrypted tunnel over public networks.

**Example**:
Employees securely access company systems from home.

---

#### Thin Client
- Minimal local processing.
- Relies on centralized servers.

**Benefit**:
- Easier security management.

---

### Key Takeaway
> Strong access controls ensure **only authenticated and authorized users** access the network.

---

## 6.4 Manage Network Security

### Placement of Network Devices

#### Inline
- Actively inspects traffic.
- Can block malicious packets.

**Example**: Firewall placed between LAN and internet.

---

#### Passive
- Monitors traffic only.
- Does not block.

**Example**: IDS connected to a network tap.

---

#### Virtual
- Deployed in cloud or virtual environments.

**Example**: Virtual firewall in AWS.

---

### Segmentation

#### Physical vs Logical
- Physical: Separate hardware
- Logical: VLANs, ACLs

---

#### VLAN
- Separates networks logically on the same switch.

**Example**:
Finance VLAN isolated from Guest VLAN.

---

#### ACL
- Rules that allow or deny traffic.

---

#### Firewall Zones
- Trust levels (Internal, DMZ, External).

---

#### Micro-segmentation
- Very fine-grained segmentation.

**Used in**:
- Cloud and zero-trust environments.

---

### Secure Device Management
- Patch management
- Strong authentication
- Disable unused services
- Secure configuration backups

---

### Key Takeaway
> Segmentation limits **lateral movement** and reduces **attack impact**.

---

## 6.5 Operate and Configure Network-Based Security Devices

### Firewalls
- Control traffic based on rules.

#### Filtering Methods
- Packet filtering
- Stateful inspection
- Application-level filtering

---

### Proxies
- Act as intermediaries.
- Hide internal systems.

---

### Web Application Firewall (WAF)
- Protects web applications.
- Blocks SQL injection, XSS.

---

### IDS vs IPS

| Feature | IDS | IPS |
|------|-----|-----|
| Detects attacks | Yes | Yes |
| Blocks attacks | No | Yes |
| Placement | Passive | Inline |

---

### Routers and Switches
- Routers: Connect networks
- Switches: Connect devices

**Security Features**:
- Port security
- Access control
- Logging

---

### Traffic-Shaping Devices

#### Load Balancing
- Distributes traffic across servers.

#### WAN Optimization
- Improves performance over long distances.

---

### Key Takeaway
> Security devices must be **correctly placed and configured** to be effective.

---

## 6.6 Secure Wireless Communications

### Wireless Technologies

#### Wi-Fi
- Most common wireless network.

#### Cellular Networks
- 4G/5G mobile communication.

#### Bluetooth
- Short-range communication.

#### NFC
- Very short-range (payments, access cards).

---

### Authentication and Encryption Protocols

#### WEP
- Weak and insecure.
- Easily cracked.

---

#### WPA / WPA2 / WPA3
- Stronger encryption.
- WPA3 is the most secure.

---

#### EAP
- Framework for authentication.
- Used with 802.1X.

---

### Internet of Things (IoT)

**Risks**:
- Weak passwords
- No patching
- Always connected

**Security Controls**:
- Network isolation
- Strong authentication
- Regular updates

---

### Key Takeaway
> Wireless networks increase convenience **but significantly increase attack surface**.

---

## Final Exam-Focused Summary

- Understand **how networks work before securing them**
- Focus on **attacks + countermeasures**
- Memorize **RADIUS vs TACACS+ vs 802.1X**
- Know **IDS vs IPS**
- Segmentation is critical for **damage containment**
- Wireless security is a **high-risk exam area**

---

**End of Domain 6 – SSCP**
