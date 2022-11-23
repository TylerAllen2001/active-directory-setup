<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Setting up Active Directory through Microsoft Azure</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
-Microsoft Azure

<h2>Configuration Steps  </h2>

<p>
<img src="https://i.imgur.com/d22FHIm.png" height="80%" width="80%" alt="Domain Controller Connection with Client"/>
</p>

- On Microsoft Azure, we will create two different VMs (virtual machines) on the same VNET with two different resource groups. The Domain Controller will be called DC-1 and the Client Machine will be called Client-1. 

- Change DC-1 to a static IP address as it is used for Active Directory services for Client-1. 
- Client-1 will join DC-1's Domain and will use it as its DNS server.
</p>
<br />

<p>
<img src="https://i.imgur.com/HvZBWzc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- Client-1 will connect to DC-1 and we will try to ping DC-1 from the client VM. 
- Pinging will not work correctly because we have to enable ICMPv4 on the DC-1 Firewall. Pinging should be successful now.
<br />
<p> <img src="https://i.imgur.com/1lrrGPw.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> </p>

- Now log back into DC-1 and install AD User & Computers. Promote VM to DC, and create a new forest titled " mydomain.com ". 
- After creation, restart the VM and log back into DC-1 as mydomain.com\labuser. 
- You will now be able to run AD Users & Computers.
<img src="https://i.imgur.com/cGjvRke.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- We can now create Organizational Units (OU). 
- Create a OU named _EMPLOYEES and _ADMINS ( must be named exactly or rest of project won't work ) You can do this by right-clicking domain area and selecting new Organizational Unit.
- Click in OU and right click, select new and select User.
- Fill out information for new user. This user will be named Jane Doe. She will be an admin with the username Jane_Admin. 
- Add Jane to the domain admins security group
<img src="https://i.imgur.com/hL7g5Y5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/kcgvzdE.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
From now on you can use Jane_admin as the administrator account. Now we will join Client-1 to the domain (mydomain.com) from the azure portal we will change client-1's DNS settings to the DC's Private IP address. After you do that restart Client-1 from within the Azure portal. Our picture below shows verification that client-1 is on the DC-1 DNS. 
</p>
<img src="https://i.imgur.com/jbrGTXW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
</p>
<img src="https://i.imgur.com/kvcm2cY.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
</p>
<p>
We have to join Client-1 to the domain in order to do so navigate to your system settings and go to about. Off to the right select rename this pc (advanced). From there select to change the domain. Enter "mydomain.com" after that enter your credentials from mydomain.com\labuser. Your computer will restart and then client-1 will be a part of mydomain.com
</p>
<br />
<p>
  <p>
<img src="https://i.imgur.com/Ze0Em5e.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Wonderufl Client-1 is now a part of the domain. Now we will set up remote desktop for non-administrative users on Client-1. We have to log into Client-1 as an admin and open system properties. Click on "Remote Desktop", allow "domain users" access to remote desktop. After completing those steps you should be able to log into Client-1 as a normal user.
</p>
<br />

<p>
  <p>
<img src="https://i.imgur.com/SApOKiE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lastly to verify that noraml users can RDP into Client-1 we will use a script to generate thousands of users into the domain. We will input the script in powershell, after the users are created we will select one and RDP into Client-1.
</p>
<br />
<img src="https://i.imgur.com/EzWG8ug.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
<p>
  <p>
<img src="https://i.imgur.com/Gkpe68K.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/n3gMwQV.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
As you can see the Powershell script created a user with the username "bab.hubo" We were able to login to Client-1 with his credentials as a normal user. 
</p>
