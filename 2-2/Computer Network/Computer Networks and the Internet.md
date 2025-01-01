#network
#### What Is the Internet?
1. A Nuts-and-Bolts Description (Basic hardware and software components)
	 >Internet : "network of network"
	- Networks
		- collections of devices, routers, links : managed by an organization
	- Hosts (= end systems)
		- connected together by a network of communication links and packet switches.
		- access the Internet through ISPs(Internet Service Providers)
	- Communitcation links
		- fiber, copper, radio, satellite
		- transmission rate : *bandwidth*
	- Packets
		- packages of information(data + header bytes)
		- Packets switches, most prominent types : routers, link-layer switches
	- Packet-switched networks ($\approx$ transportation )
	- *Protocols* are every where
		- control sending, receiving of messages
		- TCP/IP, HTTP (Web), etc..
	- Internet standards
		- RFC : Request for Comments
		- IETF : Internet Engineering Task Force

2. A Services Description (Networking infrastructure that provides services to appplications)
	- Distributed applications
		- on end systems - don't run in the packet switches in the network core
		- if you want to deliever another end systems, you follow socket interface.
	- Socket interface ($\approx$ send a letter)

3. What Is a Protocol
	- All activity in the Internet that involves two or more communicating remote entites is governed by a protocol. (running everywhere in the Internet)
	- *A <font color="#e36c09">protocol</font> defines the <font color="#e36c09">format</font> and the<font color="#e36c09"> order of messages sent and received</font> exchanged between two or more communicating entites, as well as the <font color="#e36c09">actions taken</font> on the transmission and/or receipt of a message or other event.*

#### The Network Edge
0. Host (Network Edge)
	- End systems
	- clients(desktops, laptop, etc) and servers(often in data centers, etc)
1. Access Networks 
	- The network that physically connects an end system to the first router on a path from the end systems to any other distant end system.
2. Home Access : DSL, Calbe + FTTH, 5G Fixed Wireless
	1. DSL (digital subscriber line)
		- use <font color="#e36c09">existing</font> telephone line to central office DSLAM
		- encoded at different frequencie (frequency-division multiplexing)
		- multiple transmission rates (asymmetric)
			- downstream : 24 ~ 52 Mbps
			- Upstream : 3.6 ~ 16 Mbps
	2. Cable Internet access
		- use existing cable television infrastructure.
		- HFC : hybrid fiber coax
			- astmmetric : up to 40Mbps - 1.2 Gbps downstream transmission rate, 30-100 Mbps upstream tranmission rate
		- Network of cable, fiber attaches homes to ISP router
			- home share access network to cable headend (share broadcast medium)
3. Enterprise (and the Home) : Ethernet and WiFi
	>mix of wired, wireless link tech, connecting a mix of swithces and routers 
	1. Ethernet
		- wired access at 100Mbps, 1Gbps, 10Gbps
		- User(twisted-pair copper wire) - Ethernet switch - Insitutional router - To Institution' s ISP 
	2. WiFi (WLANs)
		- wireless access points at 11, 54, 450 Mbps
