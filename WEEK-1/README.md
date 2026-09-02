# 🌐 Week 01: Networking Fundamentals & Core Protocols

> **Track:** CCNA 200-301 & CompTIA Security+ Foundations  
> **Focus:** OSI & TCP/IP Models, IPv4 Subnetting, Protocol Mechanics & Threat Surfaces  
> **Challenge Days Completed:** Days 01 – 03 of 100  
> **Status:** `In Progress` 🚀

---

## 🎯 Weekly Objective

The primary objective of Week 1 is to build an unshakable technical understanding of how computer networks operate from the physical layer up to the application layer. In cybersecurity, you cannot defend or audit what you do not fundamentally understand. 

This week focuses on dissecting the network stack, mastering binary-to-decimal calculations for IPv4 subnetting, and analyzing core protocols (HTTP, HTTPS, DNS, DHCP) both theoretically and at the packet level.

---

## 📚 Core Resources & Tools Used

| Category | Resource / Tool | Purpose & Application |
| :--- | :--- | :--- |
| **Video Course** | [Jeremy's IT Lab CCNA 200-301](https://www.youtube.com/playlist?list=PLxbwE86Cz83-or_yy9xlPXyCRwL_35_xL) | Deep networking fundamentals, Cisco architecture, packet encapsulation |
| **Video Course** | [Professor Messer CompTIA Network+ & Security+](https://www.professormesser.com/) | Standardized security baselines, protocol analysis, OSI layers |
| **Video Series** | [Practical Networking - Subnetting Mastery](https://www.youtube.com/playlist?list=PLIFyRwBY_4bQUE4IB5c4VPRyDoLgOdExE) | Fast binary math, CIDR notation, subnet calculations & magic numbers |
| **Interactive Labs** | [TryHackMe (Pre-Security / Intro to Networking)](https://tryhackme.com/) | Hands-on packet flow tracing, protocol inspection, interactive browser labs |
| **Simulation / Capture** | Cisco Packet Tracer & Wireshark | Building virtual topologies, inspecting frame headers and protocol exchanges |
| **Spaced Repetition** | Anki Flashcards (Jeremy's IT Lab & Security+ Decks) | Active recall for port numbers, protocol acronyms, header fields |

---

## 📅 Daily Breakdown: Days 01 – 03

```
  ┌─────────────────────────┐     ┌─────────────────────────┐     ┌─────────────────────────┐
  │         DAY 01          │     │         DAY 02          │     │         DAY 03          │
  │   OSI & TCP/IP Models   │ ──► │     IPv4 Subnetting     │ ──► │      Core Protocols     │
  │    & Encapsulation      │     │    & CIDR Mechanics     │     │ HTTP, HTTPS, DNS, DHCP  │
  └─────────────────────────┘     └─────────────────────────┘     └─────────────────────────┘
```

---

### 🔹 Day 01: OSI 7-Layer Model vs. TCP/IP Stack & Packet Encapsulation

#### 🎯 Goal
Understand the architectural layers governing data transmission across networks, the protocol data units (PDUs) at each stage, and the encapsulation/decapsulation lifecycle.

#### 🛠️ What Was Done
1. **OSI 7-Layer Decomposition**: Analyzed each layer's role, associated hardware, and addressing schemes:
   - **Layer 7 (Application):** User-facing protocols (HTTP, SSH, DNS, FTP, SMTP).
   - **Layer 6 (Presentation):** Data formatting, encryption/decryption (TLS/SSL), compression.
   - **Layer 5 (Session):** Session establishment, maintenance, and teardown (RPC, NetBIOS, Sockets).
   - **Layer 4 (Transport):** End-to-end communication, segmentation, port addressing, flow control, error checking (TCP vs UDP).
   - **Layer 3 (Network):** Logical addressing (IPv4/IPv6), routing between networks (Routers, L3 Switches).
   - **Layer 2 (Data Link):** Physical addressing (MAC addresses), framing, error detection via Frame Check Sequence (FCS/CRC) (Switches, NICs).
   - **Layer 1 (Physical):** Raw bitstream transmission over physical media (Copper RJ-45, Fiber optic, Radio frequencies).
2. **TCP/IP Model Mapping**: Compared the OSI model against the 4-layer TCP/IP DOD model (*Application, Transport, Internet, Network Access*).
3. **Encapsulation & Decapsulation Mechanics**:
   - Tracked how application payload data is encapsulated step-by-step:
     $$\text{Data} \xrightarrow{\text{L4 Header}} \text{Segment (TCP/UDP)} \xrightarrow{\text{L3 Header}} \text{Packet (IP)} \xrightarrow{\text{L2 Header + Trailer}} \text{Frame (Ethernet)} \xrightarrow{\text{L1}} \text{Bits}$$
   - Decapsulation occurs in reverse order as the receiving host strips off headers layer by layer.
4. **Transport Layer Comparison (TCP vs. UDP)**:
   - **TCP (Transmission Control Protocol):** Connection-oriented, establishes state via the **3-Way Handshake** (`SYN` $\rightarrow$ `SYN-ACK` $\rightarrow$ `ACK`), guaranteed delivery, ordered sequencing, flow control (windowing).
   - **UDP (User Datagram Protocol):** Connectionless, lightweight, no handshake, best-effort delivery, no retransmissions (ideal for real-time traffic like DNS, VoIP, video streaming).

#### 📊 OSI vs. TCP/IP Reference Matrix

| OSI Layer | Layer Name | TCP/IP Layer | PDU Name | Addressing / ID | Typical Protocols / Devices |
| :---: | :--- | :--- | :--- | :--- | :--- |
| **7** | Application | Application | Data | Service Name | HTTP, HTTPS, DNS, DHCP, SSH, FTP |
| **6** | Presentation | Application | Data | Encoding / Syntax | TLS, SSL, JPEG, ASCII |
| **5** | Session | Application | Data | Session ID / Sockets | RPC, NetBIOS, PPTP |
| **4** | Transport | Transport | Segment (TCP) / Datagram (UDP) | Port Numbers (0–65535) | TCP, UDP |
| **3** | Network | Internet | Packet | Logical IP (IPv4 / IPv6) | IPv4, IPv6, ICMP, IPsec, Routers |
| **2** | Data Link | Network Access | Frame | Physical MAC Address | Ethernet (802.3), Wi-Fi (802.11), Switches |
| **1** | Physical | Network Access | Bits | Electrical / Optical signals | Cables (Cat6, Fiber), Hubs, Repeaters |

#### 🔑 Key Takeaways
- **Encapsulation is modular:** Each layer is agnostic to the internal contents of the layer above it, only appending its own headers.
- **Port numbers identify processes**, IP addresses identify hosts across internetworks, and MAC addresses identify physical nodes on the local broadcast domain.

---

### 🔹 Day 02: IPv4 Addressing, Binary Arithmetic & Subnetting Mastery

#### 🎯 Goal
Master 32-bit IPv4 addressing structure, binary conversions, classful ranges, RFC 1918 private scopes, and classless inter-domain routing (CIDR) subnetting calculations.

#### 🛠️ What Was Done
1. **Binary & Decimal Conversion Foundations**:
   - Broke down the 32-bit IPv4 address into 4 octets (8 bits each): `X.X.X.X`
   - Mastered positional binary weights for 8-bit octets:
     $$\mathbf{128} \quad \mathbf{64} \quad \mathbf{32} \quad \mathbf{16} \quad \mathbf{8} \quad \mathbf{4} \quad \mathbf{2} \quad \mathbf{1}$$
   - Practiced rapid conversion between decimal octets and binary bytes (e.g., $192 = 128 + 64 = 11000000_2$, $255 = 11111111_2$).
2. **Classful Addressing & Reserved Spaces**:
   - **Class A:** `1.0.0.0 – 126.255.255.255` (Default `/8` - `255.0.0.0`)
   - **Class B:** `128.0.0.0 – 191.255.255.255` (Default `/16` - `255.255.0.0`)
   - **Class C:** `192.0.0.0 – 223.255.255.255` (Default `/24` - `255.255.255.0`)
   - **Class D:** `224.0.0.0 – 239.255.255.255` (Multicast traffic)
   - **Class E:** `240.0.0.0 – 255.255.255.255` (Experimental / Research)
3. **RFC 1918 Private IP Ranges & Special Purpose Addresses**:
   - `10.0.0.0/8` (`10.0.0.0 – 10.255.255.255`) $\rightarrow$ Large enterprise networks
   - `172.16.0.0/12` (`172.16.0.0 – 172.31.255.255`) $\rightarrow$ Medium business networks
   - `192.168.0.0/16` (`192.168.0.0 – 192.168.255.255`) $\rightarrow$ Small office / Home networks (SOHO)
   - **Loopback:** `127.0.0.0/8` (Localhost diagnostics, e.g., `127.0.0.1`)
   - **APIPA (Automatic Private IP Addressing):** `169.254.0.0/16` (Assigned when DHCP fails)
4. **CIDR & Subnet Calculation Methodology**:
   - Practiced calculating subnets using the **Magic Number** (Block Size) formula:
     $$\text{Magic Number} = 256 - \text{Interesting Octet Subnet Mask Value}$$
   - Calculated total IP addresses ($2^h$) and usable host addresses ($2^h - 2$, subtracting Network ID and Broadcast ID).
   - Applied subnetting across various prefix lengths (`/24`, `/26`, `/27`, `/28`, `/30` for point-to-point links).

#### 🧮 Subnetting Quick-Reference Matrix (Octet 4)

| CIDR Prefix | Subnet Mask | Borrowed Bits | Total IPs ($2^h$) | Usable Hosts ($2^h - 2$) | Magic Number (Block Size) |
| :---: | :--- | :---: | :---: | :---: | :---: |
| `/24` | `255.255.255.0` | 0 | 256 | 254 | 256 |
| `/25` | `255.255.255.128` | 1 | 128 | 126 | 128 |
| `/26` | `255.255.255.192` | 2 | 64 | 62 | 64 |
| `/27` | `255.255.255.224` | 3 | 32 | 30 | 32 |
| `/28` | `255.255.255.240` | 4 | 16 | 14 | 16 |
| `/29` | `255.255.255.248` | 5 | 8 | 6 | 8 |
| `/30` | `255.255.255.252` | 6 | 4 | 2 (Point-to-Point) | 4 |
| `/31` | `255.255.255.254` | 7 | 2 | RFC 3021 Router links | 2 |
| `/32` | `255.255.255.255` | 8 | 1 | Single Host Route | 1 |

#### 🔑 Key Takeaways
- Subnetting isolates broadcast domains, conserves IPv4 address space, and provides the architectural boundary necessary for applying Access Control Lists (ACLs) and network firewalls.
- Always reserve the **First Address** (Network ID) and **Last Address** (Directed Broadcast) in standard subnets.

---

### 🔹 Day 03: Core Network Protocols Analysis (HTTP, HTTPS/TLS, DNS & DHCP)

#### 🎯 Goal
Analyze the packet mechanics, handshake routines, and security architectures of essential application and network management protocols.

#### 🛠️ What Was Done

```
       DNS Resolution                     TLS 1.3 Handshake                     DHCP DORA Flow
  ┌─────────────────────────┐        ┌─────────────────────────┐        ┌─────────────────────────┐
  │ Client ──► Resolver     │        │ Client ──► Client Hello │        │ Client ──► Discover     │
  │ Resolver ──► Root (.)   │        │ Server ──► Server Hello │        │ Server ──► Offer        │
  │ Resolver ──► TLD (.com) │        │ (Keys Exchanged / Auth) │        │ Client ──► Request      │
  │ Resolver ──► Auth NS    │        │ ◄───── Encrypted ─────► │        │ Server ──► ACK          │
  └─────────────────────────┘        └─────────────────────────┘        └─────────────────────────┘
```

#### 1. HTTP (Hypertext Transfer Protocol - TCP Port 80) vs. HTTPS (TCP Port 443)
- **HTTP/1.1 & HTTP/2:** Text-based request-response protocol over cleartext TCP. Examined HTTP verbs (`GET`, `POST`, `PUT`, `DELETE`, `HEAD`) and response status codes (`200 OK`, `301/302 Redirect`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found`, `500 Server Error`).
- **Security Vulnerability:** Data is transmitted in plaintext. An attacker on the local network performing ARP Spoofing can capture session cookies, credentials, and sensitive payloads using packet sniffers.
- **HTTPS & TLS (Transport Layer Security):** Encapsulates HTTP inside an encrypted TLS session.
- **TLS Handshake Process:**
  1. `ClientHello`: Supported cipher suites, TLS version, random client nonce.
  2. `ServerHello`: Selected cipher suite, server digital certificate (X.509 containing public key), server random nonce.
  3. `Authentication & Key Exchange`: Client verifies certificate chain against trusted Certificate Authorities (CAs); uses Diffie-Hellman (ECDHE) for perfect forward secrecy.
  4. `Session Key Derivation`: Both parties compute symmetric encryption keys to protect all subsequent traffic (AES-GCM / ChaCha20-Poly1305).

#### 2. DNS (Domain Name System - UDP/TCP Port 53)
- **Function:** Translates human-readable domain names (e.g., `github.com`) into routable IP addresses.
- **Resolution Hierarchy:**
  $$\text{Client} \xrightarrow{\text{Query}} \text{Recursive Resolver} \rightarrow \text{Root Nameserver (.)} \rightarrow \text{TLD Nameserver (.com)} \rightarrow \text{Authoritative Nameserver}$$
- **Core DNS Record Types Analyzed:**
  - `A`: Maps hostname to IPv4 address (`github.com` $\rightarrow$ `140.82.121.4`).
  - `AAAA`: Maps hostname to 128-bit IPv6 address.
  - `CNAME`: Canonical Name (alias to another domain).
  - `MX`: Mail Exchange (specifies mail servers for domain).
  - `TXT`: Text record (used for domain ownership verification, **SPF**, and **DKIM** email security).
  - `PTR`: Pointer record (Reverse DNS lookup: IP $\rightarrow$ Hostname).
  - `NS` & `SOA`: Nameserver delegation and Start of Authority metadata.
- **Cybersecurity Attack Surface:**
  - **DNS Cache Poisoning / Spoofing:** Injecting false records into a recursive resolver cache to redirect victims to malicious phishing sites.
  - **DNS Tunneling:** Encoding covert data/exfiltration channels inside DNS queries (`malicious-data.attacker.com`).

#### 3. DHCP (Dynamic Host Configuration Protocol - UDP Port 67 Server / Port 68 Client)
- **Function:** Automates IP configuration, default gateway assignment, subnet masking, and DNS server distribution to hosts joining a network.
- **The 4-Step D.O.R.A. Transaction:**
  1. **Discover (`DHCPDISCOVER`):** Client broadcasts (`255.255.255.255`, L2 `FF:FF:FF:FF:FF:FF`) seeking an active DHCP server.
  2. **Offer (`DHCPOFFER`):** DHCP server responds with an available IP address, lease duration, subnet mask, gateway, and DNS servers.
  3. **Request (`DHCPREQUEST`):** Client broadcasts confirming acceptance of the offered parameters.
  4. **Acknowledge (`DHCPACK`):** DHCP server sends final confirmation and binds the lease in its database.
- **Cybersecurity Attack Surface:**
  - **DHCP Starvation:** Malicious actors flood `DHCPDISCOVER` frames with randomized MAC addresses to exhaust the entire DHCP address pool, causing a Denial of Service (DoS).
  - **Rogue DHCP Server:** An attacker introduces an unauthorized DHCP server offering the attacker's IP as the default gateway to perform Man-in-the-Middle (MitM) traffic interception.
  - **Mitigation:** DHCP Snooping on managed network switches.

---

## 📈 Days 01 – 03 Summary Matrix

| Day | Topic | Key Skills & Artifacts | Primary Resource | Status |
| :---: | :--- | :--- | :--- | :---: |
| **01** | **OSI & TCP/IP Models** | Layer mapping, PDU encapsulation, TCP 3-way handshake vs UDP | Jeremy's IT Lab / Prof. Messer | ✅ Completed |
| **02** | **IPv4 Subnetting & CIDR** | Binary conversion, RFC 1918 private scopes, Magic number method, /24 to /30 calculations | Practical Networking / CCNA | ✅ Completed |
| **03** | **Core Protocols (HTTP, TLS, DNS, DHCP)** | TLS Handshake, DNS record analysis, DHCP DORA flow, security vulnerability vectors | TryHackMe / Network+ | ✅ Completed |

---

## 🔮 Upcoming in Week 01 (Days 04 – 07)

- **Day 04:** Common Ports & Network Protocol Security Mapping (SSH, FTP, RDP, Telnet, SNMP, NTP).
- **Day 05:** VPN Architectures & Cryptographic Encapsulation (IPsec, IKEv1/v2, AH vs. ESP tunnel modes).
- **Day 06:** Wireshark Installation, Filter Syntax & Packet Sniffing Fundamentals.
- **Day 07:** PCAP Traffic Forensics & Analyzing Live Network Captures for Anomalies.

---

*Repository part of the **100 Days of Cybersecurity Challenge** by [@ani18cs](https://github.com/ani18cs).*
