<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configuring Active Directory in a virtual machine (Azure)</h1>
This tutorial outlines the implementation of Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 pro (21H2)

<h2>Prerequsites</h2>

 - create a windows server 2022 VM which will act as the domain controller, change the private ip address to static.

 - create the windows 10 VM that we will refer to as "Client-1", make sure it is in the same V-net as the domain controller

 
<h2>High-Level Deployment and Configuration Steps</h2>

- Log into the domain controller usisng remote desktop, and navigate to the windows defender firewall with advanced security. Go to the inbound rules section and filter by protocol, in the ICMPv4 area enable both Core Networking Diagnostics options.
  
- Open another remote desktop controller instance, and log into Client-1. Open command prompt and type: "ping (Domain controllers private ip adddress)" if it comes back with reply and not saying request timed out, you completed the previous step successfully.
  
- In domain controller, there should be a server manager app that opened long ago, click on roles and features and hit next until you get to server roles. Select Acive Directory Domain services and hit next and install when given the option.
  
- Click the flag in the top right which will have a warning sign, click promote this server to a domain controller and add a new forest option. Name the root domain anything, in my case im settling on ILoveThisDomain.com then hit next and input the domain controller VMs password you gave it in azure, keep clicking next and hit install after the prerequisite check
  
- You will be kicked from the remote desktop session because the computer needs to restart, log back into it with the user name ILoveThisDomain.com\(the user name you made the vm with). if you chose a different domain name use that instead, the password will be the same.

<h2>Deployment and Configuration Steps</h2>
Now we have active directory installed and are going to practice a few things like adding people and computers to the domain

- Open Active Directory Users and Computers and right click on your domain name. Hover over new and press organizational unit. Name it _EMPLOYEES. Repeat this except name this one _ADMINS. Right click the admins folder and hover over new and add a InerOrgPerson.

- Name this person "Jane Doe" and in the User logon name input "jane_Admin" make the password "Password1" and uncheck the box that says "User must change password at next logon" Right click on jane doe after adding and select properties, Member of, add, type Domain Admins, hit ok, and click apply and ok, then you can sign out of the remote desktop session and relog as ILoveThisDomain\jane_Admin

we will finally use Client-1 again, we are going to add it to our domain for non admin users
  
- Go back to azure an copy the Domain Controllers private ip address. Then go to client-1 in azure, click networking, networking settings, click the blue text which should have text above it reading "Network interface / IP configuration" and on the left select DNS servers, change it to custom and in the add DNS server box input domain controllers private ip address and hit save. This has a tendency to not save for some reason if you pasted it using Control+V, try inputting the numbers manually. After this restart the client-1 VM.

- In client-1 on remote desktop, right click the windows icon in the bottom left go to system and put it in full screen then on the right hit "Rename this pc (advanced)" in the application that opened click change, change it to a member of domain, then input ILoveThisDomain.com or your own domain name

  
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
