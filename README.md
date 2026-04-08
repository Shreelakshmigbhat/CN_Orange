CN ORANGE PROBLEM 
PACKET DROPPING SIMULATION 


1. i) Problem Statement

The objective of this project is to design and implement a Software Defined Networking (SDN) based solution using Mininet and an OpenFlow controller to simulate packet loss behavior in a network. The system should demonstrate how flow rules can be used to selectively drop packets and control traffic dynamically.

   ii) Objective 
->To add drop rules in the network using SDN
->To choose and control specific data flows between hosts
->To check how much packet loss happens after applying rules
->To observe how the network behaves when packets are dropped
->To test again (regression testing) and make sure the rules still work properly
  
  iii) Mininet creation:
  <img width="1674" height="947" alt="image" src="https://github.com/user-attachments/assets/ef002e1b-b3ad-41e7-afb7-42c826c5946e" />
      Topology initialization:
<img width="1133" height="641" alt="image" src="https://github.com/user-attachments/assets/43f7f31f-cb0d-4308-810f-963b02ae65ff" />





mininet setup:
<img width="1337" height="1089" alt="image" src="https://github.com/user-attachments/assets/703106cb-cfc0-425b-8c9c-d072d85763aa" />

<img width="405" height="205" alt="image" src="https://github.com/user-attachments/assets/66052d87-27ab-4a6b-8213-546ea7c9178b" />

Baseline setup:
<img width="1559" height="1175" alt="image" src="https://github.com/user-attachments/assets/f2022e30-feca-4545-a0a3-c17971aab7af" /> <img width="1355" height="1113" alt="image" src="https://github.com/user-attachments/assets/678ee89d-526f-4be0-845a-cdd043965bcb" />

using My controller: 

drop_controller.py file :
<img width="1735" height="1464" alt="image" src="https://github.com/user-attachments/assets/a245c0d9-bdb7-4139-b421-755d0e20e3a3" />


<img width="757" height="490" alt="image" src="https://github.com/user-attachments/assets/310e3bd2-20ce-4c72-8035-3c6ceb28aa05" />
<img width="1262" height="524" alt="image" src="https://github.com/user-attachments/assets/0f470748-fd61-4afe-a071-89a2082ccfa1" />
<img width="810" height="707" alt="image" src="https://github.com/user-attachments/assets/6d23ab9f-b528-471d-8979-845eaad06c38" />

<img width="1382" height="444" alt="image" src="https://github.com/user-attachments/assets/b0f9b9dc-0e56-42ac-b70d-324fd6faa986" />

<img width="559" height="200" alt="image" src="https://github.com/user-attachments/assets/aa8c960e-246e-44c7-9dfa-061d4a8da840" />

regression :
<img width="1400" height="807" alt="image" src="https://github.com/user-attachments/assets/00125193-54ba-4ec6-ad18-6f31dbece4bf" />

<img width="1512" height="1116" alt="image" src="https://github.com/user-attachments/assets/795eb9b1-7d13-44a7-b332-83a284a8d47a" />







