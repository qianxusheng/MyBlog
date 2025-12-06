+++
title = "Application of Network"
date = "2025-12-04"
author = "Max"
tags = ["network"]
description = "aa"
+++

Application layer
Application communication pattern: peer to peer or client-server
Application is software with two or more processes running in end systems that send messages over a network to accomplish some goal
Network applications use `socket` interface to access transport layer services
Application layer protocols are used by applications to communicate with each other. Below that, it is two hosts are communicating.

HTTP(Web)
HTTP -> HTTP1.1 -> HTTP/2 -> HTTP/3
HTTP request message: request line(method, URL, protocol version); request headers; request body(optional data)
HTTP response message: status line(protocol version, status code, status phrase); response header; body
HTTP performance: RTT(round trip time)
Web caches(proxy servers): deployed by ISPs
CDN: plays a imporant role in moving content closer to users in Web and streaming video services
MPEG-DASH: Dynamic Adaptive Streaming over HTTP; Client-side buffering and playout delay, and videos are divided into multiple chunks and encoded at different rates, so if poor network, CDN can provide low rates(poor quality) to maintain smooth playback without stalling.

SMTP(E-mail): user agents <-> mail servers
VoIP: Call on internet 
SIP: session initiation protocol
RTP: real-time protocol
RTCP: real-time control protocol

DNS: 
IP address <-> hostnames; 
13 root name servers; 
DNS Hierarchical: root -> top level domain -> authoritative

Summary:
1. application(chrome, safari), they both use HTTP!
2. application layer protocol: HTTP
3. Application is a software with two or more processes running in the end systems to send message over a network to accomplish some goal.
4. socket API.

--- 

transport layer(host to host)
multiplexing/demultiplexing in transport layer: receiver will demultiplex message up to different applications via socket. It is based on port number. UDP uses destination port number only while TCP uses 4-tuple: source and destination IP addresses, and port numbers.
reliable data transfer: sender sends data and receiver waits for data.
the goal of transport layer: build reliable channel(protocol) over unreliable channel(in reality).

UDP basis(unordered, unreliable):
UDP datagram format: source and dest port, header length, checksum for error detection, and pay load.
UDP error detection: 16bits checksum.

TCP(segments, in-order byte stream) basis:
Stop and wait:if Ack, move to next packet; if nAck, resend.
Corrupted Ack problem: add sequence number. If sequence number is not correct, receiver could discard duplicate packet safely.
Loss: set timeout.
Reliable data transfer mechanism: checksum, ACKs/NAKs, Retransimission, sequence number, timeouts.
It works but not efficient.
Pipelined reliable data transfer: just like water, occupied entire pipe.
sliding window: sender buffer sent but not-yet-acknowledged packets. The window also contains not-yet-sent packets, and if window is filled with not-yet-acknowledged packets, the sender cannot send any packets.

Go-Back-N: when timeout occurs, sender will resend all not-yet-acknowledged packets(up to N).
selective repeat(more like real world):receiver individually acknowledges each correctly received packet and buffer out-of-order packets.

tcp segement structure: source and dest port, checksum, sequence number, acknowledgment, advertised window, header length

how to set timeout: too long: slow reaction to loss; too short: waste bandwidth. Should be close to RTT.

how to estimate RTT? dynamic RTT estimation: estimateRTT = (1 - a)estimateRTT + a * sampleRTT; estimateRTT is a safety margin, sampleRTT is the current measurement(the duration that sender receives ACK)

fast retransmit: TCP will retransmit a segment upon receiving 3 duplicates ACKs for that segment.

TCP 3-way handshake: establish connection.

advanced TCP: flow control and congestion control
flow control: advertised window(RWND) tells sender how many bytes it can accept.
congestion control: 
congestion control: stay left of cliff; 
congestion avoidance: stay around or left of knee. 
Congestion window: CWND << RWND; sending rate approximates window/RTT.
Basic idea: if no congestion, increases sending rate; if timeout or 3 duplicates ACKs, decrease sending rate.
increasing CWND:
Slow start: slow start for safety but ramp up quickly for efficiency(slow start threshold).
Congestion avoidance: move to additive increase.
reducing CWND:
timeout: cut CWND to 1 MSS(max segment size), go to slow start
3 duplicate ACKs: cut CWND in half, go to congestion avoidance

Sumary:
1. contorl.
2. reliability.

---

network layer(routing, best efforts host-to-host delivery)
1. path-selection algorithms -> forwarding table
2. IP protocol
3. ICMP protocol

IP packets: TTL, IP version, checksum, header length, upper layer protocol(TCP or UDP), source and dest IP address

data plane: what is the output port for the upcoming datagram at current router.
control plane: how datagram routes among routers from src to dest.
1.traditional approach: implemented on routers.
2.software-defined network: implemented in remote servers/controllers.

router architecture:
1.control plane: software, 
2.data plane: hardware
physical layer -> datalink -> forwarding queueing -> switching fabric & routing processor -> queueing -> datalink -> physical layer

routers:
1.backbone routers
2.enterprise routers
3.access routers

forwarding tables: based on IP dest address, use longest prefix match to find the out link interface.
switching fabric: transfer packet from input link to appropriate outputlink
managing queueing: too much buffering will increase delay
1.which packet to drop when buffer is full？drop tail; priority
2.which packet to send next from the queue？FIFO;priority scheduling

network neutrality

