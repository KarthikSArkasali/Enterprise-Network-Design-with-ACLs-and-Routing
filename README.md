# 🌐 Enterprise Network Design with OSPF, ACL & Static Routing

# 🚀 Project Overview
The project aims to design and implement a scalable, high-availability enterprise network within a single building, structured floor-wise with a dedicated data center. The network will be built to ensure security, efficient communication, and optimal performance. This simulation, created using Cisco Packet Tracer, will model a real-world corporate setup consisting of multiple buildings (Building 1, Building 2), each housing various teams. Key networking concepts such as VLANs, OSPF routing, Access Control Lists (ACLs), and static routing will be integrated to enforce network segmentation and security.

VLANs will be used to isolate network traffic by team, while ACLs will restrict access to resources, ensuring that team members only have access to their designated servers. Team leaders will have broader access to all servers for administrative control. OSPF will be utilized to enable dynamic routing, optimizing network communication between different building segments and the centralized data center. The overall objective is to build a secure, efficient, and reliable network that mirrors the infrastructure of a corporate enterprise.

# 📌 Key Features

🔹 **Floor-wise Network Segmentation**
  - Each floor has a dedicated subnet to improve security and network management.
  - Reduces broadcast domain congestion for enhanced performance.
  
🔹 **Wireless Access Points (APs) for Seamless Connectivity**
  - Access Points deployed per floor for wireless connectivity.
  - Supports multiple SSIDs for different access levels (e.g., Staff, Guests).
  - WPA2 Enterprise security ensures encrypted communication.

🔹 **Dynamic & Static Routing for Optimized Traffic Flow**
  - OSPF (Open Shortest Path First) for efficient routing across all floors.
  - Static routes for data center-specific traffic to enhance control.

🔹 **Access Control & Security Implementation**
  - ACLs (Access Control Lists) to restrict unauthorized inter-floor communication.
  - Role-based access ensures Finance/Admin Servers are isolated from regular users.
  - Guest VLAN for Wireless APs to separate internal and guest traffic

# 🖥️ Network Topology

![Enterprise Project ACLs](https://github.com/user-attachments/assets/bdb1c7c6-5df0-4962-860b-ef3574dfe5de)

# 🛠️ Network Components

- **Switch:** WS-C296024TT (Better Processor, Better QOS, COs features) – 1
- **Access Point:** Access Point-PT (Acts as a stand-alone root unit in wireless networks) – 1
- **Router:** ISR4331/K9 (Full-stack Observability, Hybrid Cloud and Work) – 1
- **PC:** PC-PT – 1
- **Laptop:** Laptop-PT – 2
- **Ethernet Cable:** RJ-45 – Multiple


# ⚙️ Configuration Steps

1️⃣ OSPF Dynamic Routing

- Configured OSPF in area 0 to enable automatic route updates
- Defined network statements to advertise LAN and WAN routes

      router ospf 10
      network 192.168.1.0 0.0.0.255 area 0
      network 10.1.1.0 0.0.0.255 area 0

2️⃣ Static Routing

- Manually configured static routes for direct communication

      ip route 192.168.10.0 255.255.255.0 10.1.1.2
      ip route 192.168.20.0 255.255.255.0 10.1.1.3

3️⃣ ACL Security Implementation

- Restricted unauthorized access between network segments
- Allowed only necessary services

      access-list 100 deny ip 192.168.1.0 0.0.0.255 192.168.10.0 0.0.0.255
      access-list 100 permit ip any any
      interface Gig0/1
      ip access-group 100 in

