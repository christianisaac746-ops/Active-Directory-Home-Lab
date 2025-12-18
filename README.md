# Active-Directory-Home-Lab
This is an active directory home lab I made following a tutorial by Josh Madakor.  
Active Directory Home Lab: From Scratch Implementation
A Micro-System Replication for Cybersecurity Portfolio

**Professional Preface**
As an IT Department member for McLoud Public Schools, my day-to-day responsibilities rely heavily on managing user accounts and infrastructure within our Active Directory (AD) environment. I routinely use AD to:

Manage Faculty and Staff Accounts: Adding, moving, and deleting user accounts for teachers and faculty between different Organizational Units (OUs), representing various schools within the district.

Handle Account Maintenance: Performing essential security functions like password resets to ensure smooth and secure daily operations.

This home lab project was undertaken to demonstrate my foundational understanding of AD architecture by successfully recreating a functional, micro-scale version of the AD environment I manage daily. The goal was to build a domain controller from the ground up, proving the ability to deploy and configure this critical infrastructure service.

**Project Summary**
This project documents the step-by-step process of establishing a functional Active Directory domain controller within a virtualized lab environment. This micro-system replication demonstrates proficiency in fundamental Windows Server roles, network configuration, and core Active Directory concepts necessary for enterprise identity and access management.

**Project Objectives**
Server Setup & Configuration: Deploy a base Windows Server 2019/2022 virtual machine.

**Network Configuration:** Configure the server with a static IP address for reliable domain services.

**Role Installation:** Install the Active Directory Domain Services (AD DS) role.

**Domain Promotion:** Promote the server to a Domain Controller (DC) and establish a new AD Forest and Domain.

**Organizational Unit (OU) Creation:** Recreate a logical structure of OUs similar to the McLoud Public Schools environment (e.g., separating administrative users from faculty).

**User and Group Management:** Demonstrate the ability to create, manage, and move users and groups, including password resets.

**Implementation Steps (Walkthrough)**
The following high-level steps outline the process used to deploy the Active Directory environment.

**1. Base OS and Initial Setup**
Virtual Machine (VM) Deployment: Installed Windows Server (e.g., 2019 or 2022) on a virtualization platform (e.g., Hyper-V or VMware).

**Static IP Assignment:** Configured a static IP address, subnet mask, and a local DNS entry for the server. (Crucial for reliable domain service location.)

**2. Installing Active Directory Domain Services (AD DS)**
Used the Server Manager console to add the Active Directory Domain Services role.

Confirmed necessary features and tools (like the AD administrative center) were installed.

**3. Promoting to Domain Controller**
After the role installation, initiated the Domain Controller Promotion wizard.

Selected "Add a new forest" and defined the root domain name (e.g., mcloudlab.local).

Specified the Domain and Forest Functional Level and set the Directory Services Restore Mode (DSRM) password.

**4. Creating the Organizational Unit (OU) Structure**
To mirror the real-world environment, a basic OU structure was created to facilitate policy application and user management (Note these are not the same as what I really use, these examples):

**Primary OUs:** McLoud-HighSchool, McLoud-MiddleSchool, Administration.

**Sub-OUs (within school OUs):** Teachers, Students, IT-Staff.

**5. Demonstrating Account Management (User/Group Provisioning)**
User Creation: Created test accounts (e.g., JSmith and ASmith) within the Teachers OU of the respective schools.

**Group Creation:** Created a security group (e.g., McLoud-Teachers-Group) and added the user accounts.

**Account Mobility:** Successfully moved a user object from the McLoud-MiddleSchool\Teachers OU to the McLoud-HighSchool\Teachers OU to simulate a change in school assignment.

**Password Management:** Performed a simulated password reset for one of the test accounts.
**Skills Demonstrated:**

<img width="682" height="264" alt="Image" src="https://github.com/user-attachments/assets/cb75bccc-a7f8-418b-bf05-9e8616359141" />

**Visual Representation of HomeLab:**

