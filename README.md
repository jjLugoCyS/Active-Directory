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
6. Install Splunk Universal Forwarder on target machine. First assign a static IP to target machine on the NAT network created earlier.<br>
  ![9  Target machine static IP](https://github.com/user-attachments/assets/f71fd8fe-021b-4fb6-9e4d-8ed34d6b043e)<br>
*Ref 10: Target Machine Static IP*<br>
7. Find the SUF input.conf file on the target machine and modify it to gather telemetry.<br>
  ![10  splunk forwarder input conf file edit](https://github.com/user-attachments/assets/5edc1311-fd87-4893-aa31-3f1118516802)<br>
*Ref 11: input.conf file*<br>
8. Log into Splunk and navigate to indexes, click on new index button and create an endpoint index.<br>
  ![11  New endpoint index](https://github.com/user-attachments/assets/48653e4a-cf82-462b-b71e-1f4caaa4fcc6)<br>
*Ref 12: New endpoint index*<br>
9. Navigate to forwarding and receiving > configure receiving > new receiving port and enter a port number.<br>
  ![12  new receiving port](https://github.com/user-attachments/assets/59c8d242-5f27-4830-bba4-a882d3e0122b)<br>
*Ref 13: New receiving port*<br>
10. Click apps> search & reporting and type in "index=endpoint"<br>
  ![13  index search](https://github.com/user-attachments/assets/3f059198-3b73-47b7-8289-c0fa509b2614)<br>
*Ref 14: Index Search*<br>
11. Using the same steps as the target machine, install sysmon and splunk on the windows server.
12. Set a static IP on the Windows Server.<br>
  ![14  Win Server static IP](https://github.com/user-attachments/assets/d6c3c4ad-a5a7-4498-a6bf-c59236e4a5be)<br>
*Ref 15: Windows Server Static IP*<br>
13. Go to the Server Manager and click manage > add Roles and Features > click next.<br>
  ![15  wins server manager roles and feats](https://github.com/user-attachments/assets/fc6fde08-8c38-4230-aa7a-e49c05d4c996)<br>
*Ref 16: Manager, Roles and feats*<br>
14. Select Role-based or Feature-based.<br>
  ![16 roles and feeats server selection](https://github.com/user-attachments/assets/bd9b3317-ceb6-428f-a218-3ee6782e1345)<br>
*Ref 17: Roles and Feats. Server Selection<br>
15. Select Active Directory Domain Services and install. <br>
  ![17  R+F ADDS](https://github.com/user-attachments/assets/64b53b4e-2998-4c01-b4f1-5b7717d55fee)<br>
*Ref 18: Active Directory Domain Services*<br>
16.
