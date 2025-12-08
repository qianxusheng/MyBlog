HTTP evolution
Web caches(proxy servers)
CDN
MPEG-DASH: Dynamic Adaptive Streaming over HTTP
VoIP: call on internet
DNS
Transport layer multiplexing/demultiplexing: based on port number, reuse single IP address for multi-application
UDP error detection: checksum
UDP datagram
TCP evolution(reliable): ACK->sequence number->timeout->sliding window->selective repeat(allow disordered packets) 
TCP segments
TCP handshakes(connection setup and finish)
how to set up timeout for TCP: RTT estimation(sampleRTT + estimateRTT)
TCP flow control:RWND
TCP congestion control:CWND, how to increase CWND, how to reduce CWND
data plane(hardware) and control plane(software)
routers: routing
switches: forwarding. queueing management.
subnets:
subnet mask: 223.1.1/24.
CIDR
how to get IP address: DHCP
NAT: share IPv4 address 
transition from IPv4->IPv6: tunneling, unique routers
middleboxes
routing algorithms: dijskstra, bellman-ford
autonomous systems: a bunch of routers
Interconnected ASes: intra-AS(OSFP), inter-AS(BGP)
BGP
OSFP
Service level agreements: verizon SLAs, network KPIs
virtual networks: VLAN, MPLS, SDN
MPLS: label switching(different QoS)
Data center
Network management
SDN: network OS and network apps and switches
NIC: chip
Error control
MAC protocol
CSMA/CD
Ethernet
MAC address
ARP: address resolution protocol
VLAN: three ways
bridged VLANs: IEEE 802.1Q
switch flooding: MST
switch self-learning: