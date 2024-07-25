
# Networking basics

- Introduction
- Protocols
- Protocols layers
- Network Interconnection/Internet

## Introduction

### What is a network

A network can be defined as a group of computers and devices that are connected between them in such way that they can send and receive (exchanging) data between the devices of such network.

  - Each of this devices has an address, which is unique for each device, this address acts as the identifier of such devices, e.g: 204.160.241.98. Some networks can also have a "name" that is more easily to remember for us, humans, e.g: www.javasoft.com, corresponding to the above numeric address.

 - We can think of any devices as a node connected to the graph that is a network.

### DNS: Domain Name System

 When we browse through the internet we usually see the address of the pages we are visiting like: : www.javasoft.com The DNS is responsible for converting a mnemonic textual internet address like the wikipedia one, into its hard numeric Internet Address, which in the case of javasoft would be 204.160.241.98.

### Ports
They are the "doors "in which an application can run in the internet host machine

- There are some ports that are dedicated to some specific functions like: 
	- HTTP: 80
	- FTP: 20, 21
	- Gopher: 70
	- SMTP(Email): 25
	- POP3(email): 110
	- Telnet: 23
	- Finger: 79

### Data transmission:

 When data is sent across a network to one or many devices it is not send in its full "form", instead it is sent using "packet switching", that means that the data we intend to pass is broken into multiple packages, each package has a maximum size, and two containing parts: a *header* that contains information about its source and its destination, and a *content* part that contains a fragment of the "message" intended to transfer.

 Once each packet arrive to its destination the data is extracted from each packed, and it is reconstructed.

### Types of Networks

#### WAN : Wide Area Networks
This type of network is designed to connect networks across large distances, like states, countries, and even continents. It relies heavily in packet switching for efficiency.

#### LAN: Local Area Networks
This type of networks is designed to connect devices within a smaller geographical area, like a building or office. They can use packet switching too, but usually rely in other technologies to transfer information depending of the type of LAN.

- Ethernet: The most common type of LAN. It uses a shared medium approach, where all devices are connected through the network by the same cable. Data transmission is governed here by: CSMA/CD (Carrier Sense Multiple Access with Collision Detection) protocol, which allows devices to "listen" for traffic and avoid collisions.

- Token Ring: Uses a less common tech, where each device take turns passing data across the network using a token.

- Fiber channel: uses packet switching optimized for high-bandwidth and low-latency

### Interconnection

- Networks of low capacity may be connected together via a backbone
network which is a network of high capacity such as a FDDI network, a
WAN network etc.

- LANs and WANs can be interconnected via T1 or T3 digital leased
lines

- According to the protocols involved, networks interconnection is
achieved using one or several of the following devices:

→ Bridge: a computer or device that links two similar LANs based on
the same protocol.

→ Router: a communication computer that connects different types of
networks using different protocols.

→ B-router or Bridge/Router: a single device that combines both the
functions of bridge and router.

→ Gateway: a network device that connects two different systems, using
direct and systematic translation between protocols


# Protocols and Protocols layer

 Protocols are in charge of stablishing the rules that govern the exchange of data between two or more devices in the same network.

 Its role is addressing and routing messages, error handling, sequence and flow control of the interaction

- Protocols are designed based on a layered structure like OSI
- each entity at layer n can communicate with entities that are at layer n-1, but cannot communicate with entities at layer n+1, as each layer is encapsulated.

## Layers

The OSI (Open Systems Interconnection) Data Model

- ISO standard for computer networks design and functioning.

- Involves at least 7 layers, each playing a specific role when
applications are communicating over the net.

- During the sending process, each layer (from top to down) will add
a specific header to the raw data.

- At the reception, headers are eliminated conversely until the data
arrived to the receiving application.

**OSI Layers**
- Application Layer : applications connected to the network
- Presentation Layer : provides standard data representations for applications
-  Session Layer : manages sessions among applications
-  Transport Layer : provides end-to-end errors detection and correction
- Network Layer : handles connection to the network by the higher layers
- Data-link  Layer : provides safe communication of data over the physical network
- Physical Layer : defines the physical characteristics of the network





resources
 - https://www.ece.uvic.ca/~itraore/elec567-13/notes/dist-03-4.pdf
- 