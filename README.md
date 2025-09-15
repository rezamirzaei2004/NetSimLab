Network Project – Multi-Branch Organization (Packet Tracer)
Overview

This is a networking project I built in Cisco Packet Tracer for my course.
The idea was to design a multi-branch network with VLANs, DHCP, WiFi, and a Server Farm, all connected through a central router.

Network Topology (per branch)

Each branch includes:

4 departmental switches (Security, IT, Financial, Archive) – each with 3 PCs

1 Server Farm switch with 3 servers (File, DNS, Web)

1 internal router (DHCP enabled)

1 WiFi network (~250 users)

Connection to a central 2911 router

IP Addressing
VLANs (/26 each)

Security → 192.168.1.0/26

IT → 192.168.1.64/26

Financial → 192.168.1.128/26

Archive → 192.168.1.192/26

WiFi

192.168.5.0/24

Gateway: 192.168.5.1

DHCP: 192.168.5.2 - 192.168.5.254

Server Farm

192.168.2.0/23

Gateway: 192.168.2.1

File Server → 192.168.2.2

DNS Server → 192.168.2.3

Web Server → 192.168.2.4

Summarization (per branch)

Branch 1 → 192.168.0.0/20

Branch 2 → 192.168.16.0/20

Branch 3 → 192.168.32.0/20

Branch 4 → 192.168.48.0/20

DHCP Example (on router)
ip dhcp pool SECURITY
 network 192.168.1.0 255.255.255.192
 default-router 192.168.1.1
 dns-server 192.168.2.3

ip dhcp pool WIFI
 network 192.168.5.0 255.255.255.0
 default-router 192.168.5.1
 dns-server 192.168.2.3

Router-on-a-stick (sample config)
interface fa0/0.10
 encapsulation dot1Q 10
 ip address 192.168.1.1 255.255.255.192

interface fa0/0.50
 encapsulation dot1Q 50
 ip address 192.168.5.1 255.255.255.0

interface fa0/0.60
 encapsulation dot1Q 60
 ip address 192.168.2.1 255.255.254.0

VLANs on Switch
vlan 10
 name Security
vlan 20
 name IT
vlan 30
 name Financial
vlan 40
 name Archive
vlan 50
 name WiFi
vlan 60
 name ServerFarm

interface range fa0/1-3
 switchport mode access
 switchport access vlan 10

interface fa0/24
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50,60

Key Points

VLANs separate the departments

Router handles DHCP and inter-VLAN routing

WiFi supports up to 250 clients

Server Farm hosts core services (DNS, Web, File)

Each branch has its own summarized block

Conclusion

This project shows how to design a branch-based enterprise network with VLANs, DHCP, WiFi, and servers.
It’s scalable, organized, and can be easily expanded if needed.
