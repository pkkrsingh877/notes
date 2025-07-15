# Unit I: Foundations, Architecture & Media

---

## 1. What Is a Computer Network?  
- Enables devices to share resources (files, printers, internet) across distances.  
- Cuts costs by centralizing services—one powerful server vs. many underpowered PCs.  
- Supports distributed computing (e.g., Google’s data centers working in concert).  
- Analogy: a railway network where trains (data) carry cargo (information) between stations (devices).

## 2. Layered Network Architecture: ISO-OSI Model  
1. **Physical Layer (L1)**  
   - Transmits raw bits over a medium (copper voltages, light pulses).  
   - Device examples: cables, repeaters.  
   - Analogy: the pavement on a highway—foundation for everything above.  
2. **Data Link Layer (L2)**  
   - Frames bits into error-checked packets; manages MAC addresses.  
   - Devices: switches, bridges.  
   - Analogy: lane markings that keep cars (frames) in order.  
3. **Network Layer (L3)**  
   - Routes packets using logical addresses (IP); ICMP for diagnostics.  
   - Devices: routers.  
   - Analogy: highway interchange signs directing traffic.  
4. **Transport Layer (L4)**  
   - Ensures end-to-end delivery: reliable (TCP) or fast (UDP).  
   - Flow control, congestion control.  
   - Analogy: seatbelts vs. sports cars—safety vs. speed.  
5. **Session Layer (L5)**  
   - Manages dialogues, check-pointing, recovery (e.g., RPC, NetBIOS).  
6. **Presentation Layer (L6)**  
   - Translates data formats, handles encryption/decryption, compression.  
   - Examples: SSL/TLS, JPEG.  
7. **Application Layer (L7)**  
   - Interfaces for user-facing software: HTTP, SMTP, DNS, FTP.

## 3. Transmission Fundamentals  
- **Bandwidth vs. Bitrate:**  
  - Bandwidth = range of frequencies (Hz), Bitrate = data speed (bps).  
  - Analogy: bandwidth = number of lanes, bitrate = vehicles per second.  
- **Signal Types:** analog (continuous waves) vs. digital (discrete pulses).  
- **Noise & Attenuation:** thermal noise, crosstalk, signal weakening over distance.  
- **Shannon’s Capacity Formula:**  
  \[ C = B \log_2(1 + \tfrac{S}{N}) \]  
  where C = max data rate, B = bandwidth, S/N = signal-to-noise ratio.  
  Analogy: water flow in pipes slowing when pipes get noisy or leaky.

## 4. Communication Media  

### 4.1 Conductive Metal (Wired Cable)  
- **Unshielded Twisted Pair (UTP):**  
  - Cat 5e up to 1 Gbps; Cat 6 up to 10 Gbps (limited to ~55 m).  
  - Cost-effective, easy to install.  
- **Shielded Twisted Pair (STP):**  
  - Foil or braid reduces EMI; used near heavy machinery.  
- **Coaxial Cable:**  
  - Single conductor + shield; used for cable TV, broadband.  
- Analogy: UTP = cheap garden hose; STP = hose with metal braid.

### 4.2 Optical Fiber Links  
- **Single-Mode Fiber:**  
  - Long-distance (kilometers), 10 Gbps+.  
- **Multi-Mode Fiber:**  
  - Shorter runs (100 m), 10 Gbps.  
- **Principle:** total internal reflection keeps light inside.  
- Analogy: laser beam guiding light through a glass straw.

### 4.3 Wireless Communication  
- **Radio Links:** Wi-Fi (2.4/5 GHz), Bluetooth (2.4 GHz); multipath fading.  
- **Microwave:** point-to-point, line-of-sight (backhaul).  
- **Satellite:**  
  - GEO (~36,000 km, ~250 ms latency), LEO (1,200 km, ~40 ms latency).  
- Pros: mobility, rapid deployment. Cons: interference, security challenges.  
- Analogy: walkie-talkies vs. fiber optic highways.

