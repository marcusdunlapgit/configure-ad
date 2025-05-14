<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Preparing Active Directory in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resource Group and Virtual Network
- Deploy Domain Controller (DC-1)
- Configure Network Settings and DNS
- Deploy and Connect Client (Client-1)

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Resource Group and Virtual Network"/>
</p>
<p>
<strong>Step 1: Create Resource Group and Virtual Network</strong><br />
- Create a new resource group named <code>Active-Directory-RG</code><br />
- Create a virtual network named <code>Active-Directory-VNET</code> with a subnet<br />
- Ensure the virtual network is placed inside the <code>Active-Directory-RG</code>
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Domain Controller Setup"/>
</p>
<p>
<strong>Step 2: Setup Domain Controller (DC-1)</strong><br />
- Deploy a Windows Server 2022 VM named <code>DC-1</code> in the <code>Active-Directory-VNET</code><br />
- Use the credentials: <code>labuser / Cyberlab123!</code><br />
- Set DC-1’s NIC private IP address to static:<br />
  <code>DC-1 → Network Settings → VNet NIC → Ipconfig1 → Change to STATIC → Save</code><br />
- Disable the Windows Firewall:<br />
  <code>Run → wf.msc → Windows Defender Firewall Properties → Turn Off Domain, Private & Public → Apply</code>
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Client Setup and DNS Configuration"/>
</p>
<p>
<strong>Step 3: Setup Client-1 VM and DNS</strong><br />
- Create a Windows 10 VM named <code>Client-1</code> using same region and VNET as <code>DC-1</code><br />
- Use the credentials: <code>labuser / Cyberlab123!</code><br />
- Change Client-1 DNS to DC-1’s private IP:<br />
  <code>Client-1 → Network Settings → VNet NIC → DNS Servers → Custom → Enter DC-1's IP</code><br />
- Restart Client-1 via Azure Portal
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Connectivity Verification"/>
</p>
<p>
<strong>Step 4: Verify Connectivity</strong><br />
- Login to <code>Client-1</code><br />
- Ping <code>DC-1</code>'s private IP to verify connectivity:<br />
  <code>ping 10.0.0.4</code><br />
- Open PowerShell and run <code>ipconfig /all</code> to confirm DC-1's IP as DNS server
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Lab Management"/>
</p>
<p>
<strong>Finishing Up</strong><br />
- Do not delete the VMs. They will be used in future labs.<br />
- To save cost, stop the VMs from the Azure Portal when done for the day
</p>
<br />
