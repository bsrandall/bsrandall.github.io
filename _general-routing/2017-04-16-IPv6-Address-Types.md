---
layout: post
title: IPv6 Address types
category: IPv6 General
tag: knowledge
date: 2017-04-16 18:54:45
---
There are 3 types of IPv6 addresses:
- Unicast
- Anycast
- Multicast

There is no “broadcast” type as in IPv4, but an “all nodes” multicast address does exist, which essentially serves the same purpose.
#### Unicast
A unicast address is an address that identifies a single device. A *global* unicast address is one that is assigned to a single host and is globally unique. These are the equivalent of a routable IPv4 address.
[link][1]
The host portion of the address is called the Interface ID. This is a more accurate description as a host can have more than one address (as can an interface, but often not).

IPv6 addresses, unlike IPv4 addresses, have the subnet bits built in as part of the network portion of the address. In IPv4, the subnet bits were borrowed from the host portion. One benefit from this is that the Interface ID can be a consistent length for all IPv6 addresses, simplifying parsing of the address. The Interface ID, with very few exceptions, is 64 bits long. Also, with very few exceptions, the Subnet ID field is 16 bits long, providing for 65,636 separate subnets. This leaves 48 bits for the Global Routing Prefix of the address.

The currently allocated IPv6 global unicast addresses are 2xxx::/4 through 3xxx::/4. The most common allocation is a /48 global routing prefix, a 16-bit subnet ID, and a 64 bit Interface ID.

IPv6 also has *link-local* unicast address in addition to the global unicast address type. The difference is that a link-local address’ scope is limited to a single link, and its uniqueness in not guaranteed outside of that link. The first 10 bits are always FE80 (1111111010). Link-local addresses have great utility for functions like Neighbor Discovery Protocol and Address Autoconfiguration. They are similar to the 169.254.0.0/16 in IPv4. Link local addresses are never routable. Below is an example configuration in which you will see a subnet is not even declared.
```
`R1(config)# interface GigabitEthernet0/1
R1(config-if)# ipv6 address FE80::1 link-local
R1config-if)# exit
```
`Link-local addresses are significant only within a single link. Packets with link-local sources or destinations are mostly used by the router’s control plane protocols, such as IPv6 routing protocols. 


There is also *unique-local* IPv6 addresses. These are equivalent to IPv4 RFC1918 addresses. They are likely unique, but not routable via global BGP. Thee always start with FC00::/7.

#### Anycast
An any cast address really represents more of a service than an address. An any cast address can reside on multiple hosts. Routers do not know they reside on different hosts but assume that they have multiple routes to the same host, so a single router simply choses the route to which it has the lowest cost route. Anycast also offers reliable backup, for if a single device goes down, routers will just route to the next lowest-cost available server. There are some reserved Anycast addresses, but for most services, an anycast address is just a global unicast address providing the any cast service.

#### Multicast
A multicast address identifies a set of devices - a *multicast group*. The first 8 bits of a multicast address are always 1s (FF00). The next 4 bits are the Flags. The following 4 bits are the Scope. Finally, the last 112 bits represent the Group ID.

#### Address Type Identification
| **Address Type**      | **Binary Prefic** | **IPv6 notation** |
| Unspecified  | 00…0 (128 bits) | ::/128 |
| Loopback | 00…1 (128 bits) | ::1/128 |
| Multicast | 11111111 | FF00::/8 |
| Link-local Unicast | 1111111010 | FE80::/10 |
| Unique-local Unicast | 11111100 | FC000::/10 |

Global unicast addresses are everything else.






[1]:	http://www.cisco.com/c/dam/en/us/td/i/300001-400000/330001-340000/330001-331000/330523.tif/_jcr_content/renditions/330523.jpg