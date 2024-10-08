# Active-Directory

## Objective

Set up an Active Directory (AD) monitoring home lab with telemetry collection by deploying a Windows Server environment to generate and analyze real-time AD telemetry data for detecting and responding to security events, enhancing incident detection, and response capabilities. The setup will be tested using a Kali Linux crowbar attack to enhance incident detection and response capabilities

### Skills Learned

- Active Directory (AD) Administration:
    + Setting up and managing a Windows Server environment.
    + Configuring and managing AD services, users, groups, and permissions.

- Security Monitoring and Telemetry Collection:
    + Implementing telemetry collection tools and monitoring solutions for Active Directory.
    + Understanding various types of logs (e.g., security, event) and how to analyze them for suspicious activity.

- Incident Detection and Response:
    + Identifying indicators of compromise (IoCs) and patterns in AD telemetry data.
    + Developing and enhancing incident detection and response capabilities for AD environments.

- Offensive Security and Penetration Testing:
    + Conducting penetration testing using Kali Linux and tools like Crowbar to simulate real-world attack scenarios.
    + Understanding common attack vectors against AD, such as brute force, credential stuffing, and password spraying.

- Threat Hunting and Analysis:
    + Gaining skills in threat hunting within AD environments by identifying and analyzing suspicious behaviors.
    + Correlating telemetry data from various sources to uncover hidden threats.

- Networking and Systems Administration:
    + Managing network configurations, firewalls, and routing in a virtual lab environment.
    + Understanding the interaction between systems, networks, and AD services.

- Scripting and Automation:
    + Using PowerShell and other scripting languages to automate AD monitoring, alerting, and response actions.

### Tools Used

