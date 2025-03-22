<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

1. Created Virtual Machines in Azure
2. Observed ICMP Traffic between Virtual Machines using Wireshark
3. Configure a Firewall (Network Security Group) and analyze its impact on network traffic
4. Observe various protocol traffic (SSH, DHCP, DNS, RDP) using Wireshark

<h2>Actions and Observations</h2>

1 --> Pulled up Microsoft Azure
Logged into Azure Portal https://portal.azure.com/
Create a Resource Group

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/7605c6284a77601d4890880754ce93fb92685782/2.jpeg">

2 -->Created Resource Group Name: RG-Network-Activities

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/83b3f03e33d9b34e0cb4d358403c221405f268ca/3.jpeg">

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/1ee17510e69d8d1d5a445e78a120c981ed24a1c6/4.jpeg">

3 -->Created Virtual Machine (VM)

     - Selected the resource Group that was previously created.
     - Configured the VM to Windows 10
     - Created Username and Password
     - Under the Networking Tab, created a new virtual network (vnet) and titled it "vnet"
     - Completed the setup and deployed the VM


<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/375cbda14c3c3ac18e143fee25cd9dd6dca77e7a/6.jpeg"><br />

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/50c6838b5ff55194848b155d57ab235edef4d291/7.jpeg">

4--> Created Linux (Ubuntu) VM with the previously selected Resource Group and Virtual Network as "vnet" (both Virtual Network staying the same)

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/9.png">

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/10.png">

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/11.png">

5 -> Finished creating 2 VM’s one windows and the other Linux.


<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/12.png">

6 -> Installed and opened remote desktop connection (RDC)
      Used Remote Desktop to connect to your Windows 10 VM public IP Address 20.62.43.117

      
<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/13.png">

7 -> Logged in using Username and Password
(Username: labuser, Password: Cyberlab123!)


<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/14.png">

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/15.png">

8 -> Dowloaded Wireshark via internet [https://www.wireshark.org](https://www.wireshark.org)

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/16.png">

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/3d775501f6c2651b083d7e1f79fe449e60e000a2/17.png">

9 --> Installed WireShark on window 10 vm and opened WireShark and started packet capture.

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/3d775501f6c2651b083d7e1f79fe449e60e000a2/18.png">

10 --> Within wireshark, I filtered for ICMP Traffic only.

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/cbc329756f2e187b6ec2371190856be0be965280/20.png">

11 --> PowerShell Command Prompt from the start menu. (Typed PowerShell in search engine of the start menu)

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/1762b444ca2583e02cb5acccdd64e72ea793bf22/22.png">

12 --> Retrieved the private IP address of the Ubuntu VM (linux-vm) and attemptrf to ping it from within the Windows 10 VM

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/b42650f79369e566f96227bf2ba305f815022ab4/21.2.png">

13 --> Observed Ping request and replies within WireShark

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/b42650f79369e566f96227bf2ba305f815022ab4/24.png">

14 --> Configuring a Firewall (Network Security Group)
Initiatied a Perpetual/Non-stop ping from Windows 10 VM to Ubuntu VM (Using PowerShell Ping 10.0.0.5-t)

15 --> Firewall will block all incoming trafic to Linux Ubuntu VM and stop the pings.

16 --> Create/Add a Rule
Destination Port Rangers *(ICMP doesnt use a port)
Protocol - ICMPv4 (Ping uses ICMPv4 protocol)
Action - Deny (The Firewall will drop the traffic)
Priority 290 (Which puts the rule above the 300 SSH rule)

17 --> Disabled Incoming (Inbound)
Request Timed out in PowerShell
Request -> Reply -> Request -t

18 --> Deleted Firewall (Security Rule)

19 --> RE-enabled the ICMP Traffic in Wireshark and the command line Ping activity

20 --> Controc + C to Stop the Ping Activity

Observe SSH Traffic
Logged into Windows VM
Opened up Wireshark and start a new packet capture

Retrieved the IP address form the Linux VM

Opened PowerShell and typed : SSH labuser @10.0.0.6
SSH (SecureShell) - used to make a secure connection from one computer to another computer.
From windows computer SSH connection to linux computer and observe the traffic 
Filter for SSH Traffic Only by typing SSH in WireShark. (SSH uses TCP Port 22)
From Windows 10 VM I attempted to 
## Part 3: Configure a Firewall (Network Security Group)

### Observe ICMP Traffic with Firewall Changes

1. Initiate a continuous ping from your Windows 10 VM to the Ubuntu VM:
   - Command: `ping <Ubuntu VM Private IP> -t`.
2. Open the Network Security Group associated with the Ubuntu VM.
3. Disable inbound ICMP traffic in the Network Security Group.
4. Observe the ICMP traffic in Wireshark and the command line Ping activity (should stop).
5. Re-enable ICMP traffic in the Network Security Group.
6. Observe the ICMP traffic in Wireshark and the command line Ping activity (should resume).
7. Stop the ping activity.

<p>
<img src="https://github.com/timothycooperjr/timothycooperjr-Configuring-a-Firewall-Network-Security-Group-/blob/17c0bf559d8304a0cc2164007124d81135ea8385/2.png"></p>

<p>
<img src="https://github.com/timothycooperjr/timothycooperjr-Configuring-a-Firewall-Network-Security-Group-/blob/17c0bf559d8304a0cc2164007124d81135ea8385/3.png"></p>

<p>
<img src="https://github.com/timothycooperjr/timothycooperjr-Configuring-a-Firewall-Network-Security-Group-/blob/17c0bf559d8304a0cc2164007124d81135ea8385/4.png"></p>

<img src="https://github.com/timothycooperjr/timothycooperjr-Configuring-a-Firewall-Network-Security-Group-/blob/f25ae257ecb5afd863057d16cf53d6cf5da78fde/Configuring%20a%20Firewall.png">

<p>
<img src="https://github.com/timothycooperjr/timothycooperjr-Configuring-a-Firewall-Network-Security-Group-/blob/17c0bf559d8304a0cc2164007124d81135ea8385/5.png">
</p>

<img src="https://github.com/timothycooperjr/timothycooperjr-Configuring-a-Firewall-Network-Security-Group-/blob/f25ae257ecb5afd863057d16cf53d6cf5da78fde/Configuring%20a%20Firewall%202.png">

<img src="https://github.com/timothycooperjr/timothycooperjr-Configuring-a-Firewall-Network-Security-Group-/blob/f25ae257ecb5afd863057d16cf53d6cf5da78fde/Configuring%20a%20Firewall%203.png">

<img src="https://github.com/timothycooperjr/timothycooperjr-Configuring-a-Firewall-Network-Security-Group-/blob/f25ae257ecb5afd863057d16cf53d6cf5da78fde/Configuring%20a%20Firewall%204.png">

<img src="https://github.com/timothycooperjr/timothycooperjr-Configuring-a-Firewall-Network-Security-Group-/blob/f25ae257ecb5afd863057d16cf53d6cf5da78fde/Configuring%20a%20Firewall%205.png">

<img src="https://github.com/timothycooperjr/timothycooperjr-Configuring-a-Firewall-Network-Security-Group-/blob/f25ae257ecb5afd863057d16cf53d6cf5da78fde/Configuring%20a%20Firewall%206.png">

### Observe DHCP Traffic

1. In Wireshark, filter for DHCP traffic.
2. From the Windows 10 VM, issue a new IP address:
   - Open PowerShell as admin and run: `ipconfig /renew`.
3. Observe the DHCP traffic in Wireshark.

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/c4ee181d005383896d3bc7fcd133601f53515fcb/DHCP%202.png">

 

















