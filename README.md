# Problem 17 — Packet Dropping Simulation

**Name:** Shreelakshmi G Bhat &nbsp;|&nbsp; **SRN:** PES2UG24CS478 &nbsp;|&nbsp; **Section:** H

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

### Setup

![Setup](https://github.com/user-attachments/assets/ef002e1b-b3ad-41e7-afb7-42c826c5946e)

### Topology Initialization

![Topology initialization](https://github.com/user-attachments/assets/43f7f31f-cb0d-4308-810f-963b02ae65ff)

### Controller Setup

![Controller setup](https://github.com/user-attachments/assets/678ee89d-526f-4be0-845a-cdd043965bcb)

> **Topology justification:** The chosen topology is simple and effective — easy to understand and debug, clearly shows traffic flow, and is well-suited to demonstrating selective packet dropping.

---

## 2. Design & Implementation

### Packet-In Handling

![Packet-in handler](https://github.com/user-attachments/assets/310e3bd2-20ce-4c72-8035-3c6ceb28aa05)

### Match-Action Rule Design (`drop_controller.py`)

![drop_controller.py](https://github.com/user-attachments/assets/a245c0d9-bdb7-4139-b421-755d0e20e3a3)

### Flow-Rule Installation

![Flow rule installation](https://github.com/user-attachments/assets/b0f9b9dc-0e56-42ac-b70d-324fd6faa986)

### Priority & Matching

![Priority and matching](https://github.com/user-attachments/assets/b0f9b9dc-0e56-42ac-b70d-324fd6faa986)

---

## 3. Functional Correctness

### Baseline Connectivity

![Baseline connectivity](https://github.com/user-attachments/assets/4554a9c8-cfbd-4fcc-84ad-5424a7ac2ee2)

### Packet Drop with Errors

![Packet drop output](https://github.com/user-attachments/assets/a72577a4-ee40-49d0-9872-b9be8a0292d6)

### Selective Filtering

![Selective filtering](https://github.com/user-attachments/assets/bb37e102-f4ec-46f1-8b48-ea81d223cbbf)

---

## 4. Performance Observation & Analysis

### Packet Loss

![Packet loss](https://github.com/user-attachments/assets/a72577a4-ee40-49d0-9872-b9be8a0292d6)

### Latency

![Latency](https://github.com/user-attachments/assets/5d6cb14b-b205-4acb-869b-ad9075e6b899)

### Throughput

![Throughput](https://github.com/user-attachments/assets/11edab52-8437-4883-b40b-2c18e9bdd6dc)

### Flow Table

![Flow table](https://github.com/user-attachments/assets/7738fed6-281d-4d15-a8cf-885354771226)

---

## 5. Validation & Testing

### Validation

**Before adding the controller:**

![Before controller](https://github.com/user-attachments/assets/dc7dc4c2-d06a-4288-b1e3-ea975d6a25b9)

**After adding the controller:**

![After controller](https://github.com/user-attachments/assets/4c539a42-aa32-403e-b7df-5344277f7ed6)

### Regression Testing

![Regression test 1](https://github.com/user-attachments/assets/642c5f4f-1a03-42f0-97bd-bbcd62278181)

![Regression test 2](https://github.com/user-attachments/assets/5822bf7b-5cca-4f80-a134-8304dba73315)
