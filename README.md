<h1>Active Directory Home Lab</h1>

<h2>Description</h2>
This project documents the deployment and configuration of a Windows Server Active Directory environment using VMware Workstation Pro.

The goal of this home lab was to simulate a small enterprise IT environment and gain hands-on experience with Windows Server administration, Active Directory Domain Services (AD DS), DNS, user and group management, Group Policy, and Windows client administration.

This project was built as part of my IT/cybersecurity home lab to develop practical skills that are commonly used in Help Desk, System Administration, and Cybersecurity roles.
<br />


<h2>🎯 Objectives</h2>

- <b>Install Windows Server in VMware Workstation Pro</b>
- <b>Configure a virtualized Windows Server environment</b>
- <b>Configure a static IP address</b>
- <b>Install Active Directory Domain Services (AD DS)t</b>
- <b>Promote Windows Server to a Domain Controller</b>
- <b>Configure DNS</b>
- <b>Create an Active Directory domain</b>
- <b>Create organizational units (OUs)t</b>
- <b>Create users and security groups</b>
- <b>Join a Windows client computer to the domain</b>
- <b>Configure Group Policy</b>
- <b>Implement basic security policiest</b>
- <b>Practice common Active Directory administration tasks</b>
- <b>Document the entire deployment process</b>

<h2>🛠️ Technologies & Tools </h2>

- <b>VMware Workstation Pro: Virtualization platform<b>
- <b>Windows Server:	Domain Controller / Server<b>
- <b>Windows 10/11:	Domain client<b>
- <b>Active Directory Domain Services:	Identity and domain management<b>
- <b>DNS:	Name resolution<b>
- <b>Group Policy:	Centralized configuration and security<b>
- <b>PowerShell:	Windows administration<b>

<h2>🖥️ Lab Environment</h2>

              HOME NETWORK
                   │
                   |
            VMware Workstation
                   |
                   |
          ┌────────┴────────┐
          │                 │
        Admin             User01
          │                 │
          └────────┬────────┘
                   │
             Active Directory
                   │
            Tomashomelab.local
        

            
<h2>Program walk-through:</h2>

<p align="center">
 <br/>

---

# 1. Install VMware Workstation Pro

1. Download VMware Workstation Pro.
2. Create or sign in to a Broadcom account if required.
3. Download the appropriate VMware Workstation Pro installer<img width="1679" height="864" alt="Broadcom Vmare Screenshot" src="https://github.com/user-attachments/assets/6d8d5262-6cf0-45b3-abf1-b4713d696f8a" />
.
4. Run the installer.
5. Follow the installation wizard.
6. Complete the installation.
7. Restart the computer if prompted.

---

# 2. Download Windows Server ISO 

1. Go to Microsoft's Windows Server evaluation page.
2. Register for the evaluation if required.
3. Download the Windows Server 2022 ISO.
4. Save the ISO somewhere easy to locate.<img width="432" height="453" alt="Microsoft vmare " src="https://github.com/user-attachments/assets/4a4f173b-ba2f-4665-9ef5-683dc5ce9a96" />


The video uses Windows Server 2022 as the server operating system.

# Troubleshooting:
 
During the initial setup of the home lab, I encountered an issue with the Windows Server installation. I had accidentally installed the Microsoft Windows Server ISO directly onto my physical computer instead of installing it inside the VMware virtual machine.

Because of this, I was unable to continue with the planned virtualized Active Directory lab environment.

To resolve the issue, I had to take a detour and reconfigure my physical computer. I created a bootable USB drive containing the Windows installation media and used it to access the Windows recovery and installation environment.

I then wiped the existing installation from the computer and performed a clean Windows installation. After restoring the computer to a working state, I reinstalled and configured the necessary virtualization software so I could restart the lab using the correct virtual machine setup.

For the remainder of the project, Windows Server was installed inside VMware rather than directly onto the physical computer.


---

# 3. Create the Windows Server Virtual Machine

1. Open VMware Workstation Pro.
2. Select **Create a New Virtual Machine**.<img width="1529" height="849" alt="Vmware New virtual machine" src="https://github.com/user-attachments/assets/a7321219-7f9d-4940-b149-65c4f9eab698" />

3. Select **Typical** configuration.
4. Choose:

   **I will install the operating system later**

