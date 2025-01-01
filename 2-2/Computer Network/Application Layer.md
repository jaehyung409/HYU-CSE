#network
#### Principles of network applications
0. Basics of network applications
	- run on end systems (no need to write software for network-core devices)
	- communicate over network
1. Architecture (flexible)
	1. Client-Server paradigm
		- Server :
			- Always-on host
			- permanent IP address
			- often in data centers, for scaling (for keeping up with all the requests)
		- Clients :
			- contact, communicate with server
			- may be intermittently connected
			- may have dynamic IP address
			- do not communicate directly with each other
		- Examples : HTTP, IMAP, FTP
	2. Peer-Peer architeture
		- no always-on server (cost effective)
		- arbitary end systems directly communicate
		- peers request service from other peers, provide services in return to other peers
			- self scalability : new peers bring new service capacity, as well as new service demands
		- peer are intermittently connected and change IP address
			- complex management (security, performance, reliability)
		- Examples : P2P file sharing (BitTorrent)
2. Processes communicating
	- Process : program running within a host (end systems)
		- communicate by exchanging messages(sockets) (in different hosts)
	- Client process : process that initiates communication
	- Server process : process that waits to be contacted
	- Socket 
		>process sends/receives messages to/from its socket
		>interface between the application layer and the transport layer within a host. (API between the application and the network)
	- Identifier : IP address , Port number
3. Transport Service
	1. Need : 
		- data integrity : 100% reliable data
		- timing : low delay to be "effective"
		- throughput : minimum amount of throughput to be "effective"
		- security : encryption, data integrity ... etc.
	2. TCP service
		- <font color="#de7802">Reliable transport</font> : between sending and receiving process
		- <font color="#de7802">connection-oriented</font> : setup required between client and server processes
		- flow control : sender won't overwhelm receiver
		- congestion control : throttle sender when network overloaded
		- doer not provide : timing, minimum throughput guarantee, security 
	- Securing TCP (TLS)
		- encrypted TCP connections, data integrity, end-point authentication
	3. UDP service
		- unreliable data transfer : betweeb sending and receiving process
		- does not provde : reliability, flow control, congestion, control, timing, throughput, guarantee, security, or connection seyup 

#### The Web and HTTP
1. Overview of HTTP (Hyper Text Transfer Protocol)
    > HTTP defines how Web clients request Web pages from Web serversa nd how servers transefer Web pages to clients.
	- Client : browser that requests, receives, and "displayes" Web objects.
	- Server : Web server sends objects in response to requests.
- Using TCP as its underlying transport protocol
	- clinet initiates TCP connection (creates socket) to server, port 80
	- server accepts TCP connection from client
	- HTTP messages (applicaiton-layer protocol messages) exchanged between browse (HTTP client) and Web server (HTTP server)
	- TCP connection closed
	- ! HTTP need not worry about lost data or the details of how TCP recovers.
- HTTP is "stateless" : server maintains no information about past client requests.
2. HTTP connectios : two types
	- RTT (round-trip time) : includes packet delay
	- three-way-handshake for TCP connection (client - server) : take one RTT
	- Non-persistent HTTP (separate TCP connection)
		- In HTTP/1.0
		- downloading multiple objects required multiple connections
		- Total Time : \# of connections x (2 RTT + Time to transmit file)
	- Persistent HTTP (same TCP connection)
		- In HTTP/1.1
		- TCP connection opened to a server (multiple objects can be sent over single TCP)
		- Total Time : 1 RTT + \# of connections x (1RTT + Time to transmit file)
