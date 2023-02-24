<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://youtu.be/_T6uqRwcoAw)

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
<b>Create resources in Azure - setup two virtual machines, the first one as the domain controller, DC-1, running Windows Server 2022. Navigate to portal.azure.com and go to Virtual Machines - Create Azure virtual machine. For this machine, I chose a Standard_E2as_v4 VM size of 2 vcpus with 16 GiB of memory. Click Review + create. A virtual network and subnet will be automatically created.</b>
</p>
<br />

<p>
<img src="https://imgur.com/b3xtiNr.png" height="80%" width="80%" alt="Create Client-1"/>
</p>
<p>
<b>Next, create the client virtual machine, and name it Client-1. Use the same Resource Group as the domain controller because we want the client to be in the same virtual network, in this case it's AD-Lab. Make sure the client machine Region is set to the same region as the DC-1 machine. In this case, it's (US) East US 2.</b>
</p>
<br />

<p>
<img src="https://imgur.com/Nh0F5Ji.png" height="80%" width="80%" alt="DC NIC to Static 1"/>
</p>
<p>
<b>Set the domain controller's NIC Private IP address to be static. Navigate to Virtual machines, click on DC-1. In the Settings panel on the left, 
click Networking. Click on the Network Interface name, in this case it's dc-175.</b>
</p>
<br />

<p>
<img src="https://imgur.com/uHzoPhY.png" height="80%" width="80%" alt="DC NIC to Static 2"/>
</p>
<p>
<b>Click on IP configurations, then click on ipconfig1.</b>
</p>
<br />

<p>
<img src="https://imgur.com/RaDQv9V.png" height="80%" width="80%" alt="DC NIC to Static 3"/>
</p>
<p>
<b>Under Assignment, click on Static and then Save.</b>
</p>
<br />

<p>
<img src="https://imgur.com/SbvTkAN.png" height="80%" width="80%" alt="Ping DC-1"/>
</p>
<p>
<b>Login to Client-1 and ping DC-1's private IP address. Windows firewall is blocking ICMP traffic so the request will time out.</b>
</p>
<br />

<p>
<img src="https://imgur.com/TMF00VE.png" height="80%" width="80%" alt="Windows Firewall"/>
</p>
<p>
<b>Login to DC-1 and type wf.msc in the start menu to open the Windows Firewall Console. Click inbound rules and enable 2 ICMP echo request rules. </b>
</p>
<br />

<p>
<img src="https://imgur.com/UXG1rj7.png" height="80%" width="80%" alt="Successful Ping DC-1"/>
</p>
<p>
<b>Now there can be connectivity between the client and domain controller.</b>
</p>
<br />

<p>
<img src="https://imgur.com/bl05K69.png" height="80%" width="80%" alt="Server Manager"/>
</p>
<p>
<b>Install Active Directory. Use Server Manager to install AD. In the Windows Server Manager, go to Add roles and features.</b>
</p>
<br />

<p>
<img src="https://imgur.com/81mnn1y.png" height="80%" width="80%" alt="Add Roles and Features"/>
</p>
<p>
<b>Click Next and choose Role-based or feature-based installation.</b>
</p>
<br />

<p>
<img src="https://imgur.com/7Erzv2s.png" height="80%" width="80%" alt="Select Server"/>
</p>
<p>
<b>Select a server from the server pool.</b>
</p>
<br />

<p>
<img src="https://imgur.com/EVRtqcD.png" height="80%" width="80%" alt="Domain Services"/>
</p>
<p>
<b>Check the box for Active Directory Domain Services, then click Next through the rest of the dependencies and confirm installation.</b>
</p>
<br />

<p>
<img src="https://imgur.com/FwCZw9R.png" height="80%" width="80%" alt="Finish Install"/>
</p>
<p>
<b>Finish installing Active Directory and turn the server into a domain controller. Click on the notifications flag in the top right corner, and click on Promote this server to a domain controller.</b> 
</p>
<br />

<p>
<img src="https://imgur.com/whMoL5j.png" height="80%" width="80%" alt="Create Forest"/>
</p>
<p>
<b>In the Deployment Configuration window, click on Add a new forest and enter a Root domain name. Leave the default checked boxes as is, and enter a password for the Directory Services Restore Mode then click Next through to installation.</b>
</p>
<br />

<p>
<img src="https://imgur.com/1pG4cpY.png" height="80%" width="80%" alt="AD DS Options"/>
</p>
<p>
<b>You can specify the location of the AD DS database, log files, and SYSVOL, in this case, the default is fine, click Next. The server will reboot automatically after installation is complete.</b>
</p>
<br />

<p>
<img src="https://imgur.com/dCbw4va.png" height="80%" width="80%" alt="AD Users and Computers"/>
</p>
<p>
<b>After restart, logon to the DC-1 from the newly created domain using the FQDN (Fully qualified domain name). Now that the domain is setup, we can create 
organizational units in Active Directory and create an administrative user.</b>
</p>
<br />

<p>
<img src="https://imgur.com/q41Jdlk.png" height="80%" width="80%" alt="New Organizational Unit"/>
</p>
<p>
<b>Click on tools in the top right corner and go to Active Directory Users and Computers. Right click on the domain name in the left side panel and go to 
New - Organizational Unit.</b> 
</p>
<br />

