---
layout: post
title: RIP Classful Routing
category: RIP
tag: knowledge
date: 2017-04-19 10:06:45
---
RIPv1 is a classful routing protocol. This is not quite as black and white as it seems. First, some housekeeping. When we see a route like this:
{% raw %}
```
`R    10.10.0.0 [120/3]() via 10.5.5.1, 00:00:20, Serial1
```
`{% endraw %}
The 120/3 is the administrative distance followed by the metric. With RIP, the metric is hop count, so 3 in this route indicates the network is 3 hops away via the Serial1 interface.

If more than one route exists for a destination, and both routes have the same hop count, then equal-cost load balancing will be performed.

RIP performs the route lookup by first performing a classful route table lookup.
{% raw %}
```
`Gateway of last resort is not set
10.0.0.0 255.255.0.0 is subnetted, 9 subnets
R    10.10.0.0 [120/3]() via 10.5.5.1, 00:00:20, Serial1
   [120/3]() via 10.1.1.1, 00:00:21, Ethernet0
R    10.11.0.0 [120/3]() via 10.5.5.1, 00:00:21, Serial1
   [120/3]() via 10.1.1.1, 00:00:21, Ethernet0
```
`{% endraw %}
So if a packet destined for 10.12.10.2 came into the router, it would first look for 10.0.0.0. If there were no match, the packet is dropped and an ICMP Destination Unreachable message is sent to the packet’s source. If there is a match for the network portion (as there is in this example), then the subnets are examined. If there is a subnet match, the packet is routed. If there is not subnet match, the packet is dropped and a Destination Unreachable message is sent (as would happen with 10.12.10.2).

If you look at the routing table and examine RIP entries, you will notice there is no provision for RIP to advertise a subnet mask along with each route entry. The router’s only recourse is to assume that the mask configured on one of its interfaces for that address is used consistently throughout the rest of the network.  If the network is not directly connected, there is a listing only for the major-class network and no associated mask.

Note that since the destination address of packets being routed by a classful routing protocol are interpreted according to the subnet masks locally configured on the router’s interfaces, all subnet masks within a major, class-level network must be consistent.

In the case above where there is no directly connected network, RIP summarizes at the classful network boundaries. This is called *subnet hiding*. So a router would only send advertisements for 10.0.0.0, 172.16.0.0, and 192.169.17.0 for example.

A good way to summarize is the following:
1. If the destination address is a member of a directly connected major network, the subnet mask configured on the interface attached to that network will be used to determine the subnet of the destination.
2. If the destination address is not a member of a directly connected major network, the router will try to match only the major class A, B, or C portion of the destination address.

