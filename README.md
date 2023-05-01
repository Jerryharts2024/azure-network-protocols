<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Part 1: Create our Resources in Azure
- Part 2a: Observe ICMP Traffic
- Part 2b: Observe SSH Traffic
- Part 2c: Observe DHCP Traffic
- Part 2d: Observe DNS Traffic
- Part 2e: Observe RDP Traffic

<h2>Actions and Observations</h2>
<h3>Part 1: Create our Resources in Azure </3>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- Create a Windows 10 Virtual Machine (VM)
  - While creating the VM, select the previously created Resource Group
  - While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet
  - Create a Linux (Ubuntu) VM
  - While create the VM, select the previously created Resource Group and Vnet
- Observe Your Virtual Network within Network Watcher

<br />

<h3> Part 2b Observe SSH Traffic </h3>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  To observe SSH traffic
</p>
 
- Back in Wireshark, filter for SSH traffic only
- From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
  - open cmd or powershell
  - type ssh labuser@10.0.0.5 (this is the username for the ubuntu machine)
  - type yes to comfirm your action
  - type the password for the ubuntu machine
  - Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
- observe the wireshark for all SSH activities in the ubuntu machine
- Exit the SSH connection by typing ‘exit’ and pressing [Enter]

<br />

<h3> Part 2c: Observe DHCP Traffic </h3>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- Back in Wireshark, filter for DHCP traffic only
- From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
- Observe the DHCP traffic appearing in WireShark

<br />

<h3> Part 2d: Observe DNS Traffic </h3>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- Back in Wireshark, filter for DNS traffic only
- From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
  - type nslookup www.google.com
  - nslookup www.disney.com
- Observe the DNS traffic being show in WireShark

<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
- Oserve the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?
- Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted


<br />


