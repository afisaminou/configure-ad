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
- Powershell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
-


<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Create 2 virtual machines, one with Windows 10 (Client VM) and the other with Windows Server 2022 (DC/Domain Controller VM)
- Step 2: Set the DC’s NIC private IP address from Dynamic to Static
- Step 3: Connect to both VMs using Remote Desktop
- Step 4: Initiate a perpetual ping from the Client to the DC; if there is no reply, enable Core Networking Diagnostics in the DC’s firewall
- Step 5: Install Active Directory Domain Services on the DC and promote it to a domain controller
- Step 6: Create an admin account and Organizational Units (OU) in Active Directory Users and Computers (ADUC), then log back in using the admin account
- Step 7: Set the Client’s DNS settings to the DC’s Private IP address, then join the Client to the DC
- Step 8: Enable Remote Desktop for domain users to access the Client
- Step 9: Create user accounts using a PowerShell script (run PowerShell ISE as administrator)
- Step 10: Connect to the Client with Remote Desktop using one of the newly created user accounts

<h2>Deployment and Configuration Steps</h2>

Let's start our lab by creating two Virtual Machines (VMs) in Azure, one with Windows Server 2022 and the other with Windows 10.Make sure both VMs are in the same Net work and subnet. The Windows Server 2022 VM would serve as the Domain Controller (DC) and the Windows 10 VM would serve as the Client machine. Also, I set the DC’s NIC (Network Inteface Controller) private IP address from Dynamic to Static, so that later in the lab when I configured the Client’s DNS settings (DC’s private IP address), the Static IP address would make it easier for any services to access where a device is. Static IPs are better for remote access to a computer. A static IP address-enabled device does not need the device to send renewal requests.
<p>
<img src="https://i.imgur.com/1GvMyEx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p>
After connecting to both VMs using Remote Desktop, to ensure connectivity I initiated a perpetual ping from the Client to the DC. The requests were timing out, so I opened Windows Defender Firewall in the DC and enabled Core Networking Diagnostics (ICMPv4 protocol). This allowed the DC to reply to the requests as shown in the command-line interface (CLI).
<img src="https://i.imgur.com/hfBob3M.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/6e26Sg4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
<img src="https://i.imgur.com/Xy7nI6r.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>

Now we will log back into DC-1 to install Active Directory Domain Services (AD DS) from the Server Manager Dashboard. Once AD DS was installed, I Promoted the VM to Domain Controller so that it could manage devices and accounts on the domain. I setup a new forest as "mydomain.com" afterwards restart then log back into DC-1 as user: "mydomain.com\labuser". If you performed the steps properly you should be able to run AD Users & Computers as shown below.
<p>
<img src="https://i.imgur.com/enUXRsE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p> 
<img src="https://i.imgur.com/zw5kild.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p> 
<img src="https://i.imgur.com/FginuMU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
<img src="https://i.imgur.com/XVyVGRY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