subnets: IP addresses: subnets part(high common bits) and host part(low order bits).
subnet mask: 223.1.1/24.
CIDR: Classless InterDomain Routing. address format: a.b.c.d/x, where x is the subnet portion of address.
How does host get IP address?
1.hardcoded by system admin(static IP address - e.g. server)
2.DHCP: dynamic host configuration protocol
DHCP(on top of UDP):
goal: when host joins server, it automatically assigned with a IP address.
1.host broadcasts DHCP discover msg.
2.DHCP server offers the IP address.
3.host request: I would use this IP address.
4.DHCP: ok, you got this address.
NAT: network address translation, implemented in NAT router
all devices in local private network just share one public IPv4 address

transition from IPv4 to IPv6: long time for deployment
tunneling: IPv6 datagram carried as payload in IPv4 datagram.
middleboxes: NAT, firewalls, load balances, caches(something taht works on data path from src host to dest host but other than router)

routing algorithms classification: 1.dynamic/static; 2.global/local
1. link state algorithm(dijkstra, static, global)
2. distance vector algorithm(bellman-ford, dynamic, static)

aggregate routers into regions known as “autonomous
systems” (AS), AS is a bunch of routers.
interconnected ASes(real world):
intra-AS(OSFP, based on LS): routing among routers within same AS.
inter-AS(BGP, based on DV): inter-domain routing 

BGP: achieving policy via advertisements 
- policy to enforce: if x does not want to route from B to C via x, so x will not advertise to B a route to C

ICMP: internet control message protocol(ping, traceroute)

Service Level Agreements: legal agreement between customer and network operator, defines KPI(key performance indicators)

Verizon SLAs example:
- mean time to repair
- availability
- Jitter
- latency
- packet loss

How network operators meet these SLAs?
- routing alogrithm: policies
- buffer management: congestion detection
- queue scheduling: prioritization
- fault detection
- virtualization: QoS(quality of service) differentiation and traffic separation

virtual network: like virtual machine sharing the same host resource.

the advantanges of Virtual network:
- cost
- security
- flexibility

three types of VN technology
- VLAN 
- MPLS(multi-protocol label switching)
- SDN (data center)

MPLS: different QoS to different service classes
LSR: label swithing router
FEC: forwarding equivalence class(a subnet of packets that are treated in the same way by LSR)
LSP: label-switched path
How it works?
MPLS header encoded with FEC is inserted to a packet before packet is forwareded. Inner label tells you who you are, outer label tells you where to go.

data center ->(SDN as control plane instead of implementing control plane inside the every single routers)

network management:
- fault 
- configuration
- accouting
- performance
- security

SDN: 
- control plane: software(network apps + network OS)
- data plane: hardware(switches)
generalized forwarding: match + action
OpenFlow: controller-to-switch messages

network management components:
SNMP（simple network management protocol
CLI: command line interface
NETCONFIG/YANG:

Summary:
1. routing(BGP, OSPF).
2. Virtual network(MPLS, provide different QoS).
3. data center network(network management, SDN).
4. SLAs(network KPIs).

---


link layer(forwarding): node-link-node
links: wired, wireless
hosts, routers: nodes
frame: encapsulates datagram
analogy: you may take plane, train, taxi to your destination.
services:
- framing
- reliable delivery(error control, ARQ): seldom used on wired links, wireless links have high error rate
- half-duplex/full-duplex
- error detection
- error correction
- flow control

host link-layer implementation:
NIC(network interface card): a chip
error control: 
1. error detection + automatic repeat request(ARQ)
2. forward error correction(FEC)
error control coding(add Redundancy): parity checking, checksum

multiple access channal(MAC) protocol, three broad classes:
- partitioning(TDMA, FDMA): inactive channel, waste
- random access(ALOHA, slotted ALOHA): allow collisions
- taking turns(polling)

slotted ALOHA:
assumptions: same size frames, time divided into equal size slots, and nodes are synchronized
if collision, retransmit frame with probability p(randomization).

CSMA(carrier sense multiple access):
if channel sensed idle, transmit.
if channel sensed busy, defer transimition.

CSMA/CD(generic idea): CSMA withcollision detection

Ethernet CSMA/CD algorithm: implementation, binary exponential backoff

taking turns protocols:
1.polling(bluetooth): centralized controller invites other nodes to transmit
2.token passing(token ring): pass control token message to the next one

MAC address
ARP(address resolution protocol): find MAC address for certain IP
1.addressing within subnet: broadcast and target MAC replies
2.routing to another subnet: link layer <-> network layer

Ethernet frame: MAC src and dest, and data and CRC.
Ethernet(wired LAN) bus -> switched: Ethernet protocol, switch, MAC address
Switch: forwarding, link layer device, self-learning(broadcast)
MST: Sometimes we add addtional link to provide redundant connections to prevent potential problems, this loop could lead to infinite loop(no TTL in frame), so we need use MST to prevent this.
institutional netowrk: switched LANs, Ethernet, MST

Summary:
1. node, Link.
2. error detection, correction; multiple access(sharing a broadcast channel); link layer addressing(ARP)
3. institutional network: MST, Switched LANs, Ethernet
4. ethernet frame

Physical layer
- wire
- wireless
- optical


other topics:
network performance
- delay
- loss
- throughput

data center network

optical link layer

wireless network

security

concepts:
1. CDN(content delivery netowrk): caching for speed and replica for backup.
2. data plane: forwarding, fast, based on hardware.
3. control plane: routing, slow, based on software.
4. AS: autonomous systems. Tier 1 AS: global ISP -> Tier 2 AS: regional ISP -> Tier 3 AS: local ISP(like Pitt)
5. Delay Jitter: variation in delay. Jitter buffer.
6. Web pages: base HTML file and several referenced objects. Objects are identified by URL(unique resource locater).