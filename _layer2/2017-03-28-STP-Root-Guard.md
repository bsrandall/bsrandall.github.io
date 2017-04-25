---
layout: post
title: Spanning Tree Root Guard
category: Spanning Tree
tag: knowledge
date: 2017-03-28 16:40:45
---
Root Guard is an enhancement to STP developed by Cisco. One issue with standard STP is that there is no way to ensure root bridge placement within the network. Even if you set a switch’s bridge priority to 0, another switch can come behind it with a priority of 0 and a lower MAC address and immediately take over the Root Bridge role.

Root Guard is enabled on a per port basis. Root Guard ensures that the port on which it is configured remains a designated port. If the bridge receives superior BPDUs on that designated port, Root Guard moves the port to root-inconsistent state, which is effectively equivalent to the STP listening state so no frames are forwarded.

The difference between BPDU Guard and Root Guard is that Root Guard allows the port to participate in STP, so long as the port does not receive a *superior* BPDU. With BPDU Guard, *any* BPDU will put the port into an err-disabled state.

Again, Root Guard is enabled on a per interface basis as below.
```
SW1(config)# interface gig0/1
SW!(config-if)# spanning-tree rootguard
```

The Cisco explanation is located [here][1].


[1]:	http://www.cisco.com/c/en/us/support/docs/lan-switching/spanning-tree-protocol/10588-74.html