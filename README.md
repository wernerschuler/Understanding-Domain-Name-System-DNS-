# Understanding-Domain-Name-System-DNS-
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Requirements</h2>

- Completed the Active Directory setup and have the following:
  - Active Directory running on a virtual machine in Azure
  - A client virtual machine running in Azure and joined to the domain

<h2>A-Record Task</h2>

**1. Login to DC-1 using your domain admin account**
   - portal.azure.com --> Virtual machines --> DC-1 --> Copy DC-1's public IP address
   - Start --> Type 'Remote Desktop Connection --> Paste DC-1's public IP address
   - Enter the username and password for your domain admin account

**2. Login to Client-1 using your domain admin account**
  - portal.azure.com --> Virtual machines --> Client-1 --> Copy Client-1's public IP address
  - Start --> Type 'Remote Desktop Connection --> Paste Client-1's public IP address
  - Enter the username and password for your domain admin account (image below)

    <img src="https://i.imgur.com/ibkSBp7.png" height="40%" width="60%" alt="Disk Sanitization Steps"/>

**3. From Client-1 ping "mainframe" see how the ping failed**
  - From Client-1 --> Start --> Enter 'cmd' --> Enter 'ping mainframe'

    <img src="https://i.imgur.com/0Criu4G.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

**4. Use command nslookup to check for mainframe's record**
  - From Client-1 --> Start --> Enter 'cmd --> Enter 'nslookup mainframe'
  - Notice that this command has failed because there is no record of mainframe

    <img src="https://i.imgur.com/CsMzUsR.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
