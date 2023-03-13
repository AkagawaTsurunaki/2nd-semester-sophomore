Pure (unslotted ) ALOHA

- unslotted aloha: simpler, no-sync

- when frame first arrivess : transmit immediately

- collision probability increase: sent at $t_0 <-> [t_0-1, t_0+1]$

efficiency: (proof omitted)



## CSMA (Carrier Sense Multiple Access)

- **CSMA**: listen before transmit:
  - if channel sensed idle: transmit entire frame.
  - if busy: defer transmission.

- **CSMA collisions**
  - **collisions can still occur**: because of propagation delay -> may not hear each other.
  - **collision**: causes entire packet transmission, time wasted.
  - **note**: role of distance & propagation delay in determining collision probability.

## CSMA/CD (Collision Detection)

- CSMA/CD: carrier sensing

  - collisions detected within short time.

  - colliding transmission aborted, reducing channel wastage

- Collision detection:

  - easy in wired LANs: measure signal strengths, compare transmitted, received signals.(if signal become strong, may collision happen)
  - difficult in wireless LANs: other signal from nature or mankind may affect signal.

![image-20230313110330087](ComputerNetwork.assets\image-20230313110330087.png)

## "Taking Turns" MAC Protocols

- channel partitioning MAC proto

  - share channel efficiently and fairly at high load.

  - inefficient at low load: 1/N bandwidth allocated even if only 1 active node!

- Random access MAC protocols

  - efficient at low load: single node can fully utilize channel.

  - high load: collision overhead.

- "taking turns" protocols

#### Polling

- Master node "invites" slave nodes to transmit in turn.

- Concerns 
  - polling overhead
  - latency
  - single point of failure (master)

#### Token passing -> solve polling

- Control token passed from one node to next sequentially.
- Token message
- Concerns:
  - token overhead.
  - latency
  - single point of failure (token)



# ETHERNET

## 2 Standards of Ethernet:

DIX Ethernet V2

IEEE 802.3

## 数据链路层的两个子层

逻辑链路控制LLC(Logical Link Control)子层

媒体接入控制MAC(Media Access Control)子层

与接入到传输媒体有关的内容都放在 MAC子层，而 LLC 子层则与传输媒体无关，不管采用何种协议的局域网对 LLC 子层来说都是透明的.

#### 适配器(Adaptor)的作用

- NIC (Network Interface Card)网卡(网络接口卡)

- 功能:

  - 进行串行/并行转换
  - Cache data
  - Driver in OS
  - Implement Ethernet protocols.

  

#### LAN Addresses & ARP

- Each adaptor on LAN has unique LAN address.

- 12 Hex MAC Address 
  - Broadcast address: FF-FF-FF-FF-FF-FF

- 32-bit IP Address:
  - network-layer address
  - used to get datagram to dest IP subnet
- MAC(or LAN or physical or Ethernet) address:
  - Used to get frame from one interface to another physically-connected interface (same network) 
  - 48 bit MAC address (for most LANs) burned in the adapter ROM
- MAC address allocation administered by IEEE
- Manufacturer buys portion of MAC address space (to assure uniqueness)
- MAC flat address ➜ portability
- IP hierarchical address NOT portable: depends on IP subnet to which node is attached



#### ARP: Address Resolution Protocol

each IP node (host, router) on LAN has ARP table.

ARP stored `<IP addr, MAC addr, TTL>`(Time to Live, typically 20 min)



#### ARP protocol: Same LAN (network)

A -> No B in APR Table -> Broadcast req B -> B单播 -> A -> stored B's MAC

**soft state**: info may be invalid without broadcasting or informing.

**ARP is "plug-and-play"**: without intervention.

#### ARP protocol: Routing to another LAN

A -> not in same LAN -> A send to router -> -> find B in another LAN

R has 2 ARP tables.

modify src MAC and dest MAC

#### Start topology(ommitted)

#### Ethernet Frame Structure

![image-20230313120924788](ComputerNetwork.assets\image-20230313120924788.png)

- Preamble(前导域)

  - 10101010 前同步码

  - 10101011 帧开始定界符

- Addresses: 12 bytes
  - 6 bytes scr addr, 6 bytes dest addr
- Type
  - 2 bytes, indicates the higher protocol (normally IP) 
- CRC
  - 4 bytes

#### 无效的MAC帧

- 数据字段的长度与长度字段的值不一致；
- 帧的长度不是整数个字节；
- 用收到的帧检验序列 FCS 查出有差错；
- 数据字段的长度不在 46 ~ 1500 字节之间。
- 有效的 MAC 帧长度为 64 ~ 1518 字节之间。
- 对于检查出的无效 MAC 帧就简单地丢弃。以太网不负责重传丢弃的帧。



#### Unreliable, connectionless service

Connectionless: No handshaking between sending and receiving adapter.

Unreliable: receiving adapter doesn’t send acks or nacks to sending adapter (e.g. gaps).



#### Ethernet uses CSMA/CD



- No slots
- adapter doesn’t transmit if it senses that some other adapter is transmitting, that is, carrier sense
- transmitting adapter aborts when it senses that another adapter is transmitting, that is, collision detection.
- Before attempting a retransmission, adapter waits a random time, that is, random access.



Jam Signal

Bit time: 1 microsec for Mbps