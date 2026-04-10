# CN Orange Problem : Problem 17: Packet Dropping Simulation

**Name:** Shreelakshmi G Bhat | **SRN:** PES2UG24CS478 | **Section:** H

---

## 1. Problem Overview

### Problem Statement

Design and implement an SDN-based solution using Mininet and an OpenFlow controller to simulate packet loss behavior in a network. The system demonstrates how flow rules can be used to selectively drop packets and control traffic dynamically.

### Objectives

- Add drop rules in the network using SDN
- Choose and control specific data flows between hosts
- Measure how much packet loss occurs after applying rules
- Observe network behavior when packets are dropped
- Perform regression testing to verify rules remain effective

---

### Setup

![Setup](https://github.com/user-attachments/assets/ef002e1b-b3ad-41e7-afb7-42c826c5946e)


---

### Topology Initialization

![Topology initialization](https://github.com/user-attachments/assets/43f7f31f-cb0d-4308-810f-963b02ae65ff)

A simple linear topology is initialized with three hosts (h1, h2, h3) connected to a single OpenFlow switch (s1). The switch is configured to communicate with the Ryu controller over the OpenFlow 1.3 protocol. This topology makes it straightforward to observe selective traffic dropping between specific host pairs.

---

### Controller Setup

![Controller setup](https://github.com/user-attachments/assets/678ee89d-526f-4be0-845a-cdd043965bcb)

The Ryu controller is launched with a custom application (`drop_controller.py`) that listens for OpenFlow events. It connects to the switch on the default OpenFlow port (6633/6653) and begins handling `packet_in` events to make forwarding and dropping decisions dynamically.

---

> **Topology justification:** The chosen topology is simple and effective — easy to understand and debug, clearly shows traffic flow, and is well-suited to demonstrating selective packet dropping.

---

## 2. Design & Implementation

### Packet-In Handling

![Packet-in handler](https://github.com/user-attachments/assets/310e3bd2-20ce-4c72-8035-3c6ceb28aa05)

When a packet arrives at the switch with no matching flow rule, it is sent to the controller as a `packet_in` event. The handler parses the Ethernet frame and extracts IP header fields — specifically the source and destination IP addresses. Based on this inspection, the controller decides whether to install a drop rule or forward the packet.

---

### Match-Action Rule Design (`drop_controller.py`)

![drop_controller.py](https://github.com/user-attachments/assets/a245c0d9-bdb7-4139-b421-755d0e20e3a3)

The controller script defines match criteria using OpenFlow's `OFPMatch`, targeting packets with a specific source IP (h1: `10.0.0.1`) and destination IP (h2: `10.0.0.2`). The corresponding action list is left **empty**, which instructs the switch to drop matching packets. For all other traffic, a normal forwarding action (flood) is applied.

---

### Flow-Rule Installation

![Flow rule installation](https://github.com/user-attachments/assets/b0f9b9dc-0e56-42ac-b70d-324fd6faa986)

Flow rules are installed using `OFPFlowMod` messages sent from the controller to the switch. Each rule specifies a match condition, an action (or no action for drops), a priority, and an idle timeout. Once installed, the switch enforces the rule for all subsequent matching packets without involving the controller again.

---

### Priority & Matching

![Priority and matching](https://github.com/user-attachments/assets/b0f9b9dc-0e56-42ac-b70d-324fd6faa986)

The drop rule is assigned a **higher priority** than the default forwarding rule. OpenFlow switches always apply the highest-priority matching rule first. This ensures that h1→h2 traffic is caught and dropped before any lower-priority forwarding rules can apply. Other flows (e.g., h1→h3, h2→h3) match only the lower-priority forwarding rule and are handled normally.

**Technical Explanation:**

The controller dynamically installs flow rules upon receiving `packet_in` events from the switch. It inspects packet headers (source and destination IP) and applies match-action logic. If the packet matches the defined condition (h1 → h2), a high-priority rule with no actions is installed, effectively dropping the packet. Otherwise, packets are forwarded normally using flooding.

The implementation uses **OpenFlow 1.3** protocol for communication between the switch and the controller, ensuring compatibility with modern SDN features.

---

## 3. Functional Correctness

### Baseline Connectivity

![Baseline connectivity](https://github.com/user-attachments/assets/4554a9c8-cfbd-4fcc-84ad-5424a7ac2ee2)

Before the drop controller is applied, all hosts can communicate freely. A `pingall` test in Mininet confirms 0% packet loss across all host pairs (h1↔h2, h1↔h3, h2↔h3), establishing a working baseline for comparison.

---

### Packet Drop with Errors

![Packet drop output](https://github.com/user-attachments/assets/a72577a4-ee40-49d0-9872-b9be8a0292d6)

After the drop controller is activated, pinging from h1 to h2 results in 100% packet loss. The ICMP requests are silently discarded by the switch due to the installed drop rule. The output shows repeated timeouts with no replies received, confirming the rule is actively enforced.

---

### Selective Filtering

![Selective filtering](https://github.com/user-attachments/assets/bb37e102-f4ec-46f1-8b48-ea81d223cbbf)

To verify selectivity, pings from h1→h3 and h2→h3 are tested while the h1→h2 drop rule is active. These flows succeed with 0% packet loss, confirming that only the targeted flow (h1→h2) is dropped. All other traffic is unaffected, demonstrating fine-grained, flow-level control.

<img width="1923" height="1176" alt="image" src="https://github.com/user-attachments/assets/9e3458eb-919c-4012-862f-58d5a09bc456" />
<img width="1936" height="1408" alt="image" src="https://github.com/user-attachments/assets/f271d92c-f0ad-4747-a1c9-088403682dc4" />
<img width="1885" height="1104" alt="image" src="https://github.com/user-attachments/assets/1d925ec4-5bf7-4297-9c95-eef98cdc7c1c" />
<img width="1901" height="1390" alt="image" src="https://github.com/user-attachments/assets/ad578cce-63b7-4e92-b691-b16f335eeebe" />
<img width="1911" height="1369" alt="image" src="https://github.com/user-attachments/assets/9130e43d-2037-48f1-b6e8-5abdb556b47d" />
<img width="2007" height="1439" alt="image" src="https://github.com/user-attachments/assets/3505e91d-7d3a-46b2-97ca-cb78f8ad92bb" />

Explanation of Wireshark screenshots: 
The screenshots demonstrate both blocked and allowed traffic scenarios in the SDN-enabled network. In the first case, traffic from h1 (10.0.0.1) to h2 (10.0.0.2) results in 100% packet loss, as observed from the Mininet ping output. Correspondingly, the Wireshark capture shows ICMP Echo Requests being sent but no Echo Replies, confirming that packets are being dropped due to the installed flow rule. In contrast, communication between h2 (10.0.0.2) and h3 (10.0.0.3) is successful, with 0% packet loss and visible ICMP request–reply exchanges in Wireshark. This validates that the controller enforces selective packet dropping, affecting only the specified flow while allowing all other traffic to pass normally.
---

## 4. Performance Observation & Analysis

### Packet Loss

![Packet loss](https://github.com/user-attachments/assets/a72577a4-ee40-49d0-9872-b9be8a0292d6)

The ping test between h1 and h2 shows **100% packet loss** after the drop rule is installed. No ICMP echo replies are received, confirming total suppression of the targeted flow. All other host pairs maintain 0% loss, validating the selectivity of the implementation.

---

### Latency

![Latency](https://github.com/user-attachments/assets/5d6cb14b-b205-4acb-869b-ad9075e6b899)

For flows that are permitted (e.g., h1→h3), latency remains low and consistent. A slight increase may be observed on the very first packet of any new flow, as it triggers a `packet_in` event and waits for the controller to install a rule. Subsequent packets in the same flow are handled at line rate by the switch with no controller overhead.

---

### Throughput

![Throughput](https://github.com/user-attachments/assets/11edab52-8437-4883-b40b-2c18e9bdd6dc)

Throughput between h1 and h2 drops to **zero** as all packets are silently discarded by the switch. For other host pairs, throughput is measured using `iperf` and remains at the expected level for the emulated link, showing no degradation from the drop rules applied to unrelated flows.

---

### Flow Table

![Flow table](https://github.com/user-attachments/assets/7738fed6-281d-4d15-a8cf-885354771226)

The flow table on switch s1 is inspected using `ovs-ofctl dump-flows s1`. It shows two entries: a high-priority drop rule matching src=10.0.0.1, dst=10.0.0.2 with an empty action list, and a lower-priority flood rule for all other traffic. The packet and byte counters on the drop rule increment with each blocked packet, confirming active enforcement.

**Analysis:**

The packet loss observed for traffic between h1 and h2 is approximately **100%**, due to the installed drop rule. Other traffic flows remain unaffected, demonstrating selective filtering capability. Latency may increase slightly during initial packet transmission due to controller involvement. Throughput between blocked hosts drops to zero, confirming effective enforcement of the rule.

---

## 5. Validation & Testing

### Validation

**Before adding the controller:**

![Before controller](https://github.com/user-attachments/assets/dc7dc4c2-d06a-4288-b1e3-ea975d6a25b9)

With no custom controller active, the switch operates in default learning/flooding mode. All hosts can reach each other, and `pingall` reports full connectivity with 0% packet loss across the network.

---

**After adding the controller:**

![After controller](https://github.com/user-attachments/assets/4c539a42-aa32-403e-b7df-5344277f7ed6)

Once the drop controller is connected, the `pingall` test shows that h1→h2 fails (100% loss) while all other pairs succeed. This validates that the controller is correctly intercepting traffic and enforcing the defined drop policy without disrupting unrelated flows.

---

### Regression Testing

![Regression test 1](https://github.com/user-attachments/assets/642c5f4f-1a03-42f0-97bd-bbcd62278181)

![Regression test 2](https://github.com/user-attachments/assets/5822bf7b-5cca-4f80-a134-8304dba73315)

Regression tests are run by restarting the Mininet topology and reconnecting the controller to verify that drop rules are consistently re-applied and that previously passing flows continue to work correctly. Both test runs confirm the same behavior: h1→h2 is dropped, all other flows pass. This ensures the solution is stable and repeatable across sessions.

---





## 6. Conclusion

This project demonstrates how Software Defined Networking (SDN) enables programmable and fine-grained control over network traffic. By using a centralized controller and OpenFlow-based rules, specific traffic flows can be selectively dropped, allowing simulation of packet loss scenarios. The experiment highlights the flexibility and power of SDN in managing modern networks.

---
