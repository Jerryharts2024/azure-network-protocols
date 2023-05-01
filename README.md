<p align="center">
<img src="https://user-images.githubusercontent.com/131130119/235436639-e7b84a46-1ba6-4996-8871-d5ae77081298.JPG" alt="Traffic Examination"/>
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
<img src="https://user-images.githubusercontent.com/131130119/235441444-bce9dbf8-7153-41b2-8ad3-ce2e89db42a1.png" height="80%" width="80%" alt="Network Security Groups"/>
</p>

- Create a Windows 10 Virtual Machine (VM)
  - While creating the VM, select the previously created Resource Group
  - While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet
- Create a Linux (Ubuntu) VM
  - While create the VM, select the previously created Resource Group and Vnet
  - Observe Your Virtual Network within Network Watcher

<br />

<h3> Part 2a: Observe ICMP Traffic </h3>

<p>
<img src="https://user-images.githubusercontent.com/131130119/235440214-6e1846eb-de71-4c32-9712-ce8e16ee742f.png" height="80%" width="80%" alt="Network Security Groups"/>
</p>

- Use Remote Desktop to connect to your Windows 10 Virtual Machine

<p>
<img src="https://user-images.githubusercontent.com/131130119/235440439-5287c2d5-851a-4a99-840f-484dda6069bc.png" height="80%" width="80%" alt="Network Security Groups"/>
</p>

- Within your Windows 10 Virtual Machine, Install Wireshark
- Open Wireshark and filter for ICMP traffic only
- Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM
  - Observe ping requests and replies within WireShark

<p>
<img src="https://user-images.githubusercontent.com/131130119/235440856-87cc3a5a-e076-4f72-8c50-3098a58cba63.png" height="80%" width="80%" alt="Network Security Groups"/>
</p>

- From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark
- Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM

<p>
<img src="https://user-images.githubusercontent.com/131130119/235441157-72f3e8f1-bf60-426b-b295-f459e45deeaa.png" height="80%" width="80%" alt="Network Security Groups"/>
</p>

  - Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
  - Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
  - Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using

<p>
<img src="https://user-images.githubusercontent.com/131130119/235441789-9596cc38-2482-44e6-a0e5-15df9babe82c.png" height="80%" width="80%" alt="Network Security Groups"/>
</p>

  - Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
  - Stop the ping activity

<br />


<h3> Part 2b Observe SSH Traffic </h3>

<p>
<img src="https://user-images.githubusercontent.com/131130119/235442500-f6647c30-0a05-4247-bbc7-0b2f49f0bbcd.png" height="80%" width="80%" alt="Network Security Groups"/>
</p>

<p>
<img src="https://user-images.githubusercontent.com/131130119/235442306-c78717ee-ea44-4423-b9b0-55bdcffa4b5b.png" height="80%" width="80%" alt="Network Security Groups"/>
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
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Network Security Groups"/>
</p>

- Back in Wireshark, filter for DHCP traffic only
- From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
- Observe the DHCP traffic appearing in WireShark

<br />

<h3> Part 2d: Observe DNS Traffic </h3>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Network Security Groups"/>
</p>

- Back in Wireshark, filter for DNS traffic only
- From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
  - type nslookup www.google.com
  - nslookup www.disney.com
- Observe the DNS traffic being show in WireShark

<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Network Security Groups"/>
</p>

- Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
  - Observe the immediate non-stop spam of traffic? 
- Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?
  - Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted


<br />


