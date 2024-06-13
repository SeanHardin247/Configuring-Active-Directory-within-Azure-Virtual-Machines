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

- Open Active Directory Users and Computers and right click on your domain name. Hover over new and press organizational unit. Name it _EMPLOYEES. Repeat this except name this one _ADMINS
<h2>Deployment and Configuration Steps</h2>

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
