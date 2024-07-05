### Departmental Network Design using Cisco Packet Tracer

# Network Design for BAMO Company's New Branch in Kakamega

## Introduction
BAMO Company, a fast-growing entity in Kenya with over 2 million global customers, specializes in the buying and selling of sugar. The company is expanding its operations by establishing a new branch near the city of Kakamega. As part of this expansion, the company requires a robust network infrastructure designed specifically for the new branch. The network will operate independently from the headquarters (HQ) network and needs to accommodate various departmental requirements. This report outlines the design and implementation plan for the new branch network.

## Network Requirements
The network design for the Bonalbo branch has the following requirements:

1. Utilization of one router and one switch (both CISCO products).
2. Segmentation into three departments:
    - Admin/IT
    - Finance/HR
    - Customer Service/Reception
3. Each department must be on a different VLAN.
4. Provision of a wireless network for each department.
5. Host devices must obtain IPv4 addresses automatically.
6. Devices across all departments must be able to communicate with each other.


## Network Design Overview
Given the requirements, the network design incorporates VLANs for logical segmentation and efficient management. The Internet Service Provider (ISP) has allocated a base network of 192.168.1.0/24 for this project.

<img src="https://github.com/Munialo99/Cisco-Packet-Tracer/blob/main/Departmental%20Network/Departmental%20Network%20Design.png">

### Subnetting
To accommodate the network design, the following subnetting scheme is used:

    Subnet Mask
  
      255.255.255.192 (/26)

#### VLAN Allocation and Subnet IDs:
1. Admin/IT Department

    - LAN ID: 20
    - Network ID: 192.168.1.0/26
    - IP Range: 192.168.1.1 - 192.168.1.62
    - Subnet Mask: 255.255.255.192

2. Finance/HR Department

    - VLAN ID: 10
    - Network ID: 192.168.1.64/26
    - IP Range: 192.168.1.65 - 192.168.1.126
    - Subnet Mask: 255.255.255.192

3. Customer Service/Reception

    - VLAN ID: 30
    - Network ID: 192.168.1.128/26
    - IP Range: 192.168.1.129 - 192.168.1.190
    - Subnet Mask: 255.255.255.192

## Network Components and Configuration
### Hardware:
  - Router: CISCO 1941
  - Switch: CISCO Catalyst 2960
  - Access Points: 3 (one for each department)
  - End Devices: Desktop PCs, printers, laptops, tablets, smartphones

### Configuration Steps:

1. Router Configuration:
    - Set up inter-VLAN routing to enable communication between different VLANs.
    - Configure DHCP to automatically assign IPv4 addresses to host devices.

2. Switch Configuration:
    - Create and assign VLANs.
    - Configure trunk ports to carry multiple VLAN traffic between the switch and the router.
    - Set up access ports for devices in each department.

4. Access Points Configuration:
    - Configure WPA2-PSK authentication for secure wireless connections.
    - Assign appropriate SSIDs and VLANs for each department.

5. Device Configuration:
    - Connect devices to the appropriate access points and ensure they obtain IP addresses automatically via DHCP.

## Detailed VLAN Configuration

### Router Configuration (CISCO 1941):

    interface GigabitEthernet0/0
     no shutdown
     ip address 192.168.1.1 255.255.255.0
    
    interface GigabitEthernet0/0.10
     encapsulation dot1Q 10
     ip address 192.168.1.65 255.255.255.192
    
    interface GigabitEthernet0/0.20
     encapsulation dot1Q 20
     ip address 192.168.1.1 255.255.255.192
    
    interface GigabitEthernet0/0.30
     encapsulation dot1Q 30
     ip address 192.168.1.129 255.255.255.192
    
    ip dhcp pool Admin_IT
     network 192.168.1.0 255.255.255.192
     default-router 192.168.1.1
    
    ip dhcp pool Finance_HR
     network 192.168.1.64 255.255.255.192
     default-router 192.168.1.65
    
    ip dhcp pool Customer_Service
     network 192.168.1.128 255.255.255.192
     default-router 192.168.1.129

### Switch Configuration (CISCO Catalyst 2960):

    vlan 10
     name Finance_HR
    vlan 20
     name Admin_IT
    vlan 30
     name Customer_Service
    
    interface GigabitEthernet0/1
     switchport mode trunk
    
    interface GigabitEthernet0/2
     switchport mode access
     switchport access vlan 10
    
    interface GigabitEthernet0/3
     switchport mode access
     switchport access vlan 20
    
    interface GigabitEthernet0/4
     switchport mode access
     switchport access vlan 30


## Reasons for Configuration Choices

### Trunk Port Configuration
We configure the switch mode to trunk for the interface connecting the switch to the router to allow the router to receive and route traffic for multiple VLANs. Trunk ports carry traffic from multiple VLANs, making it possible for devices in different VLANs to communicate through a single physical link. This is essential for inter-VLAN routing and ensures efficient use of network resources.

### Encapsulation dot1Q
The encapsulation dot1Q command is used on the router's subinterfaces to identify which VLAN the traffic belongs to. IEEE 802.1Q is a standard for VLAN tagging on Ethernet frames. This command ensures that the router can correctly route traffic between VLANs by recognizing the VLAN tags added by the switch. Without this encapsulation, the router would not be able to distinguish between traffic from different VLANs.

## Security Considerations
  - WPA2-PSK Authentication: Ensures that wireless networks are secure.
  - VLAN Segmentation: Provides logical separation of departments, enhancing security and reducing broadcast domains.
  - Inter-VLAN Routing: Facilitates communication between departments while maintaining isolation.

## Testing and Validation
  - Verify that all devices can obtain IP addresses automatically.
  - Ensure inter-department communication is functional.
  - Test wireless connectivity and security settings.
  - Conduct network performance tests to ensure reliability and efficiency.

## Conclusion
The proposed network design for BAMO Company's new branch in Bonalbo meets all specified requirements, ensuring a robust and secure infrastructure that supports seamless communication across departments. The use of VLANs, inter-VLAN routing, and secure wireless access points guarantees efficient network management and security.

#### Useful Tool
<a href="https://www.calculator.net/ip-subnet-calculator.html">IP Calculator</a>















