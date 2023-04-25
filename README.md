<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Powershell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

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
<img src="https://i.imgur.com/xMWxaSv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<p>
After connecting to both VMs using Remote Desktop, to ensure connectivity I initiated a perpetual ping from the Client to the DC. The requests were timing out, so I opened Windows Defender Firewall in the DC and enabled Core Networking Diagnostics (ICMPv4 protocol). This allowed the DC to reply to the requests as shown in the command-line interface (CLI).
</p>
<img src="https://i.imgur.com/dnYvUTl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/8SRk3AF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<p>
Now we will log back into DC-1 to install Active Directory Domain Services (AD DS) from the Server Manager Dashboard. Once AD DS was installed, I Promoted the VM to Domain Controller so that it could manage devices and accounts on the domain. I setup a new forest as "mydomain.com" afterwards restart then log back into DC-1 as user: "mydomain.com\labuser". If you performed the steps properly you should be able to run AD Users & Computers as shown below.
<p>
<img src="https://i.imgur.com/v7QHRGf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p> 
<img src="https://i.imgur.com/FlamLHS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p> 
<p>
Active Directory is all set up! Let's create two(2) Organizational Units (OU) named _ADMINS and _EMPLOYEES. Now, let's create a new User "Jane Doe" as an Administrator with the username: Jane_admin and add her as a member of Domain Admins Security Group. Logged out from the default account we were in and logged back in as jane.
</p> 
<img src="https://i.imgur.com/5GUzjzt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/7lZfJaJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
In order to cintinue setting up my domain, I will join Client-1 to the domain (mydomain.com).From the azure portal we will change client-1's DNS settings to the DC's Private IP address. After you do that restart Client-1 from within the Azure portal. Our picture below shows verification that client-1 is on the DC-1 DNS.
</p>
<img src="https://i.imgur.com/NGw6Dft.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

Now we will set up remote desktop for non-administrative users on Client-1. We have to log into Client-1 as an admin and open system properties. Click on "Remote Desktop", allow "domain users" access to remote desktop. Enabling this for Domain Users would allow for any user accounts in the domain to be able to log into Client-1 as a normal user.
</p>
<img src="https://i.imgur.com/fZ2gcOV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br /> 
</p>
Finally, to verify that noraml users can RDP into Client-1, I will use a Powershell script to generate 10,000 (Thousands) of users into the domain. After the users are created we will randomly select one and RDP into Client-1.
</p>
<img src="https://i.imgur.com/QBffW1K.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/Utf0x7S.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<h3>Bonus Step: How to unlock users' accounts and reset passwords</h3>
In order to unlock a user's account, right click the user account and click "Properties." 
Click on "Unlock Account." You can also right click the user account and "Reset Password..."

<p>
<img src="https://i.imgur.com/HTcYBBU.png" height="80%" width="80%" alt="49"/>
</p>

<p>
<img src="https://i.imgur.com/lNfDusu.png" height="80%" width="80%" alt="50"/>
</p>

<p>
<img src="https://i.imgur.com/HrMlyi7.png" height="80%" width="80%" alt="51"/>
</p>

Thank you for checking out my Active Directory tutorial! I hope you were able to learn and build some intuition on how to use Active Directory. I would suggest doing this exercise several times in order to build the knowledge and skills in Active Directory. Especially if you are trying to shoot for an IT job, where Active Directory is used heavily. 

<p></p>

**REMEMBER TO DELETE YOUR RESOURCES ONCE YOU ARE DONE WITH THE LAB!**

