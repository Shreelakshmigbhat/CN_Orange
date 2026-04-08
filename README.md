CN ORANGE PROBLEM
PACKET DROPPING SIMULATION USING SDN
🔹 1. Problem Understanding & Setup
1.1 Problem Statement

The objective of this project is to design and implement a Software Defined Networking (SDN) based solution using Mininet and an OpenFlow controller to simulate packet loss behavior in a network. The system demonstrates how flow rules can be used to selectively drop packets and control traffic dynamically.

1.2 Objective
To add drop rules in the network using SDN
To control specific flows between hosts
To measure packet loss after applying rules
To observe how the network behaves when packets are dropped
To perform regression testing to ensure rules work consistently
1.3 System Setup

Explanation:
Mininet is used to create a virtual network consisting of hosts and switches, enabling SDN experimentation without physical hardware.

1.4 Topology Initialization

Explanation:
A simple topology with 3 hosts (h1, h2, h3) and 1 switch (s1) is created to clearly observe traffic behavior.

1.5 Controller Setup

Explanation:
The Ryu controller is used to dynamically control traffic by installing flow rules in the switch.

1.6 Justification of Design

The chosen topology is simple and effective:

Easy to understand and debug
Clearly shows traffic flow
Suitable for demonstrating selective packet dropping
🔹 2. SDN Logic & Flow Rule Implementation
2.1 Packet_in Handling

Explanation:
When a packet has no matching rule, it is sent to the controller using a packet_in event, allowing dynamic decision-making.

2.2 Match–Action Rule Design

Explanation:
Flow rules follow:

Match: source and destination IP
Action: drop or forward

Traffic from h1 → h2 is dropped.

2.3 Flow Rule Installation

Explanation:
The controller installs rules into the switch. The drop rule is assigned high priority.

2.4 Priority & Matching Criteria

Explanation:

Source: 10.0.0.1
Destination: 10.0.0.2
Action: DROP
Priority ensures rule is applied first
🔹 3. Functional Correctness
3.1 Baseline Connectivity

Explanation:
Initially, all hosts communicate successfully (0% packet loss).

3.2 Packet Drop Simulation

Explanation:
After applying SDN rules, packet loss is observed (33% dropped).

3.3 Selective Filtering

Explanation:

h1 → h2 ❌ blocked
h2 → h3 ✅ allowed
🔹 4. Performance Observation & Analysis
4.1 Packet Loss

Explanation:
Packet loss confirms successful traffic filtering.

4.2 Latency

Explanation:
Blocked packets cause delays and timeouts.

4.3 Throughput

Explanation:

Blocked flows → no throughput
Allowed flows → normal throughput
4.4 Flow Table Analysis

Explanation:
Flow table confirms correct rule installation.

4.5 Observed Behavior
Normal operation before rules
Packet loss after applying SDN logic
Selective filtering achieved
Performance affected accordingly
🔹 5. Validation & Testing
5.1 Validation
Before Controller

After Controller

Explanation:
Change from 0% to 33% packet loss confirms correctness.

5.2 Regression Testing




Explanation:
After restarting, the same behavior is observed, proving consistency.

🔹 6. Conclusion

This project demonstrates how SDN enables dynamic control of network behavior. By implementing a custom controller, selective packet dropping was achieved, proving the flexibility and power of SDN.
