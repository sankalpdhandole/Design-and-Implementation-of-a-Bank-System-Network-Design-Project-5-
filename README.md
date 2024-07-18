# Design-and-Implementation-of-a-Bank-System-Network-Design-Project-5-
### Project #5: Design and Implementation of a Bank System Network

#### Case Study and Requirements

1. **Network Design**:
   - Radeon Company Ltd. expanding banking and insurance services in Nairobi, Kenya.
   - Four-story building with departments on each floor.
   - Each department to have wired and wireless networks.
   - HTTP and Email servers required.
   - VLAN segmentation for each department.
   - Dynamic IP addressing using DHCP.
   - Inter-department communication required.

2. **Technologies Implemented**:

   - **Creating a Network Topology using Cisco Packet Tracer**.
   - **Hierarchical Network Design**.
   - **Connecting Networking Devices with Correct Cabling**.
   - **Configuring Basic Device Settings**.
   - **Creating VLANs and Assigning Ports VLAN Numbers**.
   - **Subnetting and IP Addressing**.
   - **Configuring Inter-VLAN Routing on Multilayer Switches (Switch Virtual Interface)**.
   - **Configuring Dedicated DHCP Server for Dynamic IP Allocation**.
   - **Configuring SSH for Secure Remote Access**.
   - **Configuring OSPF as the Routing Protocol**.
   - **Configuring Switchport Security or Port-Security on the Switches**.
   - **Configuring WLAN or Wireless Network (Cisco Access Point)**.
   - **Host Device Configurations**.
   - **Testing and Verifying Network Communication**.

#### Detailed Pointwise Implementation

1. **Network Topology Setup**:
   - Design a four-story building topology in Cisco Packet Tracer with routers, multilayer switches, PCs, and servers.

2. **Hierarchical Network Design**:
   - Divide network into core, distribution, and access layers:
     - Core: Router connecting to ISP and handling inter-VLAN routing.
     - Distribution: Multilayer switches for each floor.
     - Access: Access switches connecting PCs and wireless access points.

3. **Connecting Networking Devices with Correct Cabling**:
   - Use appropriate cables (fiber optic backbone, Ethernet within floors).

4. **Configuring Basic Device Settings**:
   - Set hostnames, console and enable passwords, banner messages, disable domain IP lookup, and encrypt passwords.

5. **Creating VLANs and Assigning Ports VLAN Numbers**:
   - Assign VLANs for each department:
     - Floor 1: VLAN 10 (Admin), VLAN 20 (Finance)
     - Floor 2: VLAN 30 (HR), VLAN 40 (Business)
     - Floor 3: VLAN 50 (Engineering), VLAN 60 (Art/Design)
     - Floor 4: VLAN 70 (IT), VLAN 80 (Server Room)

6. **Subnetting and IP Addressing**:
   - Base network: 192.168.10.0/24
   - Subnet each VLAN based on department size:
     - Example: VLAN 10 (Admin) subnet: 192.168.10.0/26
       - Subnet mask: 255.255.255.192
       - Usable IP range: 192.168.10.1 - 192.168.10.62
       - Broadcast address: 192.168.10.63

7. **Configuring Inter-VLAN Routing on Multilayer Switches (Switch Virtual Interface)**:
   - Configure SVIs on multilayer switches for inter-VLAN routing:
     ```bash
     Switch(config)# interface vlan 10
     Switch(config-if)# ip address 192.168.10.1 255.255.255.192
     ```

8. **Configuring Dedicated DHCP Server for Dynamic IP Allocation**:
   - Use a dedicated server for DHCP:
     ```bash
     DHCP(config)# ip dhcp pool VLAN10
     DHCP(dhcp-config)# network 192.168.10.0 255.255.255.192
     DHCP(dhcp-config)# default-router 192.168.10.1
     ```

9. **Configuring SSH for Secure Remote Access**:
   - Generate SSH keys on routers and switches:
     ```bash
     Router(config)# crypto key generate rsa
     Switch(config)# crypto key generate rsa
     ```
   - Configure SSH access:
     ```bash
     Router(config)# line vty 0 4
     Router(config-line)# transport input ssh
     Router(config-line)# login local
     ```

10. **Configuring OSPF as the Routing Protocol**:
    - Enable OSPF on the router to advertise routes:
      ```bash
      Router(config)# router ospf 1
      Router(config-router)# network 192.168.10.0 0.0.0.255 area 0
      ```

11. **Configuring Switchport Security or Port-Security on the Switches**:
    - Configure switchport security with sticky MAC addresses:
      ```bash
      Switch(config)# interface fastEthernet 0/1
      Switch(config-if)# switchport mode access
      Switch(config-if)# switchport port-security
      Switch(config-if)# switchport port-security mac-address sticky
      ```

12. **Configuring WLAN or Wireless Network (Cisco Access Point)**:
    - Set up wireless networks for each department:
      ```bash
      AccessPoint> enable
      AccessPoint# configure terminal
      AccessPoint(config)# interface dot11Radio 0
      AccessPoint(config-if)# ssid Admin_WLAN
      AccessPoint(config-if-ssid)# vlan 10
      ```

13. **Host Device Configurations**:
    - Configure PCs and servers with appropriate IP addresses based on VLAN subnetting.

14. **Testing and Verifying Network Communication**:
    - Use ping, traceroute, and application tests to verify connectivity and functionality across departments and VLANs.

By following these steps, you will successfully design and implement a secure and scalable network infrastructure for Radeon Company Ltd. in Nairobi, Kenya, meeting all specified requirements for banking and insurance operations.
