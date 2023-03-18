# Chapter 1: Introduction

> Aka.T: Hmm... You are not good at English? Don't worry, I will show you a table which includes some terms in Chapter 1.
>
> When you find italics in your reading, that's what I added.
>
> "Omitted" means the content of this title is not important.
>
> Some metaphors, analogies will be omitted.

| Term        | Chinese          | Term           | Chinese   |
| ----------- | ---------------- | -------------- | --------- |
| LAN         | 局域网           | Bandwidth      | 带宽      |
| WAN         | 广域网           | infrastructure | 基础设施  |
| Router      | 路由器           | Ethernet       | 以太网    |
| Switch      | 交换机           | Multiplexing   | 多路复用  |
| Protocol    | 协议             | Encapsulation  | 封装      |
| Packet      | 数据包/报文/分组 | Stack          | 栈        |
| ISP         | 因特网服务提供商 | FDM            | 频分复用  |
| TCP         | 传输控制协议     | TDM            | 时分复用  |
| UDP         | 用户数据报协议   | congestion     | 拥挤/拥塞 |
| Intranet    | 内网             | Extranet       | 外网      |
| *mainframe* | *主机*           | *topology*     | 拓扑      |

## 1.1 What is the Internet

## Definition of Computer Networks

A computer network is composed of multiple computers connected together using a telecommunication system for the purpose of sharing data, resources and communication.

## Features

Computer network connects two or more autonomous computers.

The computers can be geographically located anywhere.

## Composition of Computer Network

| Hardware                                                     | Software                                 |
| ------------------------------------------------------------ | ---------------------------------------- |
| End systems: host, PC, mainframe, client, workstation, server | Protocol: CSMA/CD, TCP/IP, UDP, PPP, ATM |
| Intermediate systems: communications: switch, router         | Applications: HTTP, SMTP, FTP, Telnet    |
| Interface: network interface card (NIC), modem               |                                          |
| Medium: twisted pair, coaxial cable, fiber, wireless         |                                          |

## Application of Networks

- Resource sharing
  - Hardware: computing resources, disks, printers...
  - Software: application software...
- Information sharing
  - Easy accessibility from anywhere: files, databases...
  - Search Capability: WWW...
- Communication
  - Email
  - Message broadcast
- Remote Computing
- Distributed Processing (GRID Computing)

## Applications

E-mail, searchable data (Web Sites), E-commerce, news groups, Internet telephony (VoIP), video conferencing, chat groups, instant messengers, Internet radio.

## "Cool" Internet Appliances(Omitted)

## Category of Computer Networks

### Classified by Topology

- The network topology defines the way in which computers, printers, and other devices are connected.

- A network topology describes the layout of the wire and devices as well as the paths used by data transmissions.

![image-20230317221701445](Chapter1.assets/image-20230317221701445.png)

#### Bus topology

Commonly referred to as a linear bus, all the devices on a bus topology are connected by one single cable.

#### Star & Tree topology

- The star topology is the most commonly used architecture in Ethernet LANS.
- Larger networks use the extended stat topology also called tree topology.
- When used with network devices that filter frames or packets, like bridges, switches, and routers, this topology significantly reduces the traffic on the wires by sending packets only to the wires of the destination host.

#### Ring topology

- A frame travels around the ring, stopping at each node. If a node wants to transmit data, it adds the data as well as the destination address to the frame.

- The frame then continues around the ring until it finds the destination node, which takes the data out of the frame.
  - Single ring - All the devices on the network share a single cable.
  - Dual ring - The dual ring topology allows data to be sent in both directions.

### Classified by Boundary

#### Intranet (Private Networks)

An Intranet is a private networks that is contained within an enterprise. It may consist of many interlinked local area network and also use leased in the wide area network.

#### Extranet (Public Networks)

An extranet is a public network that uses Internet technology and the public telecommunication system to securely share part of a business's information or operations with suppliers, vendors, partners, customers, or other businesses. An extranet can be viewed as part of a company's intranet that is extended to users outside the company. It has also been described as a "state of mind" in which the Internet is perceived as a way to do business with other companies as well as to sell products to customers.

## 1.2 Internet History

## 1.3 Network Edge

## 1.4 Network Core

## 1.5 Network Access and Physical Media

## 1.6 Internet Structure and ISPs

## 1.7 Delay & Loss in Packet-switched Networks

## 1.8 Protocols Layers, Service Models

