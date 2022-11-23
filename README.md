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
<br />