5. Select **Microsoft Windows** as the guest operating system.
6. Select the appropriate Windows Server version.
7. Give the VM a name.
<img width="676" height="595" alt="VM machine created" src="https://github.com/user-attachments/assets/8742ac03-2b99-4ae8-909c-c6fed0fe7255" />

Example:

`Windows Server 2022 - Domain Controller`

8. Select the location where the VM will be stored.
9. Configure the virtual disk.
10. Finish creating the VM.

---

# 4. Mount the Windows Server ISO

1. Select the new virtual machine.
2. Open **Virtual Machine Settings**.
3. Select **CD/DVD**.
4. Select **Use ISO image file**.
5. Browse to the Windows Server ISO.
6. Select the ISO.
7. Save the VM settings.<img width="1104" height="952" alt="CD-DVD ISO Location" src="https://github.com/user-attachments/assets/09b845fe-e9b3-4e14-9cdf-ec6315046336" />


---

# 5. Install Windows Server

1. Start the virtual machine.
2. Boot from the Windows Server ISO.
3. Select the appropriate language settings.
4. Select **Next**.<img width="1324" height="954" alt="microsoft ISO installation on vmware" src="https://github.com/user-attachments/assets/f54a2686-f26c-4407-86b6-35418cc3f6d1" />

5. Click **Install Now**.
6. Select:

   **Windows Server Standard Evaluation (Desktop Experience)**

7. Accept the license agreement.
8. Select **Custom Installation**.
9. Select the virtual disk.
10. Allow Windows to install.

11. Wait for the VM to restart.

---

# 6. Configure the Administrator Account

After installation:

1. Create a password for the local Administrator account.
2. Log into Windows Server.
3. Wait for Server Manager to load.<img width="1314" height="980" alt="microsoft ISO admin setup" src="https://github.com/user-attachments/assets/6cbf72b5-8e11-421e-a643-150f08573379" />

---

# 7. Verify the Windows Server Version

Open the Run dialog:

`Windows Key + R`

Enter:

`winver`

Verify that Windows Server is installed correctly.

---

# 8. Install Active Directory Domain Services

1. Open **Server Manager**.
2. Select **Manage**.
3. Select **Add Roles and Features**.
4. Continue through the installation wizard.
5. Select:

   **Role-based or feature-based installation**

6. Select the local server.
7. Select:

   **Active Directory Domain Services**

8. When prompted, select **Add Features**.
9. Continue through the wizard.
10. Make sure the required management tools are selected.
11. Select **Install**.
12. Wait for the installation to complete.<img width="1060" height="820" alt="Configure a Domain Controller" src="https://github.com/user-attachments/assets/7ee37844-d6f5-4ee7-8867-e8b553e58b22" />


---

# 9. Promote the Server to a Domain Controller

After AD DS is installed:

1. Open Server Manager.
2. Select the notification flag.
3. Select:

   **Promote this server to a domain controller**

4. Select:

   **Add a new forest**

5. Enter a domain name.

Example:

`example.local`

6. Configure the Domain Controller options.
7. Set the Directory Services Restore Mode (DSRM) password.
8. Continue through the wizard.
9. Review the prerequisites.
10. Select **Install**..<img width="1060" height="820" alt="Configure a Domain Controller" src="https://github.com/user-attachments/assets/36f412db-e996-4375-a545-3a33db682a0d" />

The server will restart after the domain controller installation is completed

---

# 10. Log Into the Domain

After the restart:

1. Log into Windows Server.
2. Use the domain administrator account.
3. Verify that the server is now operating as a Domain Controller.<img width="1254" height="899" alt="2 Log in to admin" src="https://github.com/user-attachments/assets/344949b8-f4e9-48db-bc5e-4223377735e1" />


Example domain:

`EXAMPLE\Administrator`

---

# 11. Open Active Directory Users and Computers

Open:

**Server Manager → Tools → Active Directory Users and Computers**<img width="1249" height="910" alt="Active Directory Users and Computers Window" src="https://github.com/user-attachments/assets/afd335d7-79c7-4fab-bc87-3ee583db26b6" />


ADUC is used to manage:

- Users
- Groups
- Computers
- Organizational Units
- Other Active Directory objects

---

# 12. Create an Organizational Unit

Organizational Units (OUs) can be used to organize Active Directory objects.

