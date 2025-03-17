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

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Actions and Observations</h2>

Pulled up Microsoft Azure https://portal.azure.com/ Created Resource Group

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/7605c6284a77601d4890880754ce93fb92685782/2.jpeg">

Resource Group Name: RG-Network-Activities

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/83b3f03e33d9b34e0cb4d358403c221405f268ca/3.jpeg">

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/1ee17510e69d8d1d5a445e78a120c981ed24a1c6/4.jpeg">

Created VM (Virtual Machine) with new v-net and subnet
<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/375cbda14c3c3ac18e143fee25cd9dd6dca77e7a/6.jpeg"><br />

<img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/50c6838b5ff55194848b155d57ab235edef4d291/7.jpeg">

Created Linux (Ubuntu) VM with the previously selected Resource Group and Virtual Network (both Virtual Network staying the same)
9-> <img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/9.png">

10-> <img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/10.png">

11 -> <img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/11.png">

12 -> <img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/12.png">

Finished creating 2 VM’s one windows and the other Linux.

13 -> <img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/13.png">

Installed and opened remote desktop connection (RDC)
Used Remote Desktop to connect to your Windows 10 VM public IP Address 20.62.43.117

14 -> <img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/14.png">

Logged in using Username and Password
Username: labuser
Password: Cyberlab123!

15 -> <img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/15.png">


Dowloaded Wireshark via internet [https://www.wireshark.org](https://www.wireshark.org)
16 -> <img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/5e9eef3599a01daf9e20c9c995a37ce48b2fa55c/16.png">

17 --> <img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/3d775501f6c2651b083d7e1f79fe449e60e000a2/17.png">

18 --> <img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/3d775501f6c2651b083d7e1f79fe449e60e000a2/18.png">

Installed WireShark on window 10 vm and opened WireShark and started packet capture.

20--> <img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/cbc329756f2e187b6ec2371190856be0be965280/20.png">

Opened PowerShell Command Prompt from the start menu. (Typed PowerShell in search engine of the start menu)

21 --> <img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/b42650f79369e566f96227bf2ba305f815022ab4/21.2.png">

22 --> <img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/b42650f79369e566f96227bf2ba305f815022ab4/23.png">

23 --> <img src="https://github.com/timothycooperjr/Exploring-Azure-and-Networking-Concepts/blob/b42650f79369e566f96227bf2ba305f815022ab4/24.png">

Observed Ping request and replies within WireShark















