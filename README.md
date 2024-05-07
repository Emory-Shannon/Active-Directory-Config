<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Creating Azure Resources
- Installing Active Directory
- Joing Client to AD
- Setup Remote Desktop for non-administrative users

<h2>Deployment and Configuration Steps</h2>

<h3>Setting up Azure Resources</h3>
<p>
<img src="AD-Resources.PNG" height="80%" width="80%" alt="AD-Resources.PNG"/>
</p>
<p>
<img src="AD-Nic-static.PNG" height="80%" width="80%" alt="AD-Nic-static.PNG"/>
</p>
<p>
<img src="AD-Nic Static 2.PNG" height="80%" width="80%" alt="AD-Nic Static 2.PNG"/>
</p>
<p>
<img src="AD-Nic Static 3.PNG" height="80%" width="80%" alt="AD-Nic Static 3.PNG"/>
</p>
<p>
Create two virtual machines, one called DC, and the other called "Client 1". When creating "DC-1" use windows server as the operating system. "Client 1" will be windows 10. Make sure they both are on the same subnet. After creating both, go to your "DC-1" VM and set the Network interface to be static. Do this by cliking on to the VM then going to network settings. Once your there click on the Network Interface then navigate to "IP Configurations", from there set the IP to static.
</p>
<br />

<h3>Ensuring Connectivity</h3>

<p>
<img src="AD- Connectivity 1.PNG" height="80%" width="80%" alt="Connectivity 1.PNG"/>
</p>

<p>
<img src="AD-Connectivity 3.PNG" height="80%" width="80%" alt="AD-Connectivity 3.PNG"/>
</p>

<p>
<img src="AD- Connectivity 2.PNG" height="80%" width="80%" alt="AD- Connectivity 2.PNG"/>
</p>
<p>
Login to "Client-1" with remote desktop and ping "DC-1's" private IP address with ping "-t (ip address)". Login to the domain controller and enable ICMPv4 on the local windows firewall. Check back on "client 1" to see if it worked.
</p>
<br />

<h3>Installing Active Directory</h3>

<p>
<img src="AD-Installation.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="AD- Add forest.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="AD- Domain Login.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
Login to "DC-1" and install domain services from the service manager dashboard. Once installed, click the flag with the warning sign on the top right of the server manager. On this page set up a new forrest as "mydomain.com". Once you do this, restart your VM and log back in. 
<p>

<h3>Post Installation setup</h3>

<p>
<img src="AD- Active Directory Users and Computers.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="AD-creating-organizational-unit.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="AD- Adding Jane Doe.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="AD-Giving Jane Admin2.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
  In your "DC-1 VM", open up "Active Directory Users and computers". Then Create two organizational Units named _ADMINS and _EMPLOYEES. Once that is done add an "admin" named Jane Doe to _ADMINS. After adding Jane, access the properties tab by right cliking on the name. Navigate to "member of" and add the role "Domain Admins" by typing it. Press apply and Jane is now an Admin.
</p>

<h3>Joining "Client-1" to "DC-1"</h3>

<p>
<img src="AD- Changing Client 1 DNS settings 1.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="AD- Changing Client 1 DNS settings 2.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="AD- Rename this PC.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="AD- Joing Confirmation.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
  The First step to joining Client-1 to DC-1 is to change the dns setting of Client-1 to match the IP address of DC-1. Follow the images to navigate. Next, login into Client-1 with an admin account and navigate to system properties (right click windows button and go to system). Now find "Rename this PC" and click that. Now plug the domain you created (mydomain.com) into the text box. Confirm it by logging in with an admin account then restart your VM. To check the confirmation navigate to "Active Directory Users and Computers" and find the computers folder under the domain. Client 1 should show up just like the image above. 
</p>

<h3>Setting up Remote Desktop for Non-Administrative Users</h3>

<p>
<img src="AD- Remote Desktop 1.PNG"80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="AD-Remote Desktop 2.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
  
<p>
To give access to non-admin users for remote desktop, navigate to the system properties and find "Select users that can remotely access this PC". Once on the menu add the group "Domain Users" to the text 
box. We will confirm this in the next section.</p>


<h3>Active Directory Activity</h3>

<p>
<img src="AD-Non admin login 1.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="AD- Non Admin Login 2.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="AD- Non admin user example.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
 Now that you set up remote desktop, create a user in the _EMPLOYEES folder you created inside "Active Directory Users and Computers". Once a user has been created log into client-1 with thier information. 
</p>

<br />
