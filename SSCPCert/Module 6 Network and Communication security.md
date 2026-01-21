# SSCP Domain 6 — Network and Communications Security

This domain focuses on how data moves across networks, how attackers exploit networks, and how security controls protect network communications.

---

## 6.1 Fundamental Networking Concepts

### OSI Model (7 Layers)

| Layer | Name | Key Function | Common Protocols / Examples |
|-----|------|-------------|-----------------------------|
| 7 | Application | User-facing network services | HTTP, HTTPS, FTP, SMTP, DNS |
| 6 | Presentation | Encryption, compression, formatting | TLS/SSL, ASCII, JPEG |
| 5 | Session | Session establishment & management | NetBIOS session, RPC |
| 4 | Transport | Reliable delivery & flow control | TCP, UDP |
| 3 | Network | Logical addressing & routing | IP, ICMP, IPSec |
| 2 | Data Link | MAC addressing & framing | Ethernet, ARP, VLAN (802.1Q) |
| 1 | Physical | Transmission of raw bits | Cables, voltages, fiber |

---

### TCP/IP Model (4 Layers)

| TCP/IP Layer | Corresponding OSI Layers | Protocol Examples |
|-------------|-------------------------|------------------|
| Application | OSI 7,6,5 | HTTP, HTTPS, FTP, SMTP, DNS |
| Transport | OSI 4 | TCP, UDP |
| Internet | OSI 3 | IP, ICMP, IPSec |
| Network Access | OSI 2,1 | Ethernet, ARP, Wi-Fi |

---
## UTP Cable Categories and Maximum Speed

| Category | Max Speed | Max Bandwidth | Typical Use |
|---------|-----------|---------------|-------------|
| Cat 1 | No data (Voice only) | N/A | Telephone lines (obsolete) |
| Cat 2 | 4 Mbps | 4 MHz | Old Token Ring (obsolete) |
| Cat 3 | 10 Mbps | 16 MHz | 10BASE-T Ethernet (old) |
| Cat 4 | 16 Mbps | 20 MHz | Token Ring (obsolete) |
| Cat 5 | 100 Mbps | 100 MHz | Fast Ethernet (100BASE-T) |
| Cat 5e | 1 Gbps | 100 MHz | Gigabit Ethernet (common LAN) |
| Cat 6 | 1 Gbps (10 Gbps ≤55 m) | 250 MHz | Modern networks |
| Cat 6a | 10 Gbps | 500 MHz | Enterprise / Data centers |
| Cat 7 | 10 Gbps | 600 MHz | Shielded, high-performance |
| Cat 8 | 25–40 Gbps | 2000 MHz | Data centers (short distance) |



---
### OSI vs TCP/IP – Key Differences

| OSI Model | TCP/IP Model |
|---------|-------------|
| Conceptual / theoretical | Practical / real-world |
| 7 layers | 4 layers |
| ISO standard | DoD standard |
| Used for learning & troubleshooting | Used for implementation |
| Separates presentation & session | Combines them |

📌 **Exam Tip:**  
OSI is used for **troubleshooting**, TCP/IP for **actual networking**

---

### Common Ports (High-Yield)

| Protocol | Port | Secure? |
|--------|------|--------|
| HTTP | 80 | ❌ |
| HTTPS | 443 | ✅ |
| FTP | 21 | ❌ |
| SSH | 22 | ✅ |
| SMTP | 25 | ❌ |
| DNS | 53 | ❌ |
| POP3 | 110 | ❌ |
| IMAP | 143 | ❌ |
| SNMP | 161 | ❌ |
| RDP | 3389 | ❌ |

---

## 6.2 Network Attacks and Countermeasures

### Common Network Attacks

| Attack | Description | Impact |
|------|------------|-------|
| DDoS | Floods target with traffic | Service outage |
| MITM | Attacker intercepts traffic | Data theft |
| DNS Poisoning | Fake DNS records | Redirect users |
| ARP Spoofing | MAC-IP manipulation | MITM |
| Replay Attack | Reuses captured packets | Unauthorized access |
| Packet Sniffing | Captures unencrypted traffic | Credential theft |

---

### Countermeasures

| Attack | Countermeasure |
|------|---------------|
| DDoS | CDN, rate limiting, load balancer |
| MITM | TLS, certificate validation |
| DNS Poisoning | DNSSEC |
| ARP Spoofing | Static ARP, DHCP snooping |
| Sniffing | Encryption (TLS, IPSec) |