4. Wireless access networks
	1. Wireless local area networks (WLANs)
		- typically within or around building (~100 ft)
	2. Wide-area cellular access networks
		- provided by mobile, cellulart network operator (10's km)
		- 10's Mbps
		- 4G/5G cellular networks
5. Data center networks
	>high-bandwidth links (10s to 100s Gbps) connect hundreds to thousands of servers together, and to Internet
6. Links : physical media
	- bit : propagates between transmitter/receiver pairs
	- physical link : what lies between transmitter & receiver
	- guided media : signals propagate in solid media : copper, fiber, coax
		- Twisted Pair
		- Coaxial cable
		- Fiber optic cable
	- unguided media : signals propagate freely, e.g., radio
		- Wireless radio (WLANs, wide-area, Bluetooth, terrestrial microwave, satellite)
Q. How to connect end systems to edge router
- residential access nets
- institutional access networks (school, company)
- mobile access networks (WiFi, 4G/5 G)

#### The Network Core
1. Packet Switching : hosts break application-layer messages into packets
	- Forwarding (switching)
		- Local Action
		- move arriving packets from router's input link to appropriate router output link 
	- Routing
		- Global Action
		- determin source-destination paths taken by packets
		- routing algorithms
	- store-and-forward packet switching
		- entire packet must arrive at router before it can be transmitted on next link
		- $d_{end-to-end} = N\frac{L}{R}$ L bits per packet, R bps, N links (N - 1 Routers)
		- Queuing Delays and Packet Loss
			- output buffer(queue) stores packets thea the router is about to send into that link. -> make dealy and loss (buffer space is full)
2. Circuit Switching
	- *reserved* for "call" between source and destination
	- dedicated resources : no sharing
	- Traditional telephone networks
	- FDM (Frequency Division Multiplexing)
		- optical, electromagnetic frequencies divided into (narrow) frequency bands
		- each call allocated its own band, can transmit at max rate of that narrow band
	- TDM (Time Division Multiplexing)
		- time divided int slots
		- each call allocated periodic slot(s), can transmit at maximum rate of (wider) frequency band (only) during its time slot(s)
3. Packet Switching Vs. Circuit Switching
	>Is packet switching a "slam dunk winner"?
	- great for "bursty" data - sometimes has data to send, but at other times not
		- resources sharing
		- simpler, no call set up
	- excessive congestion possible : packet delay and loss due to buffer overflow 
		- protocols needed for reliable data transfer, congestion control
	- circuit-like behavior with packet-switching
4. A Network of Networks
	- hosts connect to Internet via access ISPs (Internet Serviec Providers)
	- access ISPs in turn must be interconnected
		- cusomer ISPs pay their provider ISPs to obtain global Internet interconnectivity
		- so that any two hosts can send packets to each other
	- complex (evolution driven by economics, national policies)

![](https://i.imgur.com/OwJf250.png)

#### Performance : Loss, Delay, Throughput
0. Packet Loss : memory to hold queued packets fills up (high traffic)
	- lost packet may be retransmittem, or not at all (TCP/UDP)
1. Packet delay : four sources
	$$d_{nodal} = d_{proc} + d_{queue} + d_{trans} + d_{prop}$$
	 - $d_{proc}$ : nodal processing
		 - check bit errors (examine the packet's header)
		 - determine output link
		 - typically $\leq$ microsecs
	- $d_{queue}$ : queuing delay
		- time waiting at output link for transmission
		- depends on congestion level of router (traffic, # of packets)
		- microsecs ~ millisecs
	- $d_{trans}$ : transmission delay
		- times when all the bits in the packet arrived
		- L/R ; (L is packet length (bits), R : link transmission rate (bps))
		- microsecs ~ millisecs
	- $d_{prop}$ : propagation delay
		- propagate time : link -> route
		- d/s ; (d is length of physical link, s is propagation speed)
		- s $\approx$ speed of light ; $2*10^8 ~ 3*10^8$
		- millisecs
2. Packet queuing delay
	0. Supposed that 
		- a : average packet arrival rate
		- L : packet length (bits)
		- R : link bandwidth (bit transmission rate)
	$$\frac{L\times a}{R} : \frac{arrival\ rate\ of\ bits}{service\ rate\ of\ bits}$$
	![](https://i.imgur.com/pA1AXOd.png)
	1. ~ 0 : avg. queuing delay small
	2. -> 1 : avg. queuing delay large
	3. \> 1 : more "work" arriving is more than can be serviced - average delay infinite
	- pacekts arrive - bursts (delay large) / periodically (delay small)
3. End-to-End Delay (Sum of nodal delay in each routers)
	- <font color="#e36c09">traceroute</font> program
	- provides delay measurement from source to router $i$ with three special packets
4. Throughput
	> rate(bits/time unit) at which bits are being sent from sender to receiver
	- bottleneck link (minimum)
		- link on end-end path that constrain end-end throughput


  
#### Protocol layers, service models
- Layered Architecture
	- It allows us to discuss a well-defined, specific part of a large and complex system. (simplification)
	- Explicit structure allows identification, relationship of system's pieces
		- layered *reference model* for discussion
	- Modularization eases maintenance, updating of system
- Layered Internet protocol stack

| Internet protocol stack | explanation                                        | Ex                          |
| ----------------------- | -------------------------------------------------- | --------------------------- |
| Application             | supporting network applications                    | HTTP, IMAP, SMTP, DNS       |
| Transport               | process-process data transfer                      | TCP, UDP                    |
| Network                 | routing of datagrams from source to destination    | IP, routing protocols       |
| Link                    | data transfer between neighboring network elements | Ethernet, 802.11(WiFi), PPP |
| Physical                | bits "on the wire"                                 | twisted-pair copper wire                            |

- Encapsulation
	![](https://i.imgur.com/W4XwZbo.png)
	- routers and link-layer switches (both packet switches) are implement "some" layers 
	- Each layers takes the message(<font color="#e36c09">payload field</font>) and appends additional information(<font color="#e36c09">header field</font>)
		- Application : exchanges <font color="#e36c09">messages</font>
		- Transport : adding header($H_t$), create a <font color="#e36c09">transport-layer segment</font>
		- Network : adding header($H_n$, create a <font color="#e36c09">network-layer datagram</font>
		- Link : adding header($H_l$), create a <font color="#e36c09">link-layer frame</font>
	



#### History