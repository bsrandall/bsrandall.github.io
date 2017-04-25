---
layout: post
title: EtherChannel PaGP
category: EtherChannel
tag: knowledge
date: 2017-02-26 14:40:45
---
Port Aggregation Protocol (PAgP) is a Cisco proprietary protocol that is only supported on Cisco switches.

The two modes of PAgP are:
- auto: places a port into a passive negotiating state
- desirable: places a port into active negotiating state

For Layer 2 EtherChannels, the first port that comes up lends its MAC address to the EtherChannel.

PAgP supports up to 8 Ethernet ports of the same type.

For all EtherChannels (including on and PAgP), when a group is first created, all ports follow the parameters set for the first port to be added to the group. If you change the configuration of any of these parameters, you must also make changes to all ports in the group:
- Allowed-VLAN list
- Spanning-tree path cost for each VLAN
- Spanning-tree port priority for each VLAN
- Spanning-tree Port Fast setting

For all Layer 2 EtherChannels, if the ports are access ports they must all be in the same VLAN.  

