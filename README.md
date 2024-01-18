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

**5. Create a DNS A-Record on DC-1 for mainframe and set it to DC-1s private IP address**
  - From DC-1 --> Start --> Server Manager --> Tools --> DNS
  - Expand DC-1 --> Forward Lookup Zone --> Your domain (mydomain.com) --> Right click --> New Host (A or AAAA)...
     - Name: mainframe
     - IP address: DC-1's private IP address --> Add Host

    <img src="https://i.imgur.com/8m8RwMj.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

**6. Need to do step 6**

<h2>Local DNS Cache Exercise</h2>

**7. Go to DC-1 and change mainframe's record address to 8.8.8.8**
  - mainframe --> Change IP address to 8.8.8.8 --> Apply --> OK

  <img src="https://i.imgur.com/KSBJcpA.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

**8. Go to Client-1 and ping mainframe. See that it still pings the old IP address**
  - In Client-1 --> Start --> Type and open cmd --> type ping mainframe

**9. Check the local dns cache (ipconfig /displaydns)**
  - Go to cmd --> Enter ipconfig /displaydns 

**10. Flush the DNS cache (ipconfig /flushdns). See that the cache is empty**
  - Go to cmd --> Run as administrator --> Enter ipconfig /flushdns

 <img src="https://i.imgur.com/01LzcTP.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

**11. Ping mainframe again. See the new address of the record**
  - In cmd --> Enter ping mainframe

<img src="https://i.imgur.com/S7Ipkyr.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<h2>CNAME Record</h2>

**12. Go to DC-1 and create a CNAME record that points the host "search" to www.google.com**
  - In DNS Manager --> Right click --> New Alias (CNAME)...
  - Alias name: search
  - FQDN for target host: www.google.com
  - OK

**13. Go to Client-1 and ping "search", see the results of the CNAME record**
  - In cmd --> Enter ping search

**14. On Client-1 nslookup "search", see the results of the CNAME record**
  - In cma --> Enter nslookup search

**what is a root hint? What is DNS, what is a DNS a-record
       
       
