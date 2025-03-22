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

## Part 1: Create Virtual Machines

1. Log in to [Azure Portal](https://portal.azure.com/).
2. **Create a Resource Group**:
   - Navigate to "Resource Groups" and click "Create."
   - Provide a name for your Resource Group and select a region.
   - Click "Review + Create," then "Create."

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/7605c6284a77601d4890880754ce93fb92685782/2.jpeg">

Created Resource Group Name: RG-Network-Activities

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/83b3f03e33d9b34e0cb4d358403c221405f268ca/3.jpeg">

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/1ee17510e69d8d1d5a445e78a120c981ed24a1c6/4.jpeg">

Created Virtual Machine (VM)

     - Selected the resource Group that was previously created.
     - Configured the VM to Windows 10
     - Created Username and Password
     - Under the Networking Tab, created a new virtual network (vnet) and titled it "vnet"
     - Completed the setup and deployed the VM


<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/375cbda14c3c3ac18e143fee25cd9dd6dca77e7a/6.jpeg"><br />

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/50c6838b5ff55194848b155d57ab235edef4d291/7.jpeg">

Created Linux (Ubuntu) VM with the previously selected Resource Group and Virtual Network as "vnet" (both Virtual Network staying the same)

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/9.png">

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/10.png">

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/11.png">

Finished creating 2 VM’s one windows and the other Linux.


<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/12.png">

Installed and opened remote desktop connection (RDC)
Used Remote Desktop to connect to your Windows 10 VM public IP Address 20.62.43.117

      
<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/13.png">

Logged in using Username and Password
(Username: labuser, Password: Cyberlab123!)


<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/14.png">

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/15.png">

Dowloaded and Installed Wireshark via internet [https://www.wireshark.org](https://www.wireshark.org)

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/16.png">

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/3d775501f6c2651b083d7e1f79fe449e60e000a2/17.png">

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/3d775501f6c2651b083d7e1f79fe449e60e000a2/18.png">

In Windows 10 vm,  opened WireShark and started packet capture.

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/c197a3ed08253125d11d30fe650da3e1b0d2fe1d/Packet%20Capture%202.png">

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/c197a3ed08253125d11d30fe650da3e1b0d2fe1d/Packet%20Capture%201.png">


## Part 2: Observe ICMP Traffic

1. Use [Microsoft Remote Desktop](https://apps.microsoft.com/store) to connect to your Windows 10 Virtual Machine (if on Mac, install the client first).
2. **Install Wireshark** on the Windows 10 VM:
   - Download and install Wireshark from [https://www.wireshark.org/](https://www.wireshark.org/).
3. Open Wireshark and start a packet capture.
4. Filter for ICMP traffic in Wireshark.
5. Retrieve the private IP address of the Ubuntu VM and attempt to ping it from the Windows 10 VM:
   - Open Command Prompt or PowerShell and run: `ping <Ubuntu VM Private IP>`.
   - Observe the ping requests and replies in Wireshark.
6. From the Windows 10 VM, ping a public website (e.g., `www.google.com`) and observe the ICMP traffic in Wireshark.

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/cbc329756f2e187b6ec2371190856be0be965280/20.png">

PowerShell Command Prompt from the start menu. (Typed PowerShell in search engine of the start menu)

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/1762b444ca2583e02cb5acccdd64e72ea793bf22/22.png">

Retrieved the private IP address of the Ubuntu VM (linux-vm) and attemptrf to ping it from within the Windows 10 VM

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/b42650f79369e566f96227bf2ba305f815022ab4/21.2.png">

Observed Ping request and replies within WireShark

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/b42650f79369e566f96227bf2ba305f815022ab4/24.png">

 
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

## Part 4: Observe Various Protocol Traffic (SSH, DHCP ,DNS, and RDP) using WireShark
### Observe SSH Traffic

1. In Wireshark, start a new packet capture and filter for SSH traffic.
2. From the Windows 10 VM, SSH into the Ubuntu VM:
   - Command: `ssh <username>@<Ubuntu VM Private IP>`.
   - Enter the password when prompted.
3. Type commands within the SSH session and observe the SSH traffic in Wireshark.
4. Exit the SSH session: `exit`.

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/b84a648b19c8faf67c3868b1fe395423e0191fa7/SSH.png">

### Observe DHCP Traffic

1. In Wireshark, filter for DHCP traffic.
2. From the Windows 10 VM, issue a new IP address:
   - Open PowerShell as admin and run: `ipconfig /renew`.
3. Observe the DHCP traffic in Wireshark.

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/c4ee181d005383896d3bc7fcd133601f53515fcb/DHCP%202.png">

### Observe DNS Traffic

1. In Wireshark, filter for DNS traffic.
2. From the Windows 10 VM, use `nslookup` to find IP addresses for websites:
   - Example: `nslookup google.com`, `nslookup disney.com`.
3. Observe the DNS traffic in Wireshark.

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/7d776839335876ff103d7ce505a65945693dcbde/DNS.png">

### Observe RDP Traffic

1. In Wireshark, filter for RDP traffic:
   - Use the filter: `tcp.port == 3389`.
2. Observe the continuous RDP traffic between the Windows 10 VM and your local machine.

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/6061122901208fed5cb13e0860f679402eb9f3ca/RDP.png">
 

















