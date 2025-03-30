1.Router-on-a-Stick Configuration
Assuming Router Interface: GigabitEthernet0/0 connected to the switch:

# Enter configuration mode
configure terminal

# Create subinterfaces for VLANs
int gig0/0.10
 encapsulation dot1Q 10
 ip address 192.168.1.1 255.255.255.192  # First usable IP in VLAN 10

int gig0/0.20
 encapsulation dot1Q 20
 ip address 192.168.1.65 255.255.255.192  # First usable IP in VLAN 20

int gig0/0.30
 encapsulation dot1Q 30
 ip address 192.168.1.129 255.255.255.192  # First usable IP in VLAN 30

# Enable interfaces
no shutdown

# Save configuration
end
write memory




2. DHCP Configuration

If the router is also acting as a DHCP server, configure DHCP pools:

configure terminal
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


3. Switch Configuration (Trunking & VLAN Assignment)

Assuming switch interface fa0/1 is connected to the router:

configure terminal

# Create VLANs

# Set trunk port to the router
int fa0/1
 switchport mode trunk
 #do write

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


This setup will:
1. Subnet your network into three VLANs.
2. Configure router-on-a-stick to enable inter-VLAN routing.
3. Enable DHCP for each VLAN.
4. Set up VLANs and trunking on the switch.

