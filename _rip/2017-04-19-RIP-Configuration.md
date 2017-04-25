---
layout: post
title: RIP Configuration
category: RIP
tag: configuration
date: 2017-04-19 11:06:45
---
Only two steps are needed to configure RIP.
1. Enable RIP with the global configuration command `router rip`
2. Specify each major network on which to run RIP with the **network** command.

The classful nature of RIP means that we can only specify major class A, B, or C networks with the network command.

If needed, **debug ip rip** with show RIP messages and activity.

To block RIP broadcasts on an interface connected to a subnet of a RIP-enabled network, add the `passive-interface gig0/1` command to the RIP process. The **passive-interface** command is not specific to RIP as it can be used with all routing protocols for this purpose.  This will only get the router to quit **sending** updates. If you want the router to not learn routes advertised across the interface, you must filter those updates.

Another configuration option is the **neighbor**  command. If you specify a neighbor, routing exchanges will be done via unicast packets as compared to the normal RIP multicast method. Often, this is used in combination with the **passive-interface** command on Ethernet interfaces. The passive-interface disables the multicast advertisements but you can then enable advertisement exchange with a single host on the broadcast network via the **neighbor** command.

Another configuration issue is that RIPv1 does not support discontiguous networks. Discontiguous networks arise when a major network is separated by a major network. The problem arises because RIP summarizes at the major network boundary. This summarization is done at the classful boundary. If there is one major network between the two discontiguous networks, the RIP routers will receive a summarized route they already have in their routing table, so they will silently drop it. The result is that only half the of the discontiguous network is reachable. If there are two major networks between, then each major network believes it has a route to the summarized network, so they will install two equal-cost routes to the discontiguous network. This again would result in only half the communication being received by the destination network.

The workarounds for discontiguous networks with RIP would be to install static routes for the individual networks. The other solution is to apply secondary IPs to the interfaces of the in-between major network. These IPs would be from the summarized discontiguous network in question. The RIP routing process sees secondary addresses as separate data links.

Sometimes with RIP configuration, it may become necessary to manipulate the metric (hop count). This is done with the combination of an **offset-list** and an access-list. The offset-list adds the number specified to the metric of the route entry matching an access-list. The access-list matches the route for which to apply the offset-list. You use the keywords **in** and **out** with the offset-list to determine if the offset-list should change the metric on inbound Response Messages it receives or outbound Response Messages it sends. Here is an example configuration.
```
`access-list 1 permit 10.33.0.0 0.0.0.0
router rip
  network 192.168.12.0
  network 10.0.0.0
  offset-list 1 in 2 Serial0
```
`This one says examine RIP advertisements coming in interface Serial 0. If they are for the 10.33.0.0 network (from access-list 1), then add 2 hops to the metric.
```
`
Another configuration option is triggered updates. RIP will normally broadcast its entire routing table every 30 seconds by default. If no routes are changing, this can be very inefficient on slow links. On an interface, by interface basis, you can issue the command **ip rip triggered** which will force the routers on that interface to only exchange routes and updates when changes in the topology occur.
