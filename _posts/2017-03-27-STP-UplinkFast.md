---
layout: post
title: STP UplinkFast
category: Spanning Tree
tag: knowledge
---
UplinkFast provides fast convergence in case the link on which the root port is connected suffers a failure. It does this with the use of an uplink group. An uplink group is a set of Layer 2 interfaces, of which only one is forwarding at a particular time. If the root port (forwarding port) goes down, then a successor root port is chosen which immediately goes into Forwarding state, bypassing the Listening and Learning phases.

UplinkFast functionality is built into RSTP, so UplinkFast is only applicable with legacy IEEE 802.1D.

When UplinkFast is enabled on a switch, that switch’s bridge priority will automatically be increased to 49152 and its port cost will be increased to 3000. This is to ensure that the switch does not become a transit switch.

To enable UplinkFast, go to the switch on which you want it to run and run `spanning-tree uplinkfast` in global configuration mode.