📌 **Exam Tip:**  
CDNs absorb DDoS traffic before it reaches the server.

---

## 6.3 Network Access Controls

### IEEE 802.1X (Port-Based Access Control)

- Prevents unauthorized devices from joining a network
- Uses authentication **before** granting access

#### 802.1X Components
- **Supplicant:** Client device
- **Authenticator:** Switch / AP
- **Authentication Server:** RADIUS

---

### RADIUS vs TACACS+

| Feature | RADIUS | TACACS+ |
|------|--------|---------|
| Encryption | Password only | Entire payload |
| Transport | UDP | TCP |
| Authentication | Centralized | Centralized |
| Authorization | Limited | Granular |
| Accounting | Yes | Yes |
| Vendor | Open standard | Cisco |

📌 **Exam Rule:**  
- **RADIUS** → network access  
- **TACACS+** → device administration

---

### Remote Access Technologies

| Technology | Description |
|-----------|------------|
| VPN | Encrypted tunnel over public network |
| Thin Client | Centralized processing |
| Remote Desktop | Full GUI remote access |

---

## 6.4 Network Security Management

### Placement of Security Devices

| Placement | Description |
|--------|------------|
| Inline | Actively inspects & blocks traffic |
| Passive | Monitors only |
| Virtual | Cloud-based security controls |

---

### Network Segmentation

| Method | Purpose |
|------|--------|
| VLAN | Logical separation |
| Firewall Zones | Trust boundaries |
| ACL | Traffic filtering |
| Micro-segmentation | Zero Trust enforcement |
| Data/Control Plane | Network function separation |

📌 **Exam Tip:**  
Segmentation limits **blast radius** of attacks.

---

### Secure Device Management

- Change default credentials
- Disable unused services
- Patch firmware
- Secure management interfaces
- Use SSH instead of Telnet

---

## 6.5 Network Security Devices

### Firewalls

| Type | Function |
|----|---------|
| Packet Filtering | Layer 3/4 filtering |
| Stateful | Tracks sessions |
| Application Firewall | Layer 7 inspection |
| WAF | Protects web applications |

---

### Proxy Servers

| Type | Purpose |
|----|--------|
| Forward Proxy | Hides internal clients |
| Reverse Proxy | Protects servers |

---

### IDS vs IPS

| IDS | IPS |
|----|----|
| Detect only | Detect + block |
| Passive | Inline |
| Alerts SOC | Stops attack |

---

### Traffic Shaping

| Device | Purpose |
|------|--------|
| Load Balancer | Distributes traffic |
| WAN Optimizer | Improves WAN performance |

---

## 6.6 Wireless Security

### Wireless Technologies

| Technology | Use Case |
|-----------|---------|
| Cellular (4G/5G) | Mobile data |
| Wi-Fi | Local connectivity |
| Bluetooth | Short-range devices |
| NFC | Payments |
| IoT | Sensors & automation |

---

### Wireless Security Protocols

| Protocol | Security Level |
|--------|---------------|
| WEP | ❌ Broken |
| WPA | Weak |
| WPA2 | Secure |
| WPA3 | Strongest |

---

### EAP Methods

| EAP Type | Description |
|--------|------------|
| EAP-TLS | Certificate-based |
| PEAP | Encrypted tunnel |
| EAP-TTLS | Secure authentication |

---

### IoT Security Risks

- Weak authentication
- Default passwords
- Poor patching
- Insecure communication

---

## Domain 6 Exam Focus Summary

| Topic | Must Remember |
|-----|--------------|
| OSI Model | Layers + protocols |
| TCP/IP | Practical model |
| DDoS | CDN mitigation |
| 802.1X | Port-based NAC |
| RADIUS vs TACACS+ | UDP vs TCP |
| IDS vs IPS | Detect vs block |
| WPA3 | Best wireless security |
| Segmentation | Limits attack spread |

---

## One-Line Exam Memory Hooks

- **OSI = Troubleshooting**
- **TCP/IP = Real networking**
- **IPS blocks, IDS alerts**
- **WAF protects web apps**
- **RADIUS for users, TACACS+ for admins**
- **WEP is dead** Sure?
- **Segmentation reduces damage**