<p>
<img src="https://imgur.com/IvXs2L0.png" height="80%" width="80%" alt="Employees and Admins"/>
</p>
<p>
<b>Let's add an OU for EMPLOYEES and ADMINS.</b>
</p>
<br />

<p>
<img src="https://imgur.com/Q3WytW3.png" height="80%" width="80%" alt="Create Admin User"/>
</p>
<p>
<b>To create an admin user, right click on ADMINS, click New then User. In this case, Username: Ermingard_admin. Fill out the user details and password options.</b> 
</p>
<br />

<p>
<img src="https://imgur.com/Bi5dx9L.png" height="80%" width="80%" alt="Domain Admins Group"/>
</p>
<p>
<b>Now we need to assign the admin user to the domain admins group. Right click on the user name and go to Properties, click on the Member Of tab, click Add. In the Select Groups box type Domain Admins in the "Enter the object names to select" box, then click ok.</b> 
</p>
<br />

<p>
<img src="https://imgur.com/LcPSiLc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<b>Logoff of DC-1 and login again with the newly created admin account. The next step is to join Client-1 to the domain. In order to join the domain, Client-1 needs to use the domain controller as its DNS server. From the Azure portal, set Client-1's DNS settings to DC-1's Private IP address. Set Client-1's Virtual NIC to DC-1's private IP address by going to the Azure Portal - Virtual Machines, and click on Client-1. Click on Networking, then click on the Network Interface.</b> 
</p>
<br />

<p>
<img src="https://imgur.com/fsQptHs.png" height="80%" width="80%" alt="Change DNS Settings"/>
</p>
<p>
<b>Click on DNS Servers and click on the Custom bubble. In the DNS Server box, type in the private IP address of DC-1 and click Save.</b> 
</p>
<br />

<p>
<img src="https://imgur.com/e13gOuJ.png" height="80%" width="80%" alt="Restart Client-1"/>
</p>
<p>
<b>Restart Client-1 from the Azure portal.</b> 
</p>
<br />

<p>
<img src="https://imgur.com/4aXYf1n.png" height="80%" width="80%" alt="Rename PC Advanced"/>
</p>
<p>
<b>Now we need to join Client-1 to the domain. Login to Client-1 again, and go to System settings and click on Rename this PC (advanced).</b> 
</p>
<br />

<p>
<img src="https://imgur.com/28trYJE.png" height="80%" width="80%" alt="Add Domain"/>
</p>
<p>
<b>Click on Change, and in the "Member Of" section, click the Domain bubble and enter the name of the domain.</b> 
</p>
<br />

<p>
<img src="https://imgur.com/6HO4KzL.png" height="80%" width="80%" alt="Admin Credentials"/>
</p>
<p>
<b>Enter the credentials for the admin account that was created earlier. In this case, it's chrisdomain.com\Ermingard_admin. Now the admin can login to Client-1 through the domain.</b>
</p>
<br />

<p>
<img src="https://imgur.com/puY3fkS.png" height="80%" width="80%" alt="Domain Users Setup"/>
</p>
<p>
<b>Next, we'll set up all users to be able to remote in through Client-1. Go to System Settings - Remote Desktop, and click on Select users that can remotely access this PC. On the Remote Desktop Users popup, click Add. In the Select Users or Groups poput, type in Domain Users and click ok.</b> 
</p>
<br />

<p>
<img src="https://imgur.com/hVu8v0p.png" height="80%" width="80%" alt="Powershell ISE Script"/>
</p>
<p>
<b>Let's create a bunch of additional users and attempt to login to Client-1 with one of the users. Log into DC-1. To create the users, we're going to run a script in 
Powershell ISE. Right click Powershell ISE and run as administrator.</b> 
</p>
<br />

<p>
<img src="https://imgur.com/qwaWYkr.png" height="80%" width="80%" alt="Users Created"/>
</p>
<p>
<b>This script will create 1,000 new users in the EMPLOYEES organizational unit folder. The names are randomly generated by alternating vowels and consonants randomly, one after the other.</b>
</p>
<br />

<p>
<img src="https://imgur.com/rL19S8k.png" height="80%" width="80%" alt="New User Login Client-1"/>
</p>
<p>
<b>Let's try to login to Client-1 with one of the newly created user credentials. For this example, it will be bana.niri</b>
</p>
<br />

<p>
<img src="https://imgur.com/e4PuHFw.png" height="80%" width="80%" alt="Login Success"/>
</p>
<p>
<b>Login with the new user credentials is successful.</b>
</p>
<br />

<p>
<img src="https://imgur.com/MkrDZJX.png" height="80%" width="80%" alt="Unlock Account"/>
</p>
<p>
<b>Let's try password locking bana.niri out of their account. Enter an incorrect password 10 times while trying to remote into Client-1. Login to DC-1 and navigate to Active Directory Users and Computers. Go to the EMPLOYEES folder and right click on the user, then click on the Account tab. Click Unlock account and Apply changes.</b>
</p>
<br />

<p>
<img src="https://imgur.com/Dxd4MV9.png" height="80%" width="80%" alt="Reset Password"/>
</p>
<p>
<b>If a user forgets their password, it can be reset by right clicking on the user name and going to Reset Password.</b>
</p>
<br />

