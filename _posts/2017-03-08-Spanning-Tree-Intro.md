---
layout: post
title: Spanning Tree Intro
category: Spanning Tree
tag: knowledge
---
![][image-1]

Imagine in the above diagram that H1 sends out an ARP request, which is a broadcast frame. SW1 will forward this broadcast frame on ports Fa0/0 and Fa1/0 toward SW2.

SW2 will forward the broadcast frame it received on Fa0/0 out Fa1/0 and the interface connected to H2. This cycle will continue and continue. By introducing redundancy, we have created an environment that is friendly to Layer 2 loops. And since Ethernet frames do not have a TTL, they will loop around forever.

Spanning Tree is a Layer 2 protocol that was created to deal with the possible loop creation that is introduced with redundant Layer 2 loops. Spanning Tree takes over the Layer 2 forwarding decisions, and places certain ports in a blocking state to prevent the possibility of these loops occurring.

When Spanning Tree is enabled, switches send out a special frame called a BPDU (Bridge Protocol Data Unit). Included in this BPDU is the Switch’s Priority and MAC Address, which concatenated equals the Bridge Id. Among connected Switch’s, the Switch with the lowest Bridge Id becomes the Root Bridge.

A Root Bridge marks all of its ports as Designated, which are placed in a forwarding state. Designated ports lead away from the Root bridge.

For the remaining switches, we have to elect one root port on each switch. The root port will be the port whose path has the lowest cost to the root bridge

[image-1]:	https://networklessons.com/wp-content/uploads/2013/01/switches-redundant-cable-1.png