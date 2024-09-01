# Active-Directory

## Objective
[Brief Objective - Remove this afterwards]

The Detection Lab project aimed to establish a controlled environment for simulating and detecting cyber attacks. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system, generating test telemetry to mimic real-world attack scenarios. This hands-on experience was designed to deepen understanding of network security, attack patterns, and defensive strategies.

### Skills Learned
[Bullet Points - Remove this afterwards]

- Advanced understanding of SIEM concepts and practical application.
- Proficiency in analyzing and interpreting network logs.
- Ability to generate and recognize attack signatures and patterns.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used
[Bullet Points - Remove this afterwards]

- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Network analysis tools (such as Wireshark) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.

## Steps
1. Create a diagram on <a href="https://Draw.io"> Draw.io</a>
  ![Untitled Diagram](https://github.com/user-attachments/assets/d54d7780-fd52-4e89-87d8-1ecac39c5514)<br>
*Ref 1: AD Diagram*
2. Install Virtual box with a Windows 10 VM, a Kali Linux VM, a Windows Server 2022 VM, and a Splunk Server VM. Can also be installed in a cloud enviroment if preferred.
3. Create a NAT network and set all VMs to use that network.
  ![1  Create a NAT network for VMS](https://github.com/user-attachments/assets/d07ccd63-bf70-4503-9ec4-c4c5f377831f)<br>
*Ref 2: Create NAT network*<br>
  ![2  Set VMs to NAT network](https://github.com/user-attachments/assets/d2dbf52e-9d62-41f3-ae84-260c909fc929)<br>
*Ref 3: Set VMs to NAT network*<br>
4. Spin up the Splunk server to setup a static IP. Open up the init.yaml for your Splunk. Turn off dhcp for the server, add an address, a nameserver, a DNS, and setup a route for the server.
  ![3  Splunk network config](https://github.com/user-attachments/assets/067bd341-bb1f-437b-b45c-26226139e85e)<br>
*Ref 4: Splunk server network config*<br>
5. Install Splunk on the host machine and move it to the Splunk server. In virtualbox setup a shared folder. Mount the created folder in the Splunk Server. Install Splunk onto the server and start Splunk. Setup up the server to sater splunk on start up.<br>
  ![4  Shared folder settings for splunk install](https://github.com/user-attachments/assets/db9cd807-324c-417a-bd39-cd10aa9b26b4)<br>
*Ref 5: Shared folder*<br>
  ![5  Splunk Server shared folder mount](https://github.com/user-attachments/assets/1a47c435-045a-45da-b41a-5349c6ebcdf9)<br>
*Ref 6: Mount shared folder*<br>
  ![6  Install Splunk on server](https://github.com/user-attachments/assets/227aa779-375d-4d5a-a74f-666f79dca8dc)<br>
*Ref 7: Install Splunk on Server*<br>
  ![7  Splunk start](https://github.com/user-attachments/assets/05bd3ef8-65a6-4873-b25a-93062a398eec)<br>
*Ref 8: Start Splunk*<br>
  ![8  Splunk on start up command](https://github.com/user-attachments/assets/f88fd547-ba14-443d-a9a8-13233d3545d3)<br>
*Ref 9: Splunk on startup*<br>
6. 