- Windows Server 2022: Set up as the AD Domain Controller for managing user accounts, groups, policies, and generating security logs.
- Sysmon (System Monitor): Provides detailed logging of system activity, including process creation, network connections, and file integrity changes.
- Splunk: Used for ingesting, parsing, visualizing, and analyzing logs and telemetry data from the AD environment.
- Kali Linux: A penetration testing distribution used for simulating various attack scenarios against the AD environment.
- Crowbar: A brute force tool for testing AD account credentials through SSH, RDP, and other protocols.
- PowerShell: Used for monitoring and responding to security events in AD.
- Oracle VirtualBox: Virtualization platform for creating and managing multiple virtual machines (VMs) in the lab setup.
- Ubuntu Server: As a logging or utility server.
- Windows 10: For testing and endpoint simulation.
- Atomic Red Team: For executing simulated attack techniques.
- Splunk Universal Forwarder: For collecting and forwarding telemetry data.

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
16. In Server Manager click on the flag icon at the top. Click promote this server to a domain controller. Since this is a brand new domain select add a new forest. Name it and create a new password.<br>
  ![18  win server root domain](https://github.com/user-attachments/assets/7c2ddbbc-841a-429a-922d-44920e3deccf)<br>
*Ref 19: New forest*
17. The paths screen indicates where the critical files for the domain are stored (ie: password hashes) that attackers want because it contains everything they need. If these files are unexpectedly altered/accessed then its safe to bet that your controller has been compromised. After all the verifications click install.<br>
  ![19  Paths to important server files](https://github.com/user-attachments/assets/c4e3bdf4-997c-4e28-b5f7-94fb2f0bdee4)<br>
*Ref 20: Paths to important server files*<br>
18. Log in and go to Server Manager, click tools and select Active Directory Users and Computers. This is where objects can be created.<br>
  ![20  AD users and computers](https://github.com/user-attachments/assets/c621b37d-3a4f-4880-8e26-47944b599f9c)<br>
*Ref 21: AD Users and Computers*<br>
19. Expand Domain and click built in to see the automatically created groups. Right click domain > select New > click Orginizational Unit.<br>
  ![21  New Orginizational Unit](https://github.com/user-attachments/assets/fc021bec-6d3f-4659-98ec-89fcf7e6320f)<br>
*Ref 22: New OU*<br>
  ![22  New ou name](https://github.com/user-attachments/assets/d00fee5f-6b0a-49dd-baa0-a39cd4266a53)<br>
*Ref 23: Name the new OU*<br>
20. Right click the newly created OU > select New > click User. Give it a name and password <br>
  ![23  New user in OU](https://github.com/user-attachments/assets/6b57bd2c-7c15-46c6-8c7d-e7f8229a1c3c)
*Ref 24: New User in OU*<br>
  ![24  New user name](https://github.com/user-attachments/assets/988dfc16-0f26-4f02-a017-47c58a52ff82)<br>
*Ref 25: New User name*<br>
  ![25  New user Password](https://github.com/user-attachments/assets/b9dc81b8-9e12-4f56-8628-3f26fe6ced5d)<br>
*Ref 26: New User Password*<br>
21. Create Anothe new OU and User.
22. Spin up the Windows 10 target machine, Navigate to "advanced systen settings". Click Computer name and change, select domain. If you get an error go to "network and internet settings" > change adapter options > right click adapter and select properties > click into IPv4 properties, xhange the DNS server to point to the Domain Controller.<br>
  ![26  Wins 10 machine ipv4 domain](https://github.com/user-attachments/assets/35a40ba1-4435-45fd-885c-d44f009ad65a)<br>
*Ref 27: IPv4 Properties*<br>
23. To check if the change is succesful. Open command prompt and type ipconfig /all to see the DNS server.<br>
  ![27  win 10 machine dns check](https://github.com/user-attachments/assets/23bd1372-c4f9-4acb-96bc-f6d8093539aa)<br>
*Ref 28: DNS check*<br>
24. Log into the Domain now with the admin account. It will then require a restart.<br>
  ![28  Domain login](https://github.com/user-attachments/assets/abe9aabf-064d-4d34-a2ee-e42b03196a02)<br>
*Ref 29: Domain login*<br>
  ![29  Domain login success](https://github.com/user-attachments/assets/01b81556-225f-430f-8c8c-40f6ccf538b9)<br>
*Ref 30: Domain login success*<br>
25. Log back in with a domain User created before.<br>
  ![30  win 10 machine sign in to other name pointed to domain](https://github.com/user-attachments/assets/4896e644-3563-4947-afdd-0ec1a2467540)<br>
*Ref 31: Sign in pointed to Domain*<br>
  ![31  login to jay smith](https://github.com/user-attachments/assets/1a58ef16-7f45-4d45-b7b1-735061ac6d8b)<br>
*Ref 32: User login*<br>
26. Spin up a Kali machine and setup a stativ IP for it. Right-click ethernet icon > click edit connections > select the first profile > click the cog icon > click IPv4 settings > save. Check in terminal with "ip a". If the IP was not changed Disconnect and reconnect the IP profile.<br>
  ![32  Kali edit connections](https://github.com/user-attachments/assets/65dfcbff-e0da-4fc3-b104-75e7499498e8)<br>
*Ref 33: Kali edit connections*<br>
  ![33  Kali Ipv4 settings](https://github.com/user-attachments/assets/a4a38e0c-7f7c-483e-80fb-8e6a1718d136)<br>
*Ref 34: Kali IPv3 settings*<br>
  ![34  Kali ip a](https://github.com/user-attachments/assets/650b3b76-3623-4ec9-9ced-8d3d3fa8115b)<br>
*Ref 35: Keli ip a*<br>
27. Update and Upgrade, then create a new directory.<br>
  ![35  kali mkdir](https://github.com/user-attachments/assets/323bbadc-533f-4288-890a-36483a4846c0)<br>
*Ref 36: Kali mkdir*<br>
28. Install crowbar and then cd to the wordlists directory.<br>
  ![36  kali crowbar install](https://github.com/user-attachments/assets/c4ec0237-466f-4612-8282-96739fa22ea5)<br>
*Ref 37: Install Crowbar*<br>
  ![37  kali cd wordlists](https://github.com/user-attachments/assets/6024bb50-5523-4c2e-9078-110e0eb7c9fe)<br>
*Ref 38: Cd wordlists*<br>
29. Extract rockyou and copy it to the new directory.<br>
  ![38  kali exract rockyou](https://github.com/user-attachments/assets/1d6f48a6-193c-4e8e-9fda-a9e12f94dbe7)<br>
*Ref 39: Exctract rockyou*<br>
  ![39  Kali rockyou copy](https://github.com/user-attachments/assets/e67c5659-81fb-45bf-be26-4adaf9f02d00)<br>
*Ref 40: Copy rockyou*<br>
30. Using the first 20 lines in the rockyou.txt output those out to a passwords.txt file then edit passwords.txt to add the password of the target machine.<br>
  ![40  kali first 20 rockyou](https://github.com/user-attachments/assets/3d444552-411c-4bc9-b169-978fddcf8e87)<br>
*Ref 41: First 20 lines rockyou*<br>
  ![41  kali output rockyou 20 to new file](https://github.com/user-attachments/assets/32b76c20-2d5b-4956-965d-ca38f12f9dc2)<br>
*Ref 42: Rockyou output to passwords.txt*<br>
  ![42  kali password txt edit](https://github.com/user-attachments/assets/33b519e3-3e13-4b41-a8ff-1e42873478dc)<br>
*Ref 43: Passwords.txt edit*<br>
31. Go to the Windows 10 target machine and enable RDP under properties in PC > then advanced system settings > remote tab. Click "Allow remote connections" > click select users > click add > add your users.<br>
  ![43  win target RDP users](https://github.com/user-attachments/assets/9ff9cc9b-aeae-4d13-8d7b-89b50f5a6ee9)<br>
*Ref 44: Windows target RDP users*<br>
32. Back on the Kali machine check help with crowbar -h on using the crowbar brute force tool.<br>
  ![44  kali crowbar -h](https://github.com/user-attachments/assets/5c2926d5-fa5b-4439-ab08-27227df8585b)<br>
*Ref 45: Kali crowbar -h*<br>
33. Crowbar -b signals brute force through RDP, -u to enter the target user, -C for the specified password list, and -s to enter the source IP.<br>
  ![45  kali start bruteforce](https://github.com/user-attachments/assets/a264de3b-88cb-41a9-a21d-7b15a84d0f9c)<br>
*Ref 46: Start brute force*<br>
34. On <a href="https://www.splunk.com/">Splunk</a>, click Search and Reporting > search " index=endpoint tsmith " and press enter. Find the EventCode showing the crowbar attack. by click on the Event id will filter it in Splunk where we can see the attempts that happened in quick succession, signalling an attack. If the Event id is googled, a decription of the type of attack will come up<br>
  ![46  win target machine event count crowbar attack](https://github.com/user-attachments/assets/5730eac6-8b02-46be-bbb8-c2151d654881)<br>
*Ref 47: Target amachine crowbar attack count*<br>
  ![47  event id description](https://github.com/user-attachments/assets/3a1fad3a-2c07-4ee1-afff-2134706fd8a2)<br>
*Ref 48: Event id description*<br>
35. Open PowerShell with administrative privileges on the target Windows machine > login with the administrator account > type in "Set-ExecutionPolicy Bypass CurrentUser".<br>
  ![48  PS execution policy](https://github.com/user-attachments/assets/ff4b7ae9-e4ca-44a9-ac01-f88ee36ea764)<br>
*Ref 49: PS execution policy*<br>
36. Set an exclusion for the C: drive so that defender does not delete any of the <a href="https://github.com/redcanaryco/atomic-red-team">Atomic Red Team</a> files. Go to add or remove exclusion under exclusions in virus & threat protection, add an exclusion for folder, click the C: drive and click select folder.<br>
  ![49  add an exclusion folder](https://github.com/user-attachments/assets/cbb8a65f-72a3-42a6-b2e4-e6b2b7704672)<br>
*Ref 50: Add exclusion folder*<br>
  ![50  C drive exclusion](https://github.com/user-attachments/assets/250bfaf5-b71f-4208-b10a-2210da7febd7)<br>
*Ref 51: Exclude C: drive*<br>
37. In PowerShell type in " IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing); Install-AtomicRedTeam -getAtomics".<br>
38. Go to Atomic Red Team directory > click atomics > the folders seen here correspond to the <a href="https://attack.mitre.org/">Mitre Att&ck</a> framework.<br>
39. Back in PowerShell type in "Invoke AtomicTest T1136.001"/<br>
  ![51  Atomic Test T1136 001](https://github.com/user-attachments/assets/ab71364d-c131-48fe-a544-825c70c957cd)<br>
*Ref 52: AtomicTest T1136.001*<br>
40. Go back to Splunk and sear for "NewLocalUser" account, If no telemetry try another attack.<br>
41. In PowerShell type in the Invoke command this time with T1059.001. If Defender caught somethings go to Splunk, change the time to last 15 minutes and NewLocalUser shows up.<br>
  ![52  ART new account generation](https://github.com/user-attachments/assets/423473be-324d-4f7d-b1a4-8d80a7387c67)<br>
*Ref 53: ART new account*<br>
  ![53  Another ART command](https://github.com/user-attachments/assets/e4e64e17-aa81-4410-bbaa-78efef830877)<br>
*Ref 54: Second ART command*<br>
  ![54  Splunk newlocaluser](https://github.com/user-attachments/assets/bc8bbcd1-462c-454d-92bf-4c843ad027d2)<br>
*Ref 55: Splunk NewLocalUser*<br>
