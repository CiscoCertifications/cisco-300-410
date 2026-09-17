# Cisco 300-410 ENARSI Exam: Implementing Cisco Enterprise Advanced Routing and Services

[![Cisco Certified](https://img.shields.io/badge/Cisco_Certified-CCNP_Enterprise-049fd9?style=for-the-badge&logo=cisco&logoColor=white)](https://www.cisco.com/)
[![Specialist](https://img.shields.io/badge/Cisco_Specialist-Enterprise_Advanced_Infrastructure-1BA0D7?style=for-the-badge)](https://www.cisco.com/)
[![Track](https://img.shields.io/badge/Track-Enterprise_Networking-049fd9?style=for-the-badge&logo=cisco)](https://www.cisco.com/)
[![Level](https://img.shields.io/badge/Level-Professional-darkblue?style=for-the-badge)](https://www.cisco.com/)
[![Duration](https://img.shields.io/badge/Duration-90_Minutes-orange?style=for-the-badge)](https://www.cisco.com/)
[![Score](https://img.shields.io/badge/Passing_Score-~825%20%2F%201000-blue?style=for-the-badge)](https://www.cisco.com/)
[![Practice Partner](https://img.shields.io/badge/Practice_Partner-CertsClub_(20%25_Off_Code:_club20)-28a745?style=for-the-badge&logo=shield)](https://www.certsclub.com/cisco/)

---

## 1. Exam Overview & Candidate Profile

The **Cisco 300-410 ENARSI (Implementing Cisco Enterprise Advanced Routing and Services)** examination is a premier concentration exam for the **CCNP Enterprise** certification and qualifies candidates for the **Cisco Certified Specialist - Enterprise Advanced Infrastructure Implementation** certification. The exam tests a network engineer's mastery of advanced routing technologies, Layer 3 VPN services, complex infrastructure security controls, and infrastructure troubleshooting methodologies in large-scale enterprise environments.

### Target Candidate Profile & Roles
* **Senior Network Engineer**
* **Enterprise Infrastructure Implementation Specialist**
* **NOC Tier-3 Escalation / Network Operations Lead**
* **Solutions Architect (Enterprise Routing & Services)**
* **Prerequisites:** While there are no formal prerequisites, candidates are strongly advised to hold CCNA or 350-401 ENCOR foundational knowledge, alongside 3 to 5 years of hands-on experience implementing enterprise routing protocols, VPNs, and Layer 3 security.

---

## 2. Key Exam Specifications

| Parameter | Official Specification |
| :--- | :--- |
| **Exam Code** | 300-410 |
| **Exam Name** | Implementing Cisco Enterprise Advanced Routing and Services (ENARSI) |
| **Associated Certifications** | CCNP Enterprise (Concentration) & Cisco Certified Specialist |
| **Duration** | 90 Minutes |
| **Passing Score** | ~825 / 1000 (Scaled dynamic calibration) |
| **Question Count** | 55–65 questions |
| **Question Formats** | Multiple Choice (single/multiple select), Drag-and-Drop, Simlets, CLI Troubleshooting Labs |
| **Delivery Vendor** | Pearson VUE Authorized Test Centers & OnVUE Online Remote Proctored |
| **Practice Test Partner** | **[300-410 Practice Test](https://www.certsclub.com/cisco/)** (Coupon: `club20` for 20% off) |

---

## 3. Skills Measured & Blueprint Domain Weighting

| Domain Code | Domain Title | Exam Weight | Key Technical Objectives Covered |
| :--- | :--- | :---: | :--- |
| **1.0** | **Layer 3 Technologies** | **35%** | Administrative distance troubleshooting; complex route redistribution, route filtering (distribute-lists, prefix-lists, route-maps), and route tagging loop prevention; Policy-Based Routing (PBR) and VRF-lite; EIGRP (classic & named mode, metrics, stub, variance unequal-cost load balancing); OSPFv2/v3 (LSAs 1–7, area types: Stub, Totally Stubby, NSSA, Totally NSSA, virtual links, summarization); BGP (eBGP/iBGP, 13-step path selection, communities, route reflectors). |
| **2.0** | **VPN Technologies** | **20%** | MPLS operations: Label Distribution Protocol (LDP), Label Information Base (LIB), Label Forwarding Information Base (LFIB); MPLS Layer 3 VPNs: VRFs, Route Distinguishers (RD), Route Targets (RT import/export), MP-BGP VPNv4 address family; DMVPN: Phase 1, Phase 2, and Phase 3 (NHRP redirect and shortcut), mGRE, IPsec profiles. |
| **3.0** | **Infrastructure Security** | **20%** | Cisco IOS AAA device access (TACACS+, RADIUS); Control Plane Policing (CoPP) to protect the Route Processor; Unicast Reverse Path Forwarding (uRPF strict vs. loose mode); IPv6 First-Hop Security (RA Guard, DHCPv6 Guard, ND Inspection, Source Guard); Time-based and infrastructure ACLs. |
| **4.0** | **Infrastructure Services** | **25%** | SNMPv2c / SNMPv3 (authPriv views); IP SLA (ICMP, HTTP, jitter) and object tracking (`track`); Cisco IOS Embedded Event Manager (EEM) applets, event detectors, and CLI/syslog action triggers; NetFlow and Flexible NetFlow (v5, v9, IPFIX, flow records, monitors, exporters); DNA Center Assurance telemetry. |

---

## 4. Scenario-Based Technical Practice Questions

### Scenario 1: BGP Best Path Selection - Attribute Evaluation Hierarchy
**Topology Background:**  
A border router, AS 65001, receives two BGP update routes for prefix `198.51.100.0/24` from two different external upstream Internet Service Providers:
* **Path 1 (via ISP-A):** Weight `0`, Local Preference `100`, AS-Path `64512 64520` (length 2), Origin IGP (`i`), MED `50`, received via eBGP.
* **Path 2 (via ISP-B):** Weight `0`, Local Preference `100`, AS-Path `64515 64516 64517` (length 3), Origin IGP (`i`), MED `10`, received via eBGP.
Both next-hops have identical IGP metrics. Which path will the router install into its routing table, and which tie-breaker determines the decision?

* A. Path 2, because MED 10 is lower than MED 50
* B. Path 1, because the AS-Path length of 2 is shorter than the AS-Path length of 3
* C. Path 2, because ISP-B advertised the route first
* D. Both paths will be installed to perform BGP multipath equal-cost load sharing

**Correct Answer:** **B**

**Detailed Technical Explanation:**  
The Cisco BGP Best Path Selection algorithm follows an exact, deterministic sequence:
1. Highest **Weight** (default 0 for learned routes; tie at 0).
2. Highest **Local Preference** (tie at 100).
3. Locally originated routes (neither).
4. Shortest **AS-Path** length:
   * Path 1 has an AS-Path length of **2** (`64512 64520`).
   * Path 2 has an AS-Path length of **3** (`64515 64516 64517`).
* Because Path 1 has the shorter AS-Path, **Path 1 is selected immediately**. 
* The **Multi-Exit Discriminator (MED)** is evaluated at Step 6, which is only reached if AS-Path lengths are identical. Therefore, MED 10 is never evaluated.
* Distractor analysis: Option A incorrectly prioritizes MED over AS-Path. Option C is a later tie-breaker (oldest eBGP route). Option D is false because BGP multipath requires identical AS-Path lengths and attributes.

---

### Scenario 2: OSPF Area Types - NSSA and Totally NSSA LSA Filtering
**Topology Background:**  
An enterprise connects a subsidiary router running RIPv2 into OSPF Area 10. The network design requires Area 10 to:
1. Support an ASBR redistributing external RIPv2 routes into OSPF.
2. Block Type 4 and Type 5 LSAs injected by external ASBRs in other areas.
3. Block Type 3 summary LSAs injected by the Area Border Router (ABR).
4. Have the ABR automatically inject a single Type 3 default route into Area 10.
Which command must be configured under `router ospf 1` on the ABR for Area 10?

* A. `area 10 stub`
* B. `area 10 stub no-summary`
* C. `area 10 nssa`
* D. `area 10 nssa no-summary`

**Correct Answer:** **D**

**Detailed Technical Explanation:**  
* An **NSSA (Not-So-Stubby Area)** permits an internal ASBR to inject external routes into the area as **Type 7 LSAs**, which the ABR translates into standard Type 5 LSAs before flooding into Area 0.
* Standard NSSA (`area 10 nssa`) blocks Type 4 and 5 LSAs, but still permits Type 3 summary LSAs from other OSPF areas.
* Adding the **`no-summary`** keyword configures Area 10 as a **Totally NSSA**. The ABR blocks Type 3, Type 4, and Type 5 LSAs, and automatically originates a single **Type 3 LSA default route (`0.0.0.0/0`)** into Area 10.
* Distractor analysis: Options A and B (Stub / Totally Stubby) strictly forbid any ASBR within the area, which prevents RIPv2 redistribution. Option C (standard NSSA) does not block Type 3 LSAs and does not automatically inject a default route without `default-information-originate`.

---

### Scenario 3: EIGRP Named Mode - Feasibility Condition and Variance
**Topology Background:**  
In EIGRP named mode (`router eigrp ENTERPRISE`), router R1 learns three routes to destination prefix `10.50.0.0/16`:
* **Path A (via R2):** Feasible Distance (FD) = `2560000`, Reported Distance (RD) = `1280000`
* **Path B (via R3):** Feasible Distance (FD) = `3840000`, Reported Distance (RD) = `2400000`
* **Path C (via R4):** Feasible Distance (FD) = `5120000`, Reported Distance (RD) = `2800000`
R1 selects Path A as the Successor with an active FD of `2560000`. The engineer configures `variance 2` under the address family. Which paths will be installed into R1's routing table for unequal-cost load balancing?

* A. Path A only
* B. Path A and Path B
* C. Path A, Path B, and Path C
* D. Path B and Path C only

**Correct Answer:** **B**

**Detailed Technical Explanation:**  
For an EIGRP route to participate in unequal-cost load balancing via `variance`:
1. **Feasibility Condition Check:** The candidate path's Reported Distance (RD) must be **strictly less than** the Successor's Feasible Distance (FD):
   * Successor FD = `2560000`.
   * Path B RD = `2400000` ($2400000 < 2560000$ $\rightarrow$ **Feasible Successor verified**).
   * Path C RD = `2800000` ($2800000 > 2560000$ $\rightarrow$ **Fails Feasibility Condition**; discarded to prevent routing loops).
2. **Variance Calculation Check:** The candidate's FD must be less than `Successor FD * Variance`:
   * Metric threshold = $2560000 \times 2 = \mathbf{5120000}$.
   * Path B FD = `3840000` ($3840000 < 5120000$ $\rightarrow$ **Passed**).
* Result: **Path A (Successor) and Path B (Feasible Successor)** are installed into the routing table.
* Distractor analysis: Option C fails because Path C's RD exceeds Path A's FD, violating loop-free guarantees regardless of variance.

---

### Scenario 4: Mutual Redistribution - Route Tagging and Loop Prevention
**Topology Background:**  
Two boundary routers, R1 and R2, perform mutual two-way route redistribution between an OSPF Area 0 domain and an EIGRP domain. Soon after enabling redistribution, both routers experience route flapping, suboptimal routing, and routing loops. Which mechanism provides the standard, robust solution to prevent redistributed routes from looping back into their originating routing domain?

* A. Lowering the Administrative Distance of OSPF to 80
* B. Applying route-maps during redistribution to assign a numeric `tag` to routes leaving EIGRP, and denying routes with that tag when redistributing from OSPF back into EIGRP
* C. Enabling split horizon on the interconnecting OSPF interfaces
* D. Configuring `default-metric` on both routers to 10000

**Correct Answer:** **B**

**Detailed Technical Explanation:**  
* Mutual two-way redistribution across multiple boundary routers creates severe feedback loops because routes redistributed from Domain A into Domain B can be learned by the second boundary router and redistributed back into Domain A with a preferred administrative distance.
* **Standard Remediation via Route Tagging:**
  1. Router R1 attaches a unique administrative tag (e.g., `tag 100`) to all EIGRP routes when redistributing them into OSPF.
  2. Router R2 matches this tag via a route-map (`match tag 100`) and **denies** those routes when redistributing from OSPF back into EIGRP.
  3. The reverse process is applied for OSPF-originated routes (e.g., `tag 200`).
* Distractor analysis: Option A exacerbates loops by causing OSPF to override internal EIGRP routes. Option C is invalid because split horizon is a distance-vector concept that does not apply to OSPF link-state databases. Option D sets seed metrics but does not prevent route re-injection.

---

### Scenario 5: MPLS Layer 3 VPN Architecture - RD vs. RT Mechanics
**Topology Background:**  
A service provider operates an MPLS core network connecting two enterprise customers, Customer-Alpha and Customer-Beta, both using overlapping `10.0.0.0/8` private IPv4 addressing. On the Provider Edge (PE) routers:
1. Parameter 1 ensures that Customer-Alpha's `10.1.1.0/24` route is globally unique within MP-BGP by prepending an 8-byte prefix to create a 12-byte VPNv4 address.
2. Parameter 2 is an extended BGP community attached to the VPNv4 route that controls which customer VRF tables on remote PE routers will import the route.
Which terms correctly identify Parameter 1 and Parameter 2?

* A. Parameter 1: Route Target (RT) | Parameter 2: Route Distinguisher (RD)
* B. Parameter 1: Route Distinguisher (RD) | Parameter 2: Route Target (RT)
* C. Parameter 1: Label Switched Path (LSP) | Parameter 2: VC Label
* D. Parameter 1: VRF Name | Parameter 2: LDP Identifier

**Correct Answer:** **B**

**Detailed Technical Explanation:**  
In MPLS Layer 3 VPNs (RFC 4364):
* **Route Distinguisher (RD):** An 8-byte value added to the customer's 4-byte IPv4 prefix to create a globally unique **12-byte (96-bit) VPNv4 address** (e.g., `65000:100:10.1.1.0/24`). The RD prevents address collision in MP-BGP when multiple customers use overlapping RFC 1918 space.
* **Route Target (RT):** A BGP extended community attribute attached to the VPNv4 route. It defines the VPN membership and export/import policy, instructing remote PE routers whether to import the route into a specific customer VRF routing table.
* Distractor analysis: Option A reverses the definitions. Options C and D confuse data plane forwarding labels and local identifiers with BGP control plane attributes.

---

### Scenario 6: DMVPN Phase 3 - NHRP Redirect and Shortcut Forwarding
**Topology Background:**  
An enterprise deploys a Dual-Hub DMVPN Phase 3 network using mGRE and IPsec. Spoke-1 needs to communicate directly with Spoke-2 without hairpinning user traffic through the Hub router. Which two commands must be configured on the Hub and Spokes respectively to enable dynamic spoke-to-spoke direct tunnel creation?

* A. Hub: `ip nhrp map multicast dynamic` | Spokes: `ip nhrp holdtime 300`
* B. Hub: `ip nhrp redirect` on the mGRE interface | Spokes: `ip nhrp shortcut` on the mGRE interface
* C. Hub: `ip ospf network broadcast` | Spokes: `ip ospf priority 0`
* D. Hub: `tunnel mode ipsec ipv4` | Spokes: `tunnel protection ipsec profile DMVPN_PROF`

**Correct Answer:** **B**

**Detailed Technical Explanation:**  
* In **DMVPN Phase 3**:
  1. When Spoke-1 transmits a packet destined for Spoke-2 to the Hub, the Hub detects that the ingress and egress interface are both the same mGRE interface.
  2. Because **`ip nhrp redirect`** is configured on the Hub's tunnel interface, the Hub forwards the initial packet to Spoke-2 and simultaneously sends an **NHRP Redirect** message back to Spoke-1 saying "there is a more direct path."
  3. Because **`ip nhrp shortcut`** is configured on Spoke-1 and Spoke-2, Spoke-1 sends an NHRP Resolution Request to Spoke-2 to discover its public NBMA IP, establishes a direct dynamic mGRE/IPsec tunnel, and overwrites its CEF routing table to point directly to Spoke-2.
* Distractor analysis: Option A handles multicast registration for routing protocols. Option C configures OSPF area parameters. Option D is standard tunnel protection syntax that does not enable Phase 3 shortcut routing.

---

### Scenario 7: Policy-Based Routing (PBR) - Path Override Mechanics
**Topology Background:**  
A network administrator configures Policy-Based Routing on a core router's ingress interface GigabitEthernet0/0 to route all video traffic (`source port 554 RTSP`) out secondary link `192.168.200.2`, while allowing all other traffic to follow standard routing table lookups:
```ios
route-map PBR_POLICY permit 10
 match ip address 150
 set ip next-hop 192.168.200.2
!
interface GigabitEthernet0/0
 ip policy route-map PBR_POLICY
```
An engineer notices that ICMP `ping` packets generated locally on the router itself targeting remote test destinations do not obey this route-map. What command must be applied globally to apply PBR to locally generated router traffic?

* A. `ip policy route-map PBR_POLICY` in global configuration mode
* B. `ip local policy route-map PBR_POLICY` in global configuration mode
* C. `ip route-cache policy` under interface GigabitEthernet0/0
* D. `set ip default next-hop 192.168.200.2` inside the route-map

**Correct Answer:** **B**

**Detailed Technical Explanation:**  
* Interface PBR (`ip policy route-map <NAME>`) processes only traffic **entering the router from an external source** through that physical or logical interface.
* Packets originated locally by the router's own control plane (e.g., CLI `ping`, `traceroute`, SNMP, BFD) bypass interface-level PBR policies.
* To subject locally generated router traffic to PBR, the administrator must configure the global command: **`ip local policy route-map <NAME>`**.
* Distractor analysis: Option A is invalid global CLI syntax. Option C is a deprecated CEF switching cache command. Option D modifies next-hop priority when routes exist in the RIB, but does not affect local packet interception.

---

### Scenario 8: Control Plane Policing (CoPP) - Protecting the Route Processor
**Topology Background:**  
During a security audit, a network engineer observes high CPU utilization on a Cisco Catalyst 9500 core switch caused by a flood of spoofed ICMP Echo and Telnet connection requests directed at the switch's interface IP addresses. The engineer configures Control Plane Policing (CoPP). Which configuration hierarchy correctly applies a policy to drop unauthorized control plane traffic?

* A. Configure an Extended ACL $\rightarrow$ Match ACL in a `class-map` $\rightarrow$ Define rate-limits/drops in a `policy-map` $\rightarrow$ Apply via `service-policy input` under `control-plane`
* B. Configure an Extended ACL $\rightarrow$ Apply `ip access-group in` directly under `control-plane host`
* C. Configure a `route-map` $\rightarrow$ Apply under `line vty 0 4` with `transport input ssh`
* D. Apply `ip verify unicast source reachable-via rx` under all physical interfaces

**Correct Answer:** **A**

**Detailed Technical Explanation:**  
Control Plane Policing (CoPP) employs the Cisco Modular QoS CLI (MQC) framework applied to the special `control-plane` target:
1. **Classify:** Create ACLs identifying control plane protocols, and match them within class-maps (e.g., `class-map match-all COPP_CLASS; match access-group 120`).
2. **Police/Action:** Define bandwidth limits, burst allowances, or drop actions within a policy-map (e.g., `policy-map COPP_POLICY; class COPP_CLASS; police 8000 conform-action transmit exceed-action drop`).
3. **Enforce:** Apply the policy globally to the control plane using:
   ```ios
   control-plane
    service-policy input COPP_POLICY
   ```
* Distractor analysis: Option B is invalid syntax because standard ACLs cannot be bound directly to `control-plane` without MQC. Option C secures only VTY lines, leaving routing protocols and ICMP exposed. Option D configures uRPF, not CoPP.

---

### Scenario 9: Infrastructure Security - Unicast Reverse Path Forwarding (uRPF)
**Topology Background:**  
An enterprise edge router has two active upstream connections: a high-speed primary connection on interface Gi0/1 and a low-cost backup link on Gi0/2. The network runs asymmetric routing where outbound traffic exits Gi0/1, while return packets from certain external subnets enter via Gi0/2. If the engineer configures **Strict Mode uRPF** on Gi0/2 (`ip verify unicast source reachable-via rx`), what will happen to legitimate return packets arriving on Gi0/2?

* A. Packets will be forwarded normally because the destination IP is in the routing table.
* B. Packets will be dropped if the router's FIB routing table indicates that the best path back to the packet's source IP is out interface Gi0/1.
* C. The router will automatically re-route the return packets across the primary link.
* D. The router will send an ICMP Redirect packet to the upstream ISP.

**Correct Answer:** **B**

**Detailed Technical Explanation:**  
* **uRPF Strict Mode (`reachable-via rx`):** Verifies two conditions for every ingress packet:
  1. The source IP address must exist in the FIB routing table.
  2. The interface through which the packet arrived must **identically match the specific outgoing interface** that the FIB uses to reach that source IP.
* In asymmetric routing environments, the router's best route back to the external source points out Gi0/1. When return traffic enters via Gi0/2, the incoming interface (Gi0/2) does not match the FIB interface (Gi0/1), causing Strict uRPF to drop the packets.
* **Solution:** In asymmetric networks, **Loose Mode uRPF (`reachable-via any`)** must be used instead, which verifies only that a valid route to the source IP exists in the FIB regardless of incoming interface.
* Distractor analysis: Option A describes Loose mode behavior. Options C and D describe actions that uRPF does not perform.

---

### Scenario 10: Cisco IOS Embedded Event Manager (EEM) - Automated Troubleshooting
**Topology Background:**  
A network engineer creates an EEM applet to automatically capture diagnostics whenever an OSPF neighbor relationship on interface GigabitEthernet0/1 transitions from FULL to DOWN:
```ios
event manager applet OSPF_NEIGHBOR_DOWN
 event syslog pattern "OSPF-5-ADJCHG: Process 1, Nbr .* on GigabitEthernet0/1 from FULL to DOWN"
 action 1.0 cli command "enable"
 action 2.0 cli command "show ip interface brief"
 action 3.0 cli command "show log | append flash:ospf_crash.log"
```
What event detector triggers this applet, and how does the EEM engine execute the actions?

* A. An interface hardware counter detector; executes actions concurrently in separate background threads
* B. A Syslog event detector matching a regular expression pattern; executes CLI actions sequentially based on line numbering
* C. An SNMP polling trap detector; executes only when CPU utilization exceeds 90%
* D. A timer-based cron detector; executes once every 60 seconds

**Correct Answer:** **B**

**Detailed Technical Explanation:**  
* In Cisco IOS EEM:
  * The statement `event syslog pattern "..."` registers a **Syslog Event Detector**. When the Cisco IOS syslog facility logs a message matching the specified regular expression, the EEM applet is triggered.
  * The `action <label> cli command "..."` statements define the payload actions. The EEM engine evaluates and executes actions **sequentially in alphanumeric order** according to their action labels (`1.0`, then `2.0`, then `3.0`).
* Distractor analysis: Option A is incorrect because the trigger is a syslog pattern, not an interface counter, and actions are executed sequentially, not multithreaded. Option C refers to SNMP MIB event detectors. Option D describes timer event detectors (`event timer cron`).

---

## 5. Recommended Study Resources & Official Documentation

* [Cisco 300-410 ENARSI Official Certification Blueprint](https://learningnetwork.cisco.com/s/enarsi-exam-topics)
* [Cisco Press: CCNP Enterprise Advanced Routing and Services ENARSI 300-410 Official Cert Guide](https://www.ciscopress.com/)
* [300-410 Practice Test - CertsClub](https://www.certsclub.com/cisco/) (Use coupon `club20` for 20% off)
* [Cisco Modeling Labs (CML) Enterprise Network Simulation](https://www.cisco.com/c/en/us/products/cloud-systems-management/modeling-labs/index.html)
* [Cisco Validated Designs: Campus Network for High Availability Design Guide](https://www.cisco.com/c/en/us/solutions/design-zone.html)
* [RFC 4364: BGP/MPLS IP Virtual Private Networks (VPNs)](https://datatracker.ietf.org/doc/html/rfc4364)

---

## 6. SEO Keywords & Search Index Topics

```
300-410, 300-410 exam, 300-410 practice test, 300-410 study guide, cisco 300-410,
enarsi, cisco enarsi, ccnp enterprise enarsi, ccnp advanced routing, enarsi practice exam,
certsclub 300-410, bgp best path selection algorithm, ospf totally nssa no-summary,
eigrp named mode variance feasibility condition, mutual redistribution route tagging,
mpls l3vpn rd vs rt, dmvpn phase 3 nhrp redirect shortcut, ip local policy pbr,
control plane policing copp, urpf strict vs loose mode, cisco eem applet syslog
```

---

## 7. Community Discussions & Contributions

* **Advanced Topology Scenarios:** Join enterprise routing labs and configuration reviews in [GitHub Discussions](../../discussions).
* **Issue Submissions & Errata:** To submit an errata or suggest a complex routing scenario, open a ticket via [GitHub Issues](../../issues).
* **CML Lab Contributions:** Topology submissions in Cisco Modeling Labs (`.yaml`) format covering ENARSI blueprint topics are welcomed via Pull Requests.

---
*Maintained by the Cisco Certified Curriculum Community. Contributions and pull requests are welcomed.*
