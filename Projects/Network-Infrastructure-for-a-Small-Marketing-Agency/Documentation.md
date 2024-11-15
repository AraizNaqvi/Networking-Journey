3. Documentation

The following contains the step-by-step documentation to each part of the Network.

---
### **Subnet 1 Configurations**

Starting with connections, here is how devices are connected:
- Router 1 - Switch 1: GigabitEthernet
- Switch 1 - Server 1: FastEthernet
- Switch 1 - Printer 1: FastEthernet
- Switch 1 - PC 1-5: FastEthernet

Moving into individual components:

The Subnet Addresses assigned for this subnet are:
```
Subnet: 192.168.1. 0000 0000/26 => 192.168.1.0/26
1st Address: 192.168.1. 0000 0001/26 => 192.168.1.1/26
Last Address: 192.168.1. 0011 1110/26 => 192.168.1.62/26
Broadcast Address: 192.168.1. 0011 1111/26 => 192.168.1.63/26
```

#### Router 1

Here, setup was done as follows:
```
Router>en
Router#conf t
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#interface gigabitEthernet 0/0/0
Router(config-if)#ip address 192.168.1.62 255.255.255.192
Router(config-if)#no shutdown
Router(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0, changed state to up

Router#show ip interface brief
Interface IP-Address OK? Method Status Protocol
GigabitEthernet0/0/0 192.168.1.62 YES manual up up
GigabitEthernet0/0/1 unassigned YES unset administratively down down
GigabitEthernet0/0/2 unassigned YES unset administratively down down
Vlan1 unassigned YES unset administratively down down
```

Clearly, Router was assigned with IP Address of 192.168.62/26 which is the last IP Address in Subnet 1.

#### Switch 1

Here, setup was done as follows:
```
Switch>en
Switch#conf t
Enter configuration commands, one per line. End with CNTL/Z.
Switch(config)#int vlan 1
Switch(config-if)#no shutdown
Switch(config-if)#
%LINK-5-CHANGED: Interface Vlan1, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan1, changed state to up
Switch(config-if)#ip address 192.168.1.61 255.255.255.192
Switch(config-if)#exit
Switch(config)#ip default-gateway 192.168.1.62
Switch(config)#exit
Switch#
%SYS-5-CONFIG_I: Configured from console by console

Switch#show ip interface brief
Interface IP-Address OK? Method Status Protocol
FastEthernet0/1 unassigned YES unset up up
FastEthernet0/2 unassigned YES unset up up
FastEthernet0/3 unassigned YES unset up up
FastEthernet0/4 unassigned YES unset up up
FastEthernet0/5 unassigned YES unset up up
FastEthernet0/6 unassigned YES unset up up
FastEthernet0/7 unassigned YES unset up up
FastEthernet0/8 unassigned YES unset down down
FastEthernet0/9 unassigned YES unset down down
FastEthernet0/10 unassigned YES unset down down
FastEthernet0/11 unassigned YES unset down down
FastEthernet0/12 unassigned YES unset down down
FastEthernet0/13 unassigned YES unset down down
FastEthernet0/14 unassigned YES unset down down
FastEthernet0/15 unassigned YES unset down down
FastEthernet0/16 unassigned YES unset down down
FastEthernet0/17 unassigned YES unset down down
FastEthernet0/18 unassigned YES unset down down
FastEthernet0/19 unassigned YES unset down down
FastEthernet0/20 unassigned YES unset down down
FastEthernet0/21 unassigned YES unset down down
FastEthernet0/22 unassigned YES unset down down
FastEthernet0/23 unassigned YES unset down down
FastEthernet0/24 unassigned YES unset down down
GigabitEthernet0/1 unassigned YES unset up up
GigabitEthernet0/2 unassigned YES unset down down
Vlan1 192.168.1.61 YES manual up up
```

Clearly, Switch was assigned with IP Address of 192.168.61/26 which is the Second last IP Address in Subnet 1.


#### Server 1

Here, setup was done as follows:
First, manually I set:
- IP Address: 192.168.1.60/26

Then, I set the DHCP service to **active** and configured the settings to the following based on the calculations:
View ![[Server1_DHCP.png]]


#### PC & Printer Configuration

Nothing much done here.
Simply set all PC's & Printer to dynamically set IP Addresses via DHCP as follows:

View ![[PC1_DHCP.png]]

With this Subnet 1 was completed.



### **Subnet 2 Configurations**

Starting with connections, here is how devices are connected:
- Router 1 - Router D: GigabitEthernet

Moving into individual components:

The Subnet Addresses assigned for this subnet are:
```
Subnet: 192.168.1. 0100 0000/26 => 192.168.1.64/26
1st Address: 192.168.1. 0100 0001/26 => 192.168.1.65/26
Last Address: 192.168.1. 0111 1110/26 => 192.168.1.126/26
Broadcast Address: 192.168.1 0111 1111/26 => 192.168.1.127/26
```

#### Router 1

Here, setup was done as follows:
```
Router>en
Router#conf t
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#inter
Router(config)#interface g
Router(config)#interface gigabitEthernet 0/0/1
Router(config-if)#ip address 192.168.1.65 255.255.255.192
Router(config-if)#no shutdown
Router(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0/1, changed state to up
```

Clearly, Router was assigned with IP Address of 192.168.65/26 which is the first IP Address in Subnet 2.

#### Router D

Here, setup was done as follows:
```
Router>en
Router#conf t
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#int
Router(config)#interface g
Router(config)#interface gigabitEthernet 0/0/0
Router(config-if)#ip address 192.168.1.126 255.255.255.192
Router(config-if)#no shutdown
Router(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0/0, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0, changed state to up
```

Clearly, Router was assigned with IP Address of 192.168.126/26 which is the last IP Address in Subnet 2.

Till here we've set both Subnets 1 and 2. However, still PC's in Subnet 1 can't reach to Router D and vice versa cause a route has not been established saying that if a ping comes for this subnet then go through this router.
So, we do that in the next step.



#### Setting Router D and Subnet 1 Routes

#### Router 1

Here, setup was done as follows:
```
Router>en
Router#conf t
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#ip route 192.168.1.64 255.255.255.192 192.168.1.126
```

#### Router D

Here, setup was done as follows:
```
Router>en
Router#conf t
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#ip route 192.168.1.0 255.255.255.192 192.168.1.65
```

Directly after doing this communication is now possible both ways.

To cross check if your pings are going across the intended routes you can use the `tracert` command as follows:

View ![[tracert_PC1_to_RouterD.png]]


Now, the same steps as above are done for Bottom Subnets i.e. subnet 3 and subnet 4.
Subnets to use are mentioned in *Calculations*.