## 5. Communication Services & Devices  
- **Telephone System:** circuit switching—dedicated channel for the call.  
- **ISDN:** digitized voice/data; B-channels (64 kbps), D-channel for signaling.  
- **Cellular Phones:**  
  - Cells with frequency reuse; handover between towers.  
  - 2G (GSM, CDMA), 3G (WCDMA), 4G (LTE).  
- **ATM (Asynchronous Transfer Mode):** fixed 53-byte cells, QoS support.  
- **Network Security Goals:** confidentiality (encryption), integrity (hash/MAC), availability (redundancy).  
- **Virtual Terminal Protocol:** remote mainframe access (3270/5250 emulation).  
- **DNS:** hierarchical name resolution with caching.  
- **SNMP:** MIB database; agents report metrics to managers.  
- **Email Services:** SMTP (sending), POP3/IMAP (retrieval).  
- **WWW:** HTTP methods (GET, POST), status codes (200 OK, 404 Not Found).

---

*End of Unit I*

---

# Unit II: Data Security & Integrity

---

## 1. Error Detection & Correction Codes  

### 1.1 Parity Checking  
- Adds one bit per byte: even or odd parity.  
- Detects single-bit errors; fails on two-bit flips.  
- Analogy: a guest list where you know one seat oddness ruined the count.

### 1.2 Cyclic Redundancy Check (CRC)  
- Treats data as a polynomial, divides by a generator polynomial.  
- Remainder bits appended to frame; widely used (Ethernet CRC-32).  
- Example: generator polynomial 0x1021 for CRC-CCITT.  
- Analogy: skilled proofreader running a formula-based check.

### 1.3 Hamming Code  
- Positions of parity bits at powers of 2 (1, 2, 4, 8…).  
- Corrects single-bit errors, detects two-bit errors.  
- Example: 7-bit message + 4 parity bits → 11-bit codeword.  
- Analogy: safety net with multiple checkpoints.

## 2. Protocol Concepts  

### 2.1 Basic Flow Control  
- **Stop-and-Wait:** sender waits for ACK before next frame; simple but low utilization.  
- Analogy: taking one order at a time before billing.

### 2.2 Sliding Window Protocol  
- Sender can transmit up to N unacknowledged frames.  
- Improves throughput over high-latency links.  
- **Go-Back-N:** on error, resend from erroneous frame onward.  
- **Selective Repeat:** only resend the specific erroneous frames.  
- Analogy: waiter taking multiple orders before serving; if one dish burns, you remake just that dish (Selective Repeat) or all dishes since then (Go-Back-N).

## 3. Protocol Correctness & FSM  
- Model sender/receiver as finite state machines (states + transitions).  
- States: WAIT_FOR_CALL, SENDING, WAIT_FOR_ACK, etc.  
- Transitions triggered by events: frame arrival, timeout, ACK receipt.  
- Example: simplified TCP state machine (LISTEN → SYN_SENT → ESTABLISHED).

---

*End of Unit II*

---

# Unit III: Local Area Network Architectures

---

## 1. IEEE 802.x LAN Standards  

### 1.1 Ethernet (802.3)  
- CSMA/CD access; preamble (7 bytes), SFD (1 byte), 1500-byte payload.  
- Speeds: 10 Mbps, 100 Mbps (Fast Ethernet), 1 Gbps, 10 Gbps.  
- Analogy: polite drivers waiting for green light before entering intersection.

### 1.2 Token Ring (802.5)  
- Token-passing on a ring; 4 Mbps or 16 Mbps.  
- IBM’s traditional corporate LAN.  
- Analogy: a single “talking stick” passed around so only one speaker at a time.

### 1.3 Token Bus (802.4)  
- Logical ring over a physical bus; token moves electronically.  
- Used in industrial settings.  

### 1.4 FDDI (Fiber Distributed Data Interface)  
- Dual counter-rotating fiber rings at 100 Mbps.  
- Self-healing: one ring takes over if the other breaks.  

### 1.5 DQDB (Distributed Queue Dual Bus, 802.6)  
- Two unidirectional buses, each node competes for access.  
- Speeds up to 150 Mbps for metropolitan area networks.

