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







