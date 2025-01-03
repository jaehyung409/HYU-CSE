#### Introduction and Transprot-layer Services
- A transport-layer protocol provides for **logical communications** between application processes running on different hosts.
- The transport layer converts the application-layer messages it receives from a sending application process into transport-layer packets, known as transport-layer **segments**.
#### Multiplexing and Demultiplexing
- Based on segment, datagrm header field values, happen at all layers![](https://i.imgur.com/Ev6VGeK.png)
- Multiplexing 
	- handle data from multiple sockets, add transport header (later used for demultiplexing)
- Demultiplexing
	- use header info(<font color="#e36c09">IP addresses & port numbers</font>) to deliver received segments to correct socket
	- In UDP
		- Sending host : datagram send into UDP socket 
			- dest IP, dest port number
		- Receiveing host : UDP segment
			- checks dest port number
			- directs UDP segment to sokect with that port number
		- same dest, port \# (but different src, port) -> dircet to same socket
	- In TCP
		- identified by 4-tuple (reciver uses all four values to direct segment to socket)
			- source IP address
			- source port number
			- destination IP address
			- destination port number
		- server may support many simultaneous TCP sockets
#### Connectionless Transport: UDP
- Ref : [RFC 768: User Datagram Protocol](https://www.rfc-editor.org/rfc/rfc768)
- UDP : User Datagram Protocol ("no frills" protocol, num : 17)
	- Aside from the multiplexing/demultiplexing function and some light error checking, it adds nothing to IP.
	- ***connectionless*** : No handshaking (no RTT incurred)
	- No congestion control
	- maybe ... lost, delivered out-of-order to app.
	- best effort service : "send and hope for the best"
- UDP use
	- streaming multimedia apps (loss tolerant, rate sensitive)
	- DNS
	- SNMP
	- HTTP/3 (build additional functionality on top of UDP in application layer)
- UDP sender/receiver actions
	- Sender : 
		- is passed an application layer message
		- determines UDP segment header filed values and creates UDP segment
		- passes segment to IP
	- Receiver : 
		- receives segment from IP
		- checks UDP checksum header value
		- extracts application layer message
		- demultiplexes message up to application via socket
- UDP segment format

| 32bits (each header ; two bytes) |          <          | Field  |
|:--------------------------------:|:-------------------:|:------ |
|         Sourece Port \#          | Destination Port \# | Header |
|    Length (header(8) + data)     |      Checksum       | ^      |
|    Application data (message)    |          <          | Data   |
- UDP Checksum
	- Goal : Detect errors in transmitted segment (Not perfectly : bit flips...)
	- Overflow -> wrapped around
	- 1's complement
	- No errors, clearly the sum at the receiver will be 1111111111111111.
	- The entire UDP segment, except the checksum filed itself, and the IP sender and receive address fields
#### Principles of Reliable Data Transfer
- using  [[Final State Machine]] 
- Key elements : <font color="#e5b9b7">check-sum, sequence numbers, timers, ACK and NAK</font>![](https://i.imgur.com/BFpxL86.png)
1. reliable data transfer protocol(rdt) <-> unreliable data transfer(udt)
	- Complexity of reliable data transfer protocol will depend on characteristics of unreliable channel (lose, corrupt, reorder data)
	- Sender, Receiver don't know the "state" of each other 
		- only communticate with message
	- interface of RDT![](https://i.imgur.com/c9qzOgc.png)
2. RDT 1.0 : reliable transfer over a reliable channel![](https://i.imgur.com/0jAYPZo.png)
3. RDT 2.0 : channel with bit errors - ACK, NAK (stop and wait)
	- ARQ (Automatic Repeat reQuest) protocols 
		- *Error detection - Receiver feedback - Retransmission*
	- <font color="#e36c09">acknowledgement (ACKs)</font> : receiver explicitly tells sender than pkt received OK
	- <font color="#e36c09">negative acknowledgements (NAKs)</font> : receiver explicitly tells sender that pkt had errors
	- sender <font color="#e36c09">retransmits</font> pkt on receipt of NAK (<font color="#e36c09">stop and wait</font>)
		- sender sends on pkt, then waits for receiver response
		- sender will not send a new piece of data until it is sure that the receiver has correctly received the current packet.
	- ![](https://i.imgur.com/TRBSFm7.png)
	- rdt 2.0 has a fatal flaw!
		- ACK/NAK packet could be corrupted 
			- add <font color="#92cddc">sequence number</font> to each packet
	- RDT 2.1 (using sequence number 0, 1 : alternative using to detect duplicate)
	- RDT 2.1 : Sender![](https://i.imgur.com/fgp2bN2.png)
	- RDT 2.1 : Receiver![](https://i.imgur.com/WfZFh3Z.png)
	- RDT 2.2 : NAK-free protocol
		- same functionality as rdt2.1, using ACKs only
		- instead of NAK, receiver sends ACK for last pkt received OK
			- receiver must *explicitly* include seq \# of pkt being ACKed
		- duplicate ACK at sender results in the same action as NAK : 
			- retransmit current pkt
		- TCP uses this approach to be NAK-free
		- Sender![](https://i.imgur.com/fo5NRES.png)
		- Receiver![](https://i.imgur.com/UmocRF5.png)
4. RDT 3.0 : channels with errors and loss
	- sender waits "reasonable" amount of time for ACK (use <font color="#de7802">timer</font>)
	- Sender![](https://i.imgur.com/5EXf5rc.png)
5. Peformance Problem ('Cause stop-and-wait protocol) -> <font color="#e5b9b7">Pipelining</font>
	- Performance : $$U_{sender}=\frac{L/R}{RTT+L/R}\qquad, d_{trans}=L/R$$
	- Pipelining : sender allows multiple, "in-flight", yet-to-be-acknowledged packets![](https://i.imgur.com/gpym2SC.png)
		- range of sequence numbers must be increased
		- buffering at sender and/or receiver
	- ***Go-Back-N***
		- Sender (uses only a single timer, which can be thought of as a timer for the oldest transmitted but not yet ack packet)![](https://i.imgur.com/F1Xwdfy.png)![](https://i.imgur.com/vMNSxZh.png)
		- **cumulative ACK : ACK(n)** : ACKs all packets up to, including seq \# n
			- on receiving ACK(n) : move window forward to begin at n+1
		- *timeout(n)* : retransmit packet n and all higher seq \# packets in window
		- Receiver![](https://i.imgur.com/2RdCFxM.png)![](https://i.imgur.com/LpO31Vy.png)
		- ACK-only : always send ACK for correctly-received packet so far, with highest *in-order* seq \#
			- may generate duplicate ACKs
			- need only remember <font color="#b7dde8">rcv_base</font>
		- on receipt of out-of-order packet
			- can disacrd (don't buffer) or buffer : an implementation decision (*no receiver buffering!*)
			- re-ACK pkt with highest in-order seq \#
		- Protocol allows the sender to potentially "fill the pipeline"
			- As the probability of channel errors increase, the pipeline can become filled with these unnecessary retransmission
	- ***Selective repeat***
		- avoid unnecessary retransmissions by having the sender retransmit only those packts that it suspects were received in error at the receiver
		- **individually ACK**
		- Out-of-order packets are buffered until any missing packets(that is, packets with lower sequence numbers) are received, at which point a batch of packets can be delivered in order to the upper layer.
		- ![](https://i.imgur.com/yu4TSfE.png)
		- ![](https://i.imgur.com/6iTuhF2.png)
		- window size must be less than or equal to half the size of the sequence number space
#### Connection-oriented Transport: TCP
- RFCs : 793, 1122, 2018, 5681, 7323
- TCP Connection, overview
	- reliable, in-order-byte steam
	- connection-oriented ("three-way handshake")
	- full-duplex service
		- MSS : maximum segment size (typically 1460)
	- point-to-point 
	- cumulative ACKs, pipelining, flow controlled
- TCP segment structure![](https://i.imgur.com/PoyFasE.png)
	- Sequenec Numbers : byte stream "number" of first byte in segment's data
	- ACK Numbers : seq \# of next byte expected from other side, cumulative ACK
		- TCP only acknowleges bytes up to the first missing byte in the stream
	- ![|400](https://i.imgur.com/eqZkIBQ.png)
- TCP round trip time, timeout 
	- **e**xponential **w**eighted **m**oving **a**verage (EWMA)$$\begin{align}EstimatedRTT=(1-\alpha)*EstimatedRTT + \alpha*SampleRTT\\\text{typical value : }\alpha=0.125\end{align}$$
	- timeout interval : **EstimatedRTT** plus "safety margin"$$\begin{flalign}&TimeoutInterval=EstimatedRTT+4*DevRTT\\&\text{DevRTT : EWMA of SampleRTT deviation from EstimatedRTT}\\&DevRTT = (1-\beta)*DevRTT +\beta*|SampleRTT-EstimatedRTT|\\&\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\text{typical value : }\beta=0.25\end{flalign}$$
- TCP reliable data transfer
	- Sender![](https://i.imgur.com/8PFs8h9.png)
	- Receiver![](https://i.imgur.com/7Ic1o5s.png)
	- TCP fast retransmit
		- if sender receives "triple duplicate ACKs", resend unACKed sement with smallest seq \# (don't wait for timeout)
- TCP flow control
	- receiver controls sender, so sender won't overflow receiver's buffer by transmitting too much, too fast
	- TCP receiver "advertises" free buffer space in **rwnd** field in TCP header![|300](https://i.imgur.com/EfGfnvs.png)
		- **RcvBuffer** size set via socket options (typical default is 4096 bytes)
			- many operating systems auto-adjust
		- guarantees receive buffer will not overflow
	- before exchanging data, <font color="#d99694">"handshake"</font>
		- agree to establish connection
		- agree on connection parameters (e.g., starting seq \#s)
		- Why not 2-way ?
			- retransmitted messages or loss messages
				- can make duplicate message or connection
			- can't "see" other side (reliability $\downarrow$)
			- message reordering ... and so on
	- TCP 3-way handshake![](https://i.imgur.com/m0rH5vg.png)
	- closing a TCP connection 
		- client, server each close their side of connection
			- send TCP segment with FIN bit = 1
		- respond to received FIN with ACK
			- on receiving FIN, ACK can be combined with own FIN (FIN/ACK)
		- simultaneous FIN exchanges can be handled
#### Principles of Congestion Control
- Congestion 
	- informally : "too many sources sending too much data too fast for <font color="#d99694">network</font> to handle"
	- manifestations
		- long delays (queuing in router buffers)
		- packet loss (buffer overflow at routers)
- Scenario 1, Two senders, a Router with Infinite Buffers![](https://i.imgur.com/k4QfWCK.png)
	- large queuing delays are experienced as the packet-arrival rate nears the link capacity.
- Scenario 2,  same as 1, but a Router with finite Buffers 
	- $\lambda_{in} = \lambda_{out}$
	- $\lambda_{in}^{'} \geq\lambda_{in}$, origin data + *retransmitted data*
	1. perfect knowledge (sender sends only when router buffers availiable ; no retransmitted data) : Same as scenario 1.
	2. *some* perfect knowledge (sender knows when packet has been dropped ; only resends if packet known to be lost)
		![|400](https://i.imgur.com/QhJj46Z.png)
	3. Realistic : <font color="#d99694">un-needed duplicates</font>
		![|400](https://i.imgur.com/t8E0XGg.png)
	- "costs" of congestion
		- more work (retransmission) for given receiver throughput
		- unneeded retransmissions : link carries multiple copies of a packet
			- decreasing maximum achievable through put
- Scenario 3, four senders, multi-hot paths, timeout/retransmit![](https://i.imgur.com/UWl8AJR.png)
	- another "cost" of congestion
		- when packet dropped, any upstream transmission capacity and buffering used for that packet was wasted
- Approaches towards congestion control
	- *End-to-end congestion control*
	- *Network-assisted congestion control*![](https://i.imgur.com/MPZv7mS.png)
#### TCP Congestion Control
- TCP classic : AIMD ![](https://i.imgur.com/sXWtkHi.png)
	- approach : senders can increase sending rate until packet loss (congestion) occurs, then decrease sending rate on loss event
	- TCP congestion control part
	- AIMD : a distributed, asynchronous algorithm
		- optimize congested flow rates network wide
		- have desirable stability properties
	- <font color="#d99694">Multiplicative decrease</font> detail
		- Cut in half, triple duplicated ACK (TCP Reno)
		- Cut to 1, timeout (TCP Tahoe )
	- TCP Reno![](https://i.imgur.com/Tb1z0Ia.png)
	- TCP slow start
		- initially **cwnd** = 1 MSS
		- double **cwnd** every RTT
		- done by incrementing **cwnd** for every ACK received
		- when **cwnd** gets to 1/2 of its value before timeout (**ssthresh**)
			- on loss event, **ssthresh** is set to 1/2 of **cwnd** just before loss event
	- TCP congestion avoidance 
		- increases the value of **cwnd** by just a single MSS every RTT
		- timeout -> set **ssthresh** 1/2 of **cwnd** and goto slow start
	- TCP fast recovery (recommended, but not required)![|400](https://i.imgur.com/WpEE2QD.png)
		- dupACKcount == 3, **ssthresh = cwnd/2**
			- TCP Tahoe (early version)
				- **cwnd = 1**, go to *slow start*
			- TCP Reno
				- **cwnd = ssthresh + 3**, go to congestion avoidance
- TCP CUBIC![](https://i.imgur.com/RmDZDER.png)
	- $W_{max}$ : sending rate at which congestion loss was detected
		- congestion state of bottleneck link probably hasn't changed much
	- after cutting rate/window in half on loss, initially ramp to $W_{max}$ <font color="#ccc1d9">faster</font>, but then approach $W_{max}$ more <font color="#ccc1d9">slowly</font>
	- default in Linux, most popular TCP for popular Web servers
- TCP and the congested"bottleneck link"![](https://i.imgur.com/t5Hmyuj.png)
	- above TCP (classic, CUBIC) increase TCP's sending rate until packet loss occurs at some router's output : the bottleneck link
	- Delay-based TCP congestion control (***"just full enough, but no fuller"***)
		- congestion control without inducing/forcing loss
		- <font color="#ccc1d9">Delay-based approach</font>
			- $RTT_{min}$ : minimum observed RTT (uncongested path)
			- $$measured\ throughput=\frac{\text{number of bytes sent in last RTT interval}}{\text{RTT}_{\text{measured}}}$$
			- uncongested throughput with **cwnd** is $cwnd/RTT_{min}$
			- if measured throughput "very close" to uncongested throughput
				- increase **cwnd** linearly
			- else if "far below"
				- decrease **cwnd** linearly
- Explicit congestion notification (ECN)![](https://i.imgur.com/v3h19Ji.png)
	- network-assisted congestion control
	- Indicate congestion -> adjust 
- TCP fairness
	- Fairness goal : if K TCP sessions share same bottleneck link of bandwidth R, each should have average rate of R/K![](https://i.imgur.com/JGENOpT.png)
- ... Fairness network 
	- UDP
	- parallell TCP connections
#### Evolution of Transport Layer Functionality
- QUIC : Quick UDP Internet Connections
	- application-layer protocol on the top of UDP providing reliable, congestion-controlled, authentication, crypto state data transfer between two endpoints
	- using in HTTP/3 (transport protocol)
	- 1 handshake