# 🖧 VLAN and Inter-VLAN Routing Project (Cisco Packet Tracer)

# 📌 Project Overview
This project demonstrates the configuration of VLANs (Virtual Local Area Networks) and Inter-VLAN Routing using Cisco Packet Tracer. The network includes multiple VLANs, a router, a switch, and various end devices.

# ⚡ Features

✔️ Three VLANs (Each with a PC, Printer, and Access Point)  
✔️ Router-on-a-stick Configuration for Inter-VLAN Routing  
✔️ VLAN Trunking and Proper Subnetting  
✔️ Successful VLAN Communication via Router  

# 🛠️ Technologies Used
- Cisco Packet Tracer  
- VLAN Configuration (Switchport Mode Access & Trunk)  
- Router Sub-Interfaces for Inter-VLAN Routing  
- IP Addressing & Subnetting  

# 🔧 Network Setup

- VLAN 10: PC1, Printer1, AP1  
- VLAN 20: PC2, Printer2, AP2  
- VLAN 30: PC3, Printer3, AP3  
- Router: Configured for Inter-VLAN Routing  
- Switch: VLAN Assignments & Trunk Ports  

# 📝 How to Use the Project

1️⃣ Download Cisco Packet Tracer if you don’t have it.  
2️⃣ Clone or Download this repository.  
3️⃣ Open the `.pkt` file in Cisco Packet Tracer.  
4️⃣ Run Commands (Use CLI to verify VLANs and routing).  


# 📂 Download the Project File

You can download the Cisco Packet Tracer project file from Google Drive(https://drive.google.com/file/d/1Qsb8yVpVoc97U4XnQGt5C9ibRTsp_BiC/view?usp=sharing).

# 📜 Commands Used
1.Router-on-a-Stick Configuration
Assuming Router Interface: GigabitEthernet0/0 connected to the switch:

# Enter configuration mode
configure terminal

# Create subinterfaces for VLANs
#For vlan 10
 int gig0/0.10
 
 encapsulation dot1Q 10
 
 ip address 192.168.1.1 255.255.255.192  # First usable IP in VLAN 10

#For vlan 20
 int gig0/0.20
 
 encapsulation dot1Q 20
 
 ip address 192.168.1.65 255.255.255.192  # First usable IP in VLAN 20

#For vlan 30
 int gig0/0.30
 
 encapsulation dot1Q 30
 
 ip address 192.168.1.129 255.255.255.192  # First usable IP in VLAN 30




# Save configuration
  end
  write memory




# 2. DHCP Configuration

If the router is also acting as a DHCP server, configure DHCP pools:

# configure terminal
  #service dhcp # to enable dhcp service on the devices

# VLAN 10 DHCP

 ip dhcp pool Admin-pool
 
 network 192.168.1.0 255.255.255.192
 
 default-router 192.168.1.1
 
 dns-server 192.168.1.1
 
 domain-name Admin.com

# VLAN 20 DHCP

 ip dhcp pool Finance-pool
 
 network 192.168.1.64 255.255.255.192
 
 default-router 192.168.1.65
 
 dns-server 192.168.1.65
 
 domain-name Finance.com
 

# VLAN 30 DHCP
 ip dhcp pool customer-pool
 
 network 192.168.1.128 255.255.255.192
 
 default-router 192.168.1.129
 
 dns-server 192.168.1.129
 
 domain-name customer.com


# Save configuration
 end
 write memory


# 3. Switch Configuration (Trunking & VLAN Assignment)

# Assuming switch interface fa0/1 is connected to the router:

 configure terminal

# Create VLANs

# Set trunk port to the router
 int fa0/1
 
 switchport mode trunk
 
 do write

# Assign ports to VLANs
 int range fa0/2-4
 
 switchport mode access
 
 switchport access vlan 10
 

 int range fa0/5-7
 
 switchport mode access
 
 switchport access vlan 20

 
 int range fa0/8-10
 
 switchport mode access
 
 switchport access vlan 30
 

# Save configuration
 end
 write memory


# This setup will:

1. Subnet your network into three VLANs.
2. Configure router-on-a-stick to enable inter-VLAN routing.
3. Enable DHCP for each VLAN.
4. Set up VLANs and trunking on the switch.

