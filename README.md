# CN ORANGE PROBLEM
## Problem 17: Packet Dropping Simulation

### Name: Shreelakshmi G Bhat  
### SRN: PES2UG24CS478  
### Section: H
1.
    i) Problem Statement

   The objective of this project is to design and implement a Software Defined Networking (SDN) based solution using         Mininet and an OpenFlow controller to simulate packet loss behavior in a network. The system should demonstrate         how flow rules can be used to selectively drop packets and control traffic dynamically.

    ii) Objective 
     ->To add drop rules in the network using SDN\
     ->To choose and control specific data flows between hosts\
     ->To check how much packet loss happens after applying rules\
     ->To observe how the network behaves when packets are dropped\
     ->To test again (regression testing) and make sure the rules still work properly\
  
    iii) setup:
  <img width="1674" height="947" alt="image" src="https://github.com/user-attachments/assets/ef002e1b-b3ad-41e7-afb7-42c826c5946e" />
  
    iv)Topology initialization:
<img width="1133" height="641" alt="image" src="https://github.com/user-attachments/assets/43f7f31f-cb0d-4308-810f-963b02ae65ff" />
    v) Controller setup:
  <img width="1355" height="1113" alt="image" src="https://github.com/user-attachments/assets/678ee89d-526f-4be0-845a-cdd043965bcb" />

Justification:

2. i) packet in handling:
   <img width="757" height="490" alt="image" src="https://github.com/user-attachments/assets/310e3bd2-20ce-4c72-8035-3c6ceb28aa05" />
   
   ii) match action rule design:
   drop_controller.py file ->
<img width="1735" height="1464" alt="image" src="https://github.com/user-attachments/assets/a245c0d9-bdb7-4139-b421-755d0e20e3a3" />

   iii) flow-rule installation:
   <img width="1382" height="444" alt="image" src="https://github.com/user-attachments/assets/b0f9b9dc-0e56-42ac-b70d-324fd6faa986" />

   iv) Priority & Matching:
   <img width="1382" height="444" alt="image" src="https://github.com/user-attachments/assets/b0f9b9dc-0e56-42ac-b70d-324fd6faa986" />

3.Functional Corrcectness:

   i) Baseline connectivity:
   <img width="1133" height="641" alt="image" src="https://github.com/user-attachments/assets/4554a9c8-cfbd-4fcc-84ad-5424a7ac2ee2" />

   ii) Packet drop with errors:
   <img width="1262" height="524" alt="image" src="https://github.com/user-attachments/assets/a72577a4-ee40-49d0-9872-b9be8a0292d6" />

   iii) Selective Filtering:
   <img width="810" height="707" alt="image" src="https://github.com/user-attachments/assets/bb37e102-f4ec-46f1-8b48-ea81d223cbbf" />

4. Performance Observation & Analysis:

    i) Packet loss:
     <img width="1262" height="524" alt="image" src="https://github.com/user-attachments/assets/a72577a4-ee40-49d0-9872-b9be8a0292d6" />

    ii)Latency:
   <img width="810" height="707" alt="image" src="https://github.com/user-attachments/assets/5d6cb14b-b205-4acb-869b-ad9075e6b899" />

    iii)Throughput:
   <img width="559" height="200" alt="image" src="https://github.com/user-attachments/assets/11edab52-8437-4883-b40b-2c18e9bdd6dc" />

    iv) Flow Table:
   <img width="1382" height="444" alt="image" src="https://github.com/user-attachments/assets/7738fed6-281d-4d15-a8cf-885354771226" />


5.
 i) Validation :

   Before adding controller :
   <img width="1133" height="641" alt="image" src="https://github.com/user-attachments/assets/dc7dc4c2-d06a-4288-b1e3-ea975d6a25b9" />

   After adding controller :
  <img width="1262" height="524" alt="image" src="https://github.com/user-attachments/assets/4c539a42-aa32-403e-b7df-5344277f7ed6" />


ii) regression testing 
<img width="1512" height="1116" alt="image" src="https://github.com/user-attachments/assets/642c5f4f-1a03-42f0-97bd-bbcd62278181" />
<img width="1400" height="807" alt="image" src="https://github.com/user-attachments/assets/5822bf7b-5cca-4f80-a134-8304dba73315" />






   
   


   












