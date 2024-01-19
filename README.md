# Understanding-Domain-Name-System-DNS-
<p align="center">
<img src="https://i.imgur.com/VN2T0zi.jpg" alt="Domain name system logo"/>
</p>



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Command Prompt
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Requirements</h2>

- Completed the Active Directory setup and have the following:
  - Active Directory running on a virtual machine in Azure
  - A client virtual machine running in Azure and joined to the domain

 Definition
 -- 
 - Domain name system (DNS) - A system that translate human readable domain names such as www.google.com into it's corresponding IP address such as 172.217.6.14
 - Root hints - Information that guide your computer or device to find important servers on the internet. Root hints provide your computer with information about important servers that is used as a starting point to find other servers.
    - So when your computer needs to find a specific website, it uses the root hints to find the nearest root server. Then it will ask that server for information about the next server responsible for the website you want to visit. This process continues until you reach the server responsible for the website you are looking for.

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

<h2>Local DNS Cache Exercise</h2>

**6. Go to DC-1 and change mainframe's record address to 8.8.8.8**
  - mainframe --> Change IP address to 8.8.8.8 --> Apply --> OK

  <img src="https://i.imgur.com/KSBJcpA.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

**7. Go to Client-1 and ping mainframe. See that it still pings the old IP address**
  - In Client-1 --> Start --> Type and open cmd --> type ping mainframe

**8. Check the local dns cache (ipconfig /displaydns)**
  - Go to Command Prompt --> Enter ipconfig /displaydns 

**9. Flush the DNS cache (ipconfig /flushdns). See that the cache is empty**
  - Go to Command Prompt --> Run as administrator --> Enter ipconfig /flushdns

 <img src="https://i.imgur.com/01LzcTP.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

**10. Ping mainframe again. See the new address of the record**
  - In Command Prompt --> Enter ping mainframe

<img src="https://i.imgur.com/S7Ipkyr.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<h2>CNAME Record</h2>

**11. Go to DC-1 and create a CNAME record that points the host "search" to www.google.com**
  - Start --> Server Manager --> Tools --> DNS
  - DC-1 --> Forward Lookup Zones --> mydomain.com
  - Right click --> New Alias (CNAME)...
  - Alias name: search
  - FQDN for target host: www.google.com
  - OK

<img src="https://i.imgur.com/NJKlzqB.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

**12. Go to Client-1 and ping "search", see the results of the CNAME record**
  - In Command Prompt --> Enter ping search

<img src="https://i.imgur.com/eu29TSG.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

**13. On Client-1 nslookup "search", see the results of the CNAME record**
  - In Command Prompt --> Enter nslookup search

<img src="https://i.imgur.com/BC7PA95.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

       
       
