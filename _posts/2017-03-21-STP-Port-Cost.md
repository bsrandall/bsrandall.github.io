---
layout: post
title: STP Path Selection with Port Cost
category: Spanning Tree
tag: knowledge
---
There are two ways we can alter STP Path selection. We can alter the cost of a port, or we can change the priority of a port.

When a switch receives a BPDU, that BPDU contains the root path cost from the previous switch. The receiving switch then adds the cost of the link between it and the sending switch from which it received the BPDU. That is very important - it is the receiving switch that adds the cost associated with its interface to the Root Path Cost it received from the sending switch.

Cost is used for the selection of the root port to the upstream switch.

Priority is used for influencing the root port of the downstream switch, and as such, it is set up on a port in Designated state. Cost has a higher precedence than priority. You will see priority on the local switch `show spanning-tree vlan 2` but it will actually affect the forwarding decision on the downstream connected switch.