1. Open **Active Directory Users and Computers**.
2. Right-click the domain.
3. Select:

   **New → Organizational Unit**

4. Enter the OU name.

Example:

`USA`

5. Click **OK**.<img width="1279" height="900" alt="Active Directory Creating OU " src="https://github.com/user-attachments/assets/ceb571c3-6043-4761-ab1d-51fb1e97c809" />


Additional OUs can be created for departments, users, computers, or geographic locations.

Example structure:

```text
example.local
│
├── USA
│   ├── Users
│   ├── Computers
│   ├── IT
│   └── HR
│
├── Europe
│
└── Asia
```

OUs can also be nested inside other OUs.

---

# 13. Create Active Directory Groups

1. Open the appropriate OU.
2. Right-click inside the OU.
3. Select:

   **New → Group**

4. Enter the group name.

Example:

`IT-Admins`

5. Select the appropriate group scope.
6. Select the group type.
7. Click **OK**.<img width="1261" height="913" alt="Active directory Creating Groups" src="https://github.com/user-attachments/assets/cad1bf5a-06a2-46cb-9baf-946b3595cc74" />


---

# 14. Understand Group Scope

Active Directory provides three main group scopes:

### Global

Typically used to group users from the same domain based on their role or department.

Example:

`IT-Users`

### Domain Local

Typically used when assigning permissions to resources within the domain.

Example:

`File-Server-Access`

### Universal

Can be used across multiple domains in an Active Directory forest.

---

# 15. Understand Group Types

There are two primary group types:

### Security Group

Used to assign permissions and access to resources.

Examples:

- File shares
- Folders
- Applications
- Printers

### Distribution Group

Primarily used for email distribution.

Distribution groups do not provide resource permissions like security groups.

---

# 16. Create an Active Directory User

1. Open the appropriate OU.
2. Right-click inside the OU.
3. Select:

   **New → User**

4. Enter the user's first name.
5. Enter the last name.
6. Create the user's logon name.
7. Click **Next**.
8. Create a temporary password.
9. Configure the appropriate password options.
10. Click **Next**.
11. Review the account information.
12. Select **Finish**.<img width="1261" height="904" alt="Active directory New Users" src="https://github.com/user-attachments/assets/07a869ce-11c4-4f2f-8afe-70df0e4dd9b9" />


Example:

```text
First Name: John
Last Name: Smith
Username: jsmith
```

---

# 17. Add the User to a Group

1. Locate the newly created user.
2. Right-click the account.
3. Select **Properties**.
4. Open the **Member Of** tab.
5. Select **Add**.
6. Enter the appropriate security group.
7. Confirm the group.
8. Apply the changes.

Example:

```text
John Smith
    ↓
IT-Users
    ↓
IT-Admins
```

---

# 18. Basic Active Directory Practice

After completing the initial setup, practice common administrative tasks.

### User Management

- Create users
- Disable users
- Enable users
- Reset passwords
- Unlock accounts
- Add users to groups
- Remove users from groups

### Group Management

- Create security groups
- Create distribution groups
- Modify group membership
- Configure group scope
- Assign permissions

### OU Management

- Create OUs
- Move users between OUs
- Move computers between OUs
- Create nested OUs

---

# 19. Home Lab Structure

A basic lab can be organized like this:

```text
Active Directory Domain
│
├── USA
│   │
│   ├── Users
│   │   ├── IT
│   │   ├── HR
│   │   └── Finance
│   │
│   ├── Computers
│   │
│   └── Groups
│
└── Domain Controllers
```

---

# 20. Skills Demonstrated

This project demonstrates practical experience with:

- VMware virtualization
- Windows Server administration
- Active Directory Domain Services
- Domain Controller deployment
- Active Directory Users and Computers
- Organizational Units
- User account management
- Security groups
- Distribution groups
- Group scopes
- Domain authentication
- Basic Windows Server administration

---

# Project Outcome

The completed lab provides a controlled environment for practicing Active Directory administration and common IT support tasks.

Future additions to the lab can include:

- Group Policy Objects (GPOs)
- Windows client domain joining
- DNS configuration
- DHCP
- File sharing
- Security policies
- Service accounts
- Password policies
- User lockout policies
- Help desk troubleshooting scenarios

Next I will [Creating And Setting Up GPO](https://github.com/vtomas410/Creating-And-Setting-Up-GPO)

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
