# Chapter 4: Communication and Network Security (Domain 4)

**Domain Weight**: 13% (One of the most technical domains in the CISSP exam)

**Purpose of this Domain**:  
This domain covers the secure design, implementation, and management of network architectures, components, and communication channels. It emphasizes applying security principles to protect data in transit and ensure resilient network infrastructure.

---

## 4.1 Apply Secure Design Principles in Network Architectures

### Core Concepts

#### 1. Network Models
- **OSI Model** (7 Layers) – Most important for CISSP
  - **Layer 1 – Physical**: Cables, signals, hubs, repeaters, electrical/optical characteristics.
  - **Layer 2 – Data Link**: MAC addressing, switches, bridges, VLANs, ARP, PPP, Frame Relay.
  - **Layer 3 – Network**: IP addressing (IPv4/IPv6), routers, routing protocols (OSPF, BGP), ICMP, IPsec.
  - **Layer 4 – Transport**: TCP (reliable, connection-oriented), UDP (connectionless), ports.
  - **Layer 5 – Session**: Session management, RPC, NetBIOS.
  - **Layer 6 – Presentation**: Data formatting, encryption, compression (SSL/TLS, JPEG).
  - **Layer 7 – Application**: User-facing protocols (HTTP, FTP, SMTP, DNS).

- **TCP/IP Model** (4 Layers)
  - Application → Transport → Internet → Network Interface (Link).

#### 2. IP Addressing
- **IPv4**: 32-bit, classes (A/B/C), CIDR, subnetting, NAT, private addresses.
- **IPv6**: 128-bit, built-in IPsec support, addressing types (Unicast, Multicast, Anycast, Broadcast eliminated).

#### 3. Secure Design Principles
- Defense in Depth
- Network Segmentation & Micro-segmentation
- Zero Trust Architecture
- Least Privilege
- High Availability & Redundancy
- Fail Secure / Fail Closed
- Bastion Hosts

#### 4. Implications of Multilayer Protocols
- Tunneling (e.g., VPNs)
- Covert channels
- Complexity in inspection (firewalls/IDS may miss tunneled traffic)

#### 5. Converged Protocols
- **VoIP** (Voice over IP)
- **iSCSI** (Storage over IP)
- **FCoE** (Fibre Channel over Ethernet)
- InfiniBand over Ethernet

**Exam Tip**: Master OSI vs TCP/IP mapping and which security controls operate at each layer.

---

## 4.2 Secure Network Components

### Network Architecture Elements
- **Perimeter Security** (DMZ, dual firewalls)
- **Network Segmentation** (VLANs, SDN, VXLAN)
- **SDN (Software-Defined Networking)** – Separation of control and data plane
- **SD-WAN** – Secure, optimized WAN connectivity

### Key Network Devices & Components

#### 1. Hardware Devices
- **Hubs** — Layer 1, insecure (broadcast everything).
- **Switches** — Layer 2, MAC learning, VLAN support.
- **Routers** — Layer 3, routing decisions.
- **Firewalls**:
  - Packet Filtering
  - Stateful Inspection
  - Next-Generation (NGFW) – Application awareness, IPS, URL filtering.
- **Proxy Servers** (Forward & Reverse)
- **Load Balancers**
- **Modems & CSU/DSU**

#### 2. Security Appliances
- **Intrusion Detection/Prevention Systems (IDS/IPS)**:
  - Network-based (NIDS/NIPS)
  - Host-based (HIDS/HIPS)
  - Signature-based vs Anomaly-based
- **Network Access Control (NAC)** – 802.1X, posture assessment.
- **Endpoint Security** (EDR, host firewalls).

#### 3. Wireless Components
- Access Points (Fat vs Thin)
- Wireless Security Standards:
  - WEP (broken)
  - WPA / WPA2 / **WPA3** (best)
  - 802.1X / EAP methods (PEAP, EAP-TLS, EAP-TTLS)
- Wireless Attacks: Evil Twin, Rogue AP, WPS attacks, KRACK.

#### 4. Other Components
- Bastion Hosts
- Honeypots / Honeynets
- VPN Concentrators
- Content Distribution Networks (CDN)

**Exam Tip**: Know differences between switches vs routers, stateful vs stateless firewalls, and NAC functions.

---

## 4.3 Implement Secure Communication Channels According to Design

### Secure Protocols by OSI Layer

| Layer | Secure Protocols |
|-------|------------------|
| 7     | HTTPS, S/MIME, SFTP, SNMPv3 |
| 6     | TLS/SSL |
| 4     | TLS, DTLS |
| 3     | IPsec (AH + ESP) |
| 2/3   | SSH, WireGuard |

### Major Secure Technologies

#### 1. VPN Technologies
- **IPsec** – Tunnel mode & Transport mode (AH for integrity/auth, ESP for confidentiality+integrity).
- **SSL/TLS VPN** – Clientless or client-based.
- **Site-to-Site vs Remote Access VPN**.
- L2TP/IPsec, PPTP (legacy, avoid), WireGuard.

#### 2. Remote Access
- Dial-up (legacy)
- RADIUS / TACACS+ / Diameter (AAA protocols)
- 802.1X for port-based access control

#### 3. Voice & Multimedia
- Secure VoIP (SRTP + SIP over TLS)
- Challenges: Latency, jitter, packet loss.

#### 4. Email Security
- S/MIME
- PGP / OpenPGP
- DKIM, SPF, DMARC

#### 5. Other Channels
- Secure File Transfer: SFTP, FTPS, SCP
- Web Services: WS-Security
- Database: TLS-encrypted connections

### Key Attack Vectors & Mitigations
- Eavesdropping / Sniffing → Encryption
- Man-in-the-Middle (MitM) → Mutual authentication + certificates
- DDoS → Redundancy + rate limiting
- Replay attacks → Timestamps & nonces
- DNS Poisoning → DNSSEC

**Exam Tip**: Understand when to use IPsec vs TLS and differences between authentication protocols (RADIUS vs TACACS+ vs Diameter).

---

## Summary Table – Key Focus Areas

| Subdomain | Main Topics | Exam Emphasis |
|---------|-------------|---------------|
| 4.1     | OSI/TCP/IP, IPv4/IPv6, Secure Protocols | Very High |
| 4.2     | Firewalls, Switches, IDS/IPS, NAC, Wireless | High |
| 4.3     | VPNs, IPsec, TLS, Remote Access, Secure Protocols | Very High |

**CISSP Mindset for Domain 4**:
- Security must be **built into** the network design, not added later.
- Always prefer **defense in depth** and **least privilege**.
- Data in transit must be protected using strong encryption and proper key management.

**Study Recommendations**:
- Memorize OSI layers and example protocols.
- Practice subnetting and understand IPv6 advantages.
- Know differences: IPsec vs SSL VPN, WPA2 vs WPA3, RADIUS vs TACACS+.
- Draw network diagrams with security controls.
