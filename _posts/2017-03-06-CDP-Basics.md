---
layout: post
title: CDP Basics
category: Layer 2
tag: knowledge
---
CDP is a layer 2, Cisco proprietary device discovery protocol. Even though it is a Layer 2 protocol, it provides information about Layer 3 protocols (such as IP address). CDP operates by its member devices sending multicasts to the link-local multicast address 01:00:0c:cc:cc:cc (same as VTP). The member devices listen for multicasts at that address, process them accordingly, and store the information in a local table. The announcements are sent out every 60 seconds by default. 

SNAP (Subnetwork Access Protocol) is required to run CDP, so effectively CDP can run on any data-link protocol that supports SNAP. Ethernet, Frame Relay, and ATM are example medias that support SNAP and thus CDP.

CDP relays the information about devices by Type-Length-Value (TLV) fields in the CDP packets. The *Length* is the length (in bytes) of the Type-Value-Length fields. The Type and Value fields are described below.

#### Type
- Device ID - 0x0001
- Address - 0x0002
- Port ID - 0x0003
- Capabilities - 0x0004
- Version - 0x0005
- Platform - 0x0006
- IP Prefix - 0x0007
- VTP Management Domain - 0x0009 {: .red}
- Native VLAN - 0x000a {: .red}
- Duplex Status - 0x000b {: .red}
- Appliance ID - 0x000c {: .red}
- Power consumption - 0x0010 {: .red}

#### Value
- Device ID - MAC address in ASCII or the FQDN
- Address
- Port ID - ASCII string that names the port from which the message was sent
- Capabilities - has a value describing the device capabilities:
	- 0x01 - level 3 routing
	- 0x02 - level 2 transparent bridging
	- 0x04 - level 2 source-route bridging
	- 0x08 - level 2 switching not running Spanning Tree
	- 0x10 - sends and receives packets for a network layer protocol
	- 0x20 - the device does not forward IGMP reports
	- 0x40 - level 1 function
- Version - software version running the device
- Platform - ASCII string describing the device (e.g. Cisco 7000)
- IP Prefix - a set of 0 or more IP Prefixes

Switches see the MAC multicast address used by CDP as a special address and will not forward it out of other interfaces on a switch. Routers do not forward layer 2 frames out of their interfaces ever, so therefore only directly connected neighbors receive the CDP advertisement.

The beauty of CDP is that if you walk into a network and you do not know the topology, you can use CDP to quickly learn the entire layout of the network (as long as all the devices are Cisco!).

