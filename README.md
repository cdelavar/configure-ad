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
- PowerShell ISE

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Ensure Connectivity Between the Client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account
- Join Client to Domain
- Setup Remote Desktop for Non-administrative Users on Client
- Create Additional Users

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://imgur.com/peoG1BR.png" height="80%" width="80%" alt="Create DC-1"/>
</p>
<p>
Create resources in Azure - setup 2 virtual machines, the first one as the domain controller, DC-1, running Windows Server 2022. Navigate to portal.azure.com and go to Virtual Machines - Create Azure virtual machine. For this machine, I chose a Standard_E2as_v4 VM size of 2 vcpus with 16 GiB of memory. Click Review + create. A virtual network and subnet will be automatically created.
</p>
<br />

<p>
<img src="https://imgur.com/b3xtiNr.png" height="80%" width="80%" alt="Create Client-1"/>
</p>
<p>
Next, create the client virtual machine, and name it Client-1. Use the same Resource Group as the domain controller because we want the client to be in the same virtual network, in this case it's AD-Lab. Make sure the client machine Region is set to the same region as the DC-1 machine. In this case, it's (US) East US 2.
</p>
<br />

<p>
<img src="https://imgur.com/Nh0F5Ji.png" height="80%" width="80%" alt="DC NIC to Static 1"/>
</p>
<p>
Set the domain controller's NIC Private IP address to be static. Navigate to Virtual machines, click on DC-1. In the Settings panel on the left, 
click Networking. Click on the Network Interface name, in this case it's dc-175.
</p>
<br />

<p>
<img src="https://imgur.com/uHzoPhY.png" height="80%" width="80%" alt="DC NIC to Static 2"/>
</p>
<p>
Click on IP configurations, then click on ipconfig1, under Assignment.
</p>
<br />

<p>
<img src="https://imgur.com/uHzoPhY.png" height="80%" width="80%" alt="DC NIC to Static 3"/>
</p>
<p>
Click on Static and then Save.
</p>
<br />

<p>
<img src="https://imgur.com/SbvTkAN.png" height="80%" width="80%" alt="Ping DC-1"/>
</p>
<p>
Login to Client-1 and ping DC-1's private IP address. Windows firewall is blocking icmp traffic so the request will time out.
</p>
<br />

<p>
<img src="https://imgur.com/TMF00VE.png" height="80%" width="80%" alt="Windows Firewall"/>
</p>
<p>
Login to DC-1 and type wf.msc in the start menu to open the Windows Firewall Console. Click inbound rules and enable 2 ICMP echo request rules. 
</p>
<br />

<p>
<img src="https://imgur.com/UXG1rj7.png" height="80%" width="80%" alt="Successful Ping DC-1"/>
</p>
<p>
Now there can be connectivity between the client and domain controller.
</p>
<br />

<p>
<img src="https://imgur.com/bl05K69.png" height="80%" width="80%" alt="Server Manager"/>
</p>
<p>
Install Active Directory. USe Server Manager to install AD. In the Windows Server Manager, go to Add roles and features.
</p>
<br />

<p>
<img src="https://imgur.com/81mnn1y.png" height="80%" width="80%" alt="Add Roles and Features"/>
</p>
<p>
click Next and choose Role-based or feature-based installation.  
</p>
<br />

<p>
<img src="https://imgur.com/7Erzv2s.png" height="80%" width="80%" alt="Select Server"/>
</p>
<p>
Select a server from the server pool.
</p>
<br />

<p>
<img src="https://imgur.com/EVRtqcD.png" height="80%" width="80%" alt="Domain Services"/>
</p>
<p>
Check the box for Active Directory Domain Services, then click Next through the rest of the dependencies and confirm installation.
</p>
<br />

<p>
<img src="https://imgur.com/FwCZw9R.png" height="80%" width="80%" alt="Finish Install"/>
</p>
<p>
Finish installing Active Directory and turn the server into a domain controller. Click on the notifications flag in the top right corner, and click on Promote this server to a domain controller. In the Deployment Configuration window, click on Add a new forest and enter a Root domain name. Leave the default checked boxes as is, and enter a password for the Directory Services Restore Mode then click Next through to installation. You can specify the location of the AD DS database, log files, and SYSVOL, in this case, the default is fine, click Next. The server will reboot automatically after installation is complete.
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

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
