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