## 2. Inter-Networking Devices  

### 2.1 Layer 1 Devices  
- **Repeater:** regenerates and retimes signals.  
- **Hub:** multiport repeater; broadcasts every frame to all ports.

### 2.2 Layer 2 Devices  
- **Bridge:** filters frames by MAC, builds forwarding table.  
- **Switch:** microsegmentation reduces collisions; supports VLANs.

### 2.3 Layer 3+ Devices  
- **Router:** routes IP packets based on routing tables.  
- **Gateway:** translates protocols (e.g., X.25 ↔ TCP/IP).

---

*End of Unit III*

---

# Unit IV: Wide Area Networks & Routing

---

## 1. Routing Essentials  

### 1.1 Static vs. Dynamic Routing  
- **Static:** manually configured paths; simple, low overhead, no adaptation.  
- **Dynamic:** routers share updates to adapt to topology changes.

### 1.2 Distance Vector (Bellman-Ford)  
- Each router shares full routing table with neighbors.  
- Converges slowly; prone to routing loops.  
- Analogy: friends sharing travel times to every city they know.

### 1.3 Link State (Dijkstra)  
- Routers flood link-state advertisements, build full network map.  
- Compute shortest paths with Dijkstra’s algorithm.  
- Analogy: everyone broadcasting their road conditions to build a full map.

### 1.4 OSPF (Open Shortest Path First)  
- Areas, backbone design, DR/BDR election.  
- Fast convergence, hierarchical scaling.

## 2. Flooding, Broadcasting & Multicasting  
- **Flooding:** send packet on all links except source; safe but wasteful.  
- **Broadcasting:** one-to-all within network segment (ARP requests).  
- **Multicasting:** one-to-many with group management (IGMP).

## 3. Congestion & Deadlock  
- **Congestion Causes:** queue overload, high arrival rates.  
- **Controls:** window adjustment (TCP), random early detection.  
- **Deadlock Avoidance:** ensure resource ordering, release on timeout.

## 4. Internet & Transport Protocols  

### 4.1 IP Protocol  
- IPv4 header: version, IHL, TTL, checksum, fragmentation fields.  
- IPv6: simplified header, built-in extension headers.

### 4.2 TCP (Transmission Control Protocol)  
- Three-way handshake (SYN, SYN-ACK, ACK).  
- Sliding window, flow control (advertised window), congestion control (slow start, AIMD).  
- Connection teardown: FIN, ACK sequence.

### 4.3 UDP (User Datagram Protocol)  
- Connectionless datagrams, no flow or error control.  
- Lightweight: used for DNS queries, VoIP, streaming.

---

*End of Unit IV*

---

# Unit V: Wireless Broadband Networks & Standards

---

## 1. Wireless Broadband Fundamentals  
- **Fixed Wireless:** last-mile links via microwave, MMDS.  
- **Key Metrics:** throughput, latency, reliability in non-line-of-sight environments.  
- Analogy: wireless broadband = invisible pipes carrying water to your home.

## 2. Platforms & Access Technologies  
- **Enhanced Copper:**  
  - ADSL (up to 8 Mbps down, 1 Mbps up), VDSL (up to 100 Mbps).  
- **Fibre Optic & HFC (Hybrid Fiber-Coax):**  
  - FTTH (GPON, EPON), DOCSIS over cable TV lines.  
- **3G Cellular:** CDMA2000, WCDMA; soft handoff improves reliability.  
- **Satellite:** VSAT terminals; GEO vs. LEO trade-offs.

## 3. Emerging Broadband Standards  
- **ATM over Wireless:** QoS for voice/data with 53-byte cells.  
- **HiperLAN2 (ETSI):**  
  - Operates at 5 GHz, supports real-time multimedia, dynamic frequency selection.  
- **Global 3G CDMA Harmonization:**  
  - Bridging CDMA2000 with UMTS/WCDMA for global roaming.  
  - Proposed unified protocol layers for compatibility.

---

*End of Unit V*