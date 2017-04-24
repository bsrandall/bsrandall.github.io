---
layout: post
title: RIPv2 Configuration
category: RIP
tag: configuration
date: 2017-04-19 20:48:45
---
Much of the configuration for RIPv2 is the same as for RIPv1. Here we will address some of the differences.

To specify RIPv2, use the version command under router configuration mode.
```
`router rip
  version 2
```
`
By default, a RIP process on  a Cisco router sends only RIPv1 messages but listens to both RIPv1 and RIPv2 messages. There are interface-level compatibility commands that should be utilized when working in an environment that uses both versions of RIP.
```
`interface Ethernet0
 ip address 192.168.50.129 255.255.255.192
 ip rip send version 1
 ip rip receive version 1
!
interface Ethernet1
 ip address 172.25.150.193 255.255.255.240
 ip rip send version 1 2
!
interface Ethernet2
 ip address 172.25.150.225 255.255.255.240
!
router rip
 version 2
 network 172.25.0.0
 network 192.168.50.0
```
`
We saw with RIPv1 that discontiguous subnets could be a problem. Classless routing protocols do not have the same issue, as each route update contains a mask, so subnets of one major network can be advertised into another major network. But the default behavior of RIPv2 is to summarize at network boundaries just like RIPv1. To turn off this summarization and allow subnets to be advertised across network boundaries, use the command **no auto-summary** in the RIP router configuration mode.

**ip rip triggered** will make the router stop sending periodic updates and will only send updates when there is a change to the routing table.