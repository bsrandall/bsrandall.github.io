---
layout: post
title: RIPng Configuration
category: RIPng
tag: knowledge
date: 2017-04-19 22:06:45
---
RIPng has an entirely different (and simpler) configuration process. Instead of specifying networks under router rip configuration mode, you simply enable IPv6 routing globally and then enable RIPng on a per interface basis.
```
`ipv6 unicast-routing
interface Ethernet0
 ipv6 address 2001:db8:0:6::1/64
 ipv6 rip bigMountain enable
!
interface Ethernet1
 ipv6 address 2001:db8:0:4::1/64
 ipv6 rip bigMountain enable
!
interface Ethernet2
 ipv6 address 2001:db8:0:5::1/64
 ipv6 rip bigMountain enable
```
`The process name is relevant only to the local router. But it is possible to have multiple RIPng routing processes running on the same router, unlike in RIPv1 or RIPv2 where only one RIP routing process was allowed per router. However if multiple RIPng processes are going to run on a single interface, you must change the UDP port to something other than 521 on any extra processes.
```
`ipv6 router rip smallMountain
  port 527 multicast ff02::9
```
`The fact that process names are only locally significant should also give you a clue that the port numbers would have to be different for multiple processes to be running on the same interface.

Even though the enabling of RIPng occurs at the interface level, much of the customization is still done at the router configuration mode, just as with RIPv1 and RIPv2.
```
`ipv6 router rip bigMountain
  timers 10 30 30 60
  maximum-paths 8
  distance 200
```
`The default RIPng timer values are:
- update: 30 seconds
- expire (invalid): 180 seconds
- garbage collection: 120 seconds
- holddown: 0 seconds

Metric manipulation is different with RIPng. With RIPv1 and RIPv2, the hop count was adjusted by using an offset. RIPng does not modify the metric of each entry in a list of prefixes. Instead, RIPng modifies the hop count that is associated with an interface. This increments the metric of every prefix that is advertised to the router via their interface by the mount of the hop count configured on the interface. By default, RIPng adds a hop count of one to the prefixes advertised by a neighbor received by an interface. To alter the hop count that is added, us the **metric-offset** interface subcommand.
```
`interface Ethernet0/1
  ipv6 rip smallMountain metric-offset 3
```
`