<img width="624" height="370" alt="Image" src="https://github.com/user-attachments/assets/2e68f977-6ccc-4826-ac14-c7d504e3349f" />


**Walkthrough:**
**Downloading Clients:**

I downloaded VirtualBox 7.2.4 and the VirtualBox 7.2.4 Extension Pack using the following link: (https://www.virtualbox.org/wiki/Downloads)

<img width="608" height="389" alt="Image" src="https://github.com/user-attachments/assets/82341ac0-1095-422c-9586-4dec17c9731f" />

I then downloaded a Windows 10 ISO here: (https://www.microsoft.com/en-us/software-download/windows10#d2784474-fdb0-4e9d-9e47-5e88c0e053ec)

<img width="1427" height="642" alt="Image" src="https://github.com/user-attachments/assets/2c0a1fe0-36d8-473d-b328-79501a2cae7a" />

I then downloaded a Windows Server 2019: (https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)

<img width="611" height="263" alt="Image" src="https://github.com/user-attachments/assets/2ccaff84-367a-41af-992a-146a98f08982" />

**Create The Virtual Machines:**

First, I opened up Oracle VirtualBox, and in the upper left corner, I click ‘New’. I name this one ‘Domain Controller’, select ‘Other Windows (64-bit)’ as the OS version, and then hit ‘Next’.

<img width="624" height="483" alt="Image" src="https://github.com/user-attachments/assets/21bc0b97-84ea-477f-9759-bd54aa172b5c" />

Here, I select 2048 MB (2 GB) of Base Memory, 4 CPUs ( You don’t have to use 4, but I wanted to speed things up a bit), and 20 GB for Disk Size. After that I select ‘Next’, and then ‘Finish’.

<img width="550" height="263" alt="Image" src="https://github.com/user-attachments/assets/065a36c1-f823-4c2e-957c-f2e86a34528d" />

Next, I clicked on ‘Settings’, and then selected the ‘Expert’ tab at the top, and then the ‘Network’ tab on the left hand column. Referring back to the Visual Representation I made at the beginning, I know I need two Network Adapters branching off of my Domain Controller for internet access and internal access. 
The first adapter will be NAT, acting as a single point of translation between the internal network, and the public internet (NAT is used to conserve public IP addresses, and provide security). 

<img width="541" height="440" alt="Image" src="https://github.com/user-attachments/assets/d8444d14-2e8c-4b81-a912-4d48edf72351" />

Then I select the ‘Adapter 2’ tab,  check ‘Enable Network Adapter’, and (referring back to the Visual Representation) I select ‘Internal Network’ in the ‘Attached to’ drop down menu.
I click ‘Ok’ and close out of the ‘Settings’ menu. 
Right now the VM1 (our first Virtual Machine) is configured, however its is still empty (doesn’t have Server 19 attached).
So. Let’s fix that.
Double click the ‘Domain Controller’ to start it.

<img width="462" height="258" alt="Image" src="https://github.com/user-attachments/assets/361629d7-3807-483a-825f-5077c289a416" />

After double-clicking, I select the Windows Server 19 ISO in the drop down menu, and then press ‘Mount and Retry Boot’.
And, look at that, we are in.

<img width="510" height="310" alt="Image" src="https://github.com/user-attachments/assets/417f6404-7515-4c3f-8638-0910d9026608" />

Good Job, me.

<img width="483" height="384" alt="Image" src="https://github.com/user-attachments/assets/1e262895-767e-425a-9fc6-38ba7e58ffa6" />

I click ‘Next’, ‘Install’, and select ‘Windows Server 2019 Standard Evaluation (Desktop Experience)’. I select this version to make sure I have the GUI that the desktop experience provides, versus the command line alternative. I click’ Next’, ‘Next’, and then ‘Custom Install’. I click ‘Next’ again, and wait for the VM to install the OS and reboot.

Once it reboots, I set the U/N to Administrator and set the password to ‘Password1’. *Please note I do not advocate for this basic password in a real world environment, this is for the simplicity of this lab*
After that I sign in.

Once signed in, I click the ‘Device’ tab a the top, and click ‘Insert Guest additions CD Image’.

<img width="555" height="359" alt="Image" src="https://github.com/user-attachments/assets/dd27c8a0-7926-4873-a151-7ef3b6667239" />

I find ‘VBoxWindowsAdditions-amd64’, click it, and then click through all the ‘Next’ buttons, and eventually ‘Install’. Let it install and then reboot the VM. Login after rebooting. 
Now I will assign the IP Address for the Internal Network Adapter. The external NAT will automatically assign itself one, so I just need to focus on the internal. I click the network button on the bottom right corner of the taskbar, open up the network setting box, and click ‘Change Adapter Options’. I click the network associated with the internal NIC (in this case I renamed it to ‘Internal’. I select ‘Properties’, and double click ‘Internet Protocol Version 4 (TCP/IPv4). Check the ‘Use The Following IP addresses’, 

<img width="666" height="546" alt="Image" src="https://github.com/user-attachments/assets/8057a801-3934-4430-94b9-ca748be6af8a" />

I don’t need a Default Gateway in this instance because the DC will be acting as one as it’s between the internal and external NICs. I use the loopback address for the ‘Preferred DNS Server’ 127.0.0.1. Then press ‘OK’.

So far (based on the Visual Representation) I have created the VM, both the internal/external NICS, and given an IP address to the internal network.

Now my next step is to install Active Directory Domain Services and create a domain.
I open up Server Manager, click on ‘Add Roles and Features’, hit ‘Next’ and ‘Next’ again.
I choose the DC server in the ‘Select Destination Server’ tab.

<img width="386" height="434" alt="Image" src="https://github.com/user-attachments/assets/636401ee-9814-41a5-87c1-d1162f5e83ce" />

Click ‘Next’
Then I choose ‘Active Directory Domain Services’, ‘Add Features’, ‘Next”, ‘Next’, then ‘Install’.
After the install, I click on the yellow notification near the flag in the upper right hand corner, and the I proceed to do the Post-Deployment Configuration, and promote the VM to a domain.

<img width="624" height="440" alt="Image" src="https://github.com/user-attachments/assets/f7806604-6d52-4fc8-891f-7196daf95cfe" />

I select the ‘Add a new forest’ check circle, and name the domain ‘mydomain.com’. No reason other keeping this simple. 
I continue to hit ‘Next’ until ‘Install’.
After the Install the VM will reboot.
I login again.
Now I am going to create my own dedicated domain admin account instead of using the built-in administrator account.
I press ‘Start’ on the taskbar, select ‘Windows Administrative Tools’, and then ‘Active Directory Users and Computers’.
I  create a new Organizational Unit by right-clicking mydomain.com, ‘New’, and selecting ‘Organizational Unit’. I name it ‘Admins’ and hit ok. Inside of the ‘Admin’ OU I create a new user (right-clicking, new, and then user), and I name it my name, ‘Christian Rooks’. And set the User Login name as ‘crooks’ @mydomain.com (just my first initial and last name, which is the standard I already use for the Active Directory standard working as an IT Coordinator for my school system). I hit ‘Next’, and set the password to ‘Password1’ (keeping it the same for everything for simplicity). ‘Next’ again, and then ‘Finish’.

<img width="590" height="441" alt="Image" src="https://github.com/user-attachments/assets/caea3fb1-d710-426d-80d3-85719a1affb5" />

I haven’t made it an Admin yet, so I right-click my name, go to ‘Properties’, and click the ‘Member Of’ Tab, and click ‘Add’. I add me to ‘Domain Admins’, and click ‘Apply’, and ‘Ok’.
I then Log out, click ‘Other User’ on the login screen, and then login with my crooks credentials. 

<img width="658" height="350" alt="Image" src="https://github.com/user-attachments/assets/32c0354f-bede-48de-b308-8911bb918589" />

Login successful. 
Heck yes.
Next to install the Remote Access Server (RAS).
To do this, I return to the ‘Server Manager’ and ‘Add Roles and Features’, ‘Next’, ‘Next’, ‘Next’, I select ‘Remote Access’, and then ‘Next’. I check ‘Routing’, and then press ‘Next’, ’Next’, ‘Next’, and then ‘Install’.

<img width="646" height="346" alt="Image" src="https://github.com/user-attachments/assets/f706d752-a6d4-44eb-be13-9f6db919f9bd" />

After the install, close, go to ‘Tools’ in the upper right hand corner, select ‘Routing and Remote Access’, right-click Domain Controller on the left hand column, and ‘Configure and Enable Routing and Remote Access’. ‘Next’, click ‘NAT’, ‘Next’, select ‘Internet’, ‘Next’, and then ‘Finish’.
RAS configuration: COMPLETE.
Next: Setup the DHCP server to automatically assign IP addresses between the client and server. 
I select ‘Add Roles and Features’ in the Server Manager. ‘Next’, ‘Next’, ‘Next’, select ‘DHCP’, ‘Next’, ‘Next’, ‘Next’, ‘Install’, and ‘Close’.
I go back to ‘Tools’ in the upper right hand corners, select ‘DHCP’ to set up the scope.
Referring back the visualization, I know my scope will have: 
IP Range: 172.16.0.100-200 
Subnet Mask: 255.255.255.0
Gateway:172.168.0.1
DNS: 172.16.0.1

I right-click IPv4 and select ‘New Scope’, name it 172.16.0.100-200, ‘Next’, I enter the ‘Start IP Address as ‘172.16.0.100’, the ‘End IP Address’ as ‘172.16.0.200’, I set the length to ‘24’, and set the Subnet Mask to ‘255.255.255.0’. I press ‘Next’, ‘Next’ again because I’m not including exclusions, ‘Next’, ‘Next’. Since the internal NIC is acting as the default gateway for the Domain Controller, I am going to use it’s IP for the default gateway entry in this section, so I enter ‘172.16.0.1’ in the IP address section. Hit ‘Add’, and then ‘Next’. ‘Next’. ‘Next’. ‘Next’, and finally ‘Finish’.

<img width="598" height="409" alt="Image" src="https://github.com/user-attachments/assets/4088944f-eef0-472a-b0b7-9f22ea57f2c2" />

I had to refresh dc.mydomain, but the DHCP server is now up and running.
Good Job.
Now we need Users for Active Directory.
I open internet explorer in the Domain Controller, and insert this link: https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbUQ2RXJVck5mZUpkRExGaHlhQnFxQmZiazA4Z3xBQ3Jtc0ttRHZJMUctMlY3U2JCSTJ2TFVMT0ZmYmJ6Nm5WN2U4V2hSZUMyNWUyTHpaek1laXAweEpGUWNIaDRjYWVuYkJJWkJIRzBaX3NfejFfeC0tcHZDXzgzMHVFMVVUT09CTXNqVTA0T240REFjLWtCSE1DUQ&q=https%3A%2F%2Fgithub.com%2Fjoshmadakor1%2FAD_PS%2Farchive%2Frefs%2Fheads%2Fmaster.zip&v=MHsI8hJmggI

I download the file unto the desktop, extract it. It is a list of names to be uploaded into Active Directory.

<img width="378" height="315" alt="Image" src="https://github.com/user-attachments/assets/40371579-d286-42f1-aa68-1e7931036688" />

I close out, go to ‘Start’, and open ‘Windows PowerShell’.
I find the file with the names, add, press run at the top of powershell.
After the names are uploaded, I open Active Directory, and search my name.

<img width="638" height="476" alt="Image" src="https://github.com/user-attachments/assets/8f6bfb52-543d-496e-a5c3-1837601f75cb" />

Success.
The last thing to do is make the Windows 10 Virtual Machine.
I open Oracle VirtualBox again, and create new at the top, I name it Client1, choose OS Version Windows 10 (64-bit), I give it 4096 MB of ram, and add 4 CPUs.
I change the Network Adapter 1 to Internal,  and power on the Client1 VM.
I find my Windows 10 ISO to boot from, once booted I install.
When prompted ‘Who’s going to use this PC?’ I type in ‘user’, and ‘Password1’.

<img width="568" height="430" alt="Image" src="https://github.com/user-attachments/assets/6fc450b7-7de9-4b04-98b0-3d049c31fae3" />

BUT. GUESS WHAT? 
I cannot connect to the internet. I opened the Command Prompt, and ran ipconfig, and realized I have 169.x.x.x IP address (APIPA), long story short Client1 can’t reach the DHCP server (usually the router) to get a proper IP address.
Troubleshooting Side Quest
The core issue stemmed from Client1 receiving an APIPA address (169.254.x.x), which indicated a failure to communicate with the Domain Controller (DC) acting as the DHCP server. My troubleshooting process successfully corrected two primary configuration errors to establish communication on the isolated lab network.

1. Correcting the Subnet Mismatch (The DHCP Scope Error)
My first critical error was a typo in the DHCP Scope configuration on the Domain Controller. The intended network was 172.16.0.1, but the DHCP scope was incorrectly defined using 172.160.0.1, creating a fundamental subnet mismatch. This meant the DHCP server was listening for requests on one subnet while the DC's static IP (the expected Default Gateway) was on another, preventing the DC from responding to Client1's DHCP requests. The fix involved deleting the incorrect DHCP scope and creating a new scope with the correct 172.16.0.1 static IP and the 255.255.255.0 subnet mask.

2. Validating Inter-VM Communication (Internal Network Configuration)
I ensured the DC and Client1 were correctly configured at the VirtualBox level using the Internal Network setting, which provides a private, isolated communication path necessary for a lab environment. Following the DHCP scope correction, I verified that the key DHCP options were correctly pointing to the DC's static IP. Finally, forcing Client1 to renew its IP address using the ipconfig /release and ipconfig /renew commands allowed it to successfully acquire a valid IP address from the now-correctly configured DHCP server, resolving the connection issue.
Success! +150% EXP

<img width="700" height="384" alt="Image" src="https://github.com/user-attachments/assets/02de6318-fd5b-4a8f-a18c-33de9cb87f43" />

<img width="624" height="505" alt="Image" src="https://github.com/user-attachments/assets/8f6cf166-410a-4f4c-aaf8-a5132855d056" />

I ping google.com in the Command Prompt and have success.
This is great. This means the network infrastructure is working!
I rename the PC, and add it to the domain of mydomain.com, and it asks for my admin credentials. I use crooks and Password1. Success. Looks like the Active Directory settings are working. I restart Client1 when prompted.

<img width="624" height="322" alt="Image" src="https://github.com/user-attachments/assets/2e328192-ad52-4dd6-bf65-529e0c258194" />

I check the DHCP manager on the Domain Controller, and checking under address leases I can see Client1 properly leasing an IP address from the scope.

I sign out on Client1 and try to sign in using one of the other users I added earlier with Password1. I sign in successfully.
At this point my structures, and user logins indicate I setup everything correctly. So I will conclude this lab!

<img width="634" height="545" alt="Image" src="https://github.com/user-attachments/assets/96f42bdc-729c-46c8-ba9d-5be6d1c41eda" />


This project, originally designed by Josh Madakor, serves as a comprehensive lab for developing Active Directory skills tailored for corporate environments. The process also honed my diagnostic and troubleshooting capabilities through the resolution of real-world implementation hurdles.


##  **Credits & Attributions**
This lab was inspired by and follows the architectural framework designed by **Josh Madakor**. 

* **Logic & Workflow:** Based on the "How to Setup a Basic Home Lab Running Active Directory (Oracle VirtualBox) | Add Users w/PowerShell" project. 

While the foundational steps follow the guide above, all documentation, network troubleshooting (specifically the DHCP scope resolution), and environment configuration were performed independently by me.











