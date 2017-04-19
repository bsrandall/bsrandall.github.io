---
layout: post
title: GRE Tunnels
category: General Routing
tag: knowledge
date: 2017-04-09 17:40:45
---
A GRE Tunnel is an encapsulated tunnel between two devices that makes the connection act like a point-to-point interface. We are essentially putting packets inside packets; in other words, we are encapsulating the IP packets into GRE packets.

[link][1]
We will use the above figure to create a sample tunnel between the HQ and Branch routers.
```
`HQ(config)#interface tunnel 1     
HQ(config-if)#tunnel source fastEthernet 0/0
HQ(config-if)#tunnel destination 192.168.23.3
HQ(config-if)#ip address 192.168.13.1 255.255.255.0
```
````
`Branch(config)#interface tunnel 1
Branch(config-if)#tunnel source fastEthernet 0/0
Branch(config-if)#tunnel destination 192.168.12.1
Branch(config-if)#ip address 192.168.13.3 255.255.255.0
```
`
The default tunneling mode is GRE so it is not required to set it explicitly in this case.

Notice we are setting the destination address to be the outside interface that is reachable over the un-encapsulated network. You can also use loopback addresses.

Some options that GRE tunneling supports are:
- add an additional checksum
- specify a tunnel key
- enforce packet sequencing

Those options are seen under the **tunnel** subcommand in interface configuration mode.
```
`Router(config-if)# tunnel ?
  bandwidth           Set tunnel bandwidth informational parameter
  **checksum            enable end to end checksumming of packets**
  destination         destination of tunnel
  flow                flow options
  **key                 security or selector key**
  mode                tunnel encapsulation method
  mpls                MPLS tunnel commands
  path-mtu-discovery  Enable Path MTU Discovery on tunnel
  protection          Enable tunnel protection
  rbscp               Set tunnel RBSCP parameters
  route-via           Select subset of routes for tunnel transport
  **sequence-datagrams  drop datagrams arriving out of order**
  source              source of tunnel packets
  tos                 set type of service byte
  ttl                 set time to live
  udlr                associate tunnel with unidirectional interface
  vrf                 set tunnel vrf membership
```
`



[1]:	https://networklessons.com/wp-content/uploads/2013/04/three-cisco-routers-with-tunnel.png