3. HTTP request message
	- Request line(\#1) 
		- Method : POST, _GET_, HEAD, PUT
	- Header lines(\#2~4)  
	- Blank line(\#5) : carriage return + line-feed, means header lines end, after lines are "entity body"
```HTTP
1	method URL version \r\n
2	header field name: value \r\n
	...
4	header field name: value \r\n
5	\r\n
```
4. HTTP response message
	- Response line(\#1) 
		- status codes : 200 OK, 301 Moved Permanently, 400 Bad Request, 404 Not Found, 505 HTTP Version Not Supported
	- Header lines(\#2~4)  
	- Blank line(\#5) : carriage return + line-feed, means header lines end, after lines are "entity body"
```HTTP
1	version status-code phrase \r\n
2	header field name : value \r\n
	...
4	header field name : value \r\n
5	\r\n
```
5. Web Cookies 
    > maintain some state between transactions
	- four components :
		1. cookie header line of HTTP response message
		2. cookie header line in next HTTP request message
		3. cookie file kept on user's host, managed by user's browser
		4. back-end database at Web site
	- used for authorization, shopping carts, recommendations, user session state
	- tracking a user's browsing behavior
		- track user behavior on a given website (<font color="#de7802">first party cookies</font>)
		- track user behavior across multiple websites (<font color="#de7802">third party cookies</font>) without user ever choosing to vist tracker site.
	- Invasion of privacy problem (~GDPR)
6. Web Caches (Proxy server)
	> Goal : satisfy client requests without involving origin server
	> Network entity that satisfies HTTP requests on the behalf of an orign Web server. It has own disk storage and keeps copies of recently requested objects in this storage
	- Profit : reduce response time and reduce traffic on an institution's access link
7. Browser caching : Conditional GET
	>Goal : don't send object if browser has up-to-date cached version (no object transmission delay)
	- client : specify date of browser-cached copy in HTTP request
		- **If-modified-since: \<date>**
	- server : response contains no object if browser-cached copy is up-to-date
		- **HTTP/1.0 304 Not Modified**
8. HTTP/2
	>Key goal : decreased delay in multi-object HTTP requests
	- HTTP/1.1 : server responds _in-order_ 
		- problem of HOL blocking => Using multiple parallel TCP connections
		- **Framing!** in HTTP/2
	- HTTP/2 : transmission ordr of requested objects based on client-specified object priority
		- *push* unrequested object to client (server send multiple response)
		- divide objects into frames, schedule frames to mitigate HOL blocking
		- no security over vanilla TCP connection -> HTTP/3 (adds security)

![](https://i.imgur.com/HcM6TfY.png)->objects divided into frames, frame transmission interleaved




#### The Domain Name System DNS
1. Services Provided by DNS : Domain Name System
	- Internet hosts, routers has many identifiers such as IP address, "hostname"
	- DNS  :
		- distributed database implemented in a hierachy of **DNS servers**
		- application-layer protocol : hosts, DNS servers communicate to _resolve_ names (address/name translation) 
	- DNS services :
		- hostname-to-IP-address translation
		- host aliasing
		- mail server aliasing
		- load distribution 
			- replicated Web servers : many IP addresses correspond to one name
2. Overview of How DNS Works
	- Simple Design (centralize)
		- single point of failure
		- traffic volume
		- distant centralized database
		- maintenance
	- A Distributed, Hierarchical Database
		- Root DNS servers : provide the IP addresses of the TLD servers
			- official, contact-of-last-resort by name servers that can not resolve name
			- <font color="#de7802">incredibly important</font> Internet function
			- Copies of 13 different root servers, managed by 12 different organizations.
		- TLD (Top-Level Domain) servers
			- .com, .org, .net ... and all top-level country domains
		- Authoritative DNS servers
			- organization's own DNS server(s), providing authoritative hostname to IP mapping for organization's named hosts.
		- Local DNS server (not strictly belong to the hierarchy of servers)
			- when host makes DNS query, it is sent to its local DNS server
			- Local DNS server returns reply, answering

		- ![](https://i.imgur.com/I08pecw.png)
3. DNS name resolution 
	- Iterated and Recursive query
	- ![](https://i.imgur.com/leAxyd4.png)
4. DNS Caching
	> once name server learns mapping, it caches mapping, and immedtiately returns a cached mapping in response to a query
	> cached entries may be out-of-data
5. DNS Records and Messages
	-  DNS : distributed database storing resource records (<font color="#de7802">RR</font>)
	- Resource Record is a four-tuple that contains (_Name, Value, Type, TTL(time to live_))
		- <font color="#de7802">type=A (AAAA : IPv6)</font>
			- _name_ is hostname
			- _value_ is IP address
		- <font color="#de7802">type=NS</font>
			- _name_ is alias name for some "canonical" name
			- _value_ is canonical name
		- type=CNAME
			- _name_ is domain
			- _value_ is hostname of authoriative name server for this domain
			- used to route DNS queries further along in the query chain
		- type=MX
			- _value_ is name of SMTP mail server associated with _name_
	- DNS protocol Messages
		>DNS <font color="#de7802">query</font> and <font color="#de7802">reply</font> messages, both have same <font color="#de7802">format</font>
	
| DNS messages format                  | <                 | Explanation                                |
| ------------------------------------ | ----------------- | ------------------------------------------ |
| <- 2bytes ->                         | <- 2bytes ->      |                                            |
| Identification                       | Flags             | 12bytes, header section                    | 
| \# questions                         | \# answer RRs     | ^                                          |
| \# authority RRs                     | \# additional RRs | ^                                          |
| questions (variable \# of questions) | <                 | name,type fields for a query               |
| answers (variable \# of RRs)         | <                 | RRs in response to query                   |
| authority (variable \# of RRs)       | <                 | records for authoritative servers          |
| additional info (variable \# of RRs) | <                 | additional "helpful" info that may be used |
- Identification : 16 bit \# for query, reply to query uses same \#
- Flags : 1-bit query/reply flags
	- query or reply
	- recursion desired
	- recursion availiable
	- reply is authoritative
6. Getting your info into the DNS
	1. register name network at _DNS register_
		- provide names, IP addresses of authoritative name server
		- register inserts NS, A RRs into TLD server
	2. create authoriatives server locally with IP address
		- type A record for your Web server and the type MX resource for your mail server.
7. DNS security
	1. DDoS attacks (bombed root servers, TLD servers)
	2. Spoofing attacks (intercept DNS queries, returning bogus replies)

#### Socket programin with UDP and TCP