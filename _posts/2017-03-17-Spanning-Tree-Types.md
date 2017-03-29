---
layout: post
title: Virtual Switch System
category: Layer 2
tag: knowledge
---
There are several different versions of the Spanning Tree Protocol that we will come across. We will review them in chronological order today.

The original spanning tree is Common Spanning Tree, or CST. It was defined with IEEE 802.1D. The basic premise is to create a logical loop free topology for Ethernet networks by building a spanning tree of connected layer-2 bridges. The links that are not part of the spanning tree are disabled, leaving a single active path between any two network nodes.

PVST and PVST+ are both Cisco proprietary protocols. Cisco developed them as they believed we may need different spanning-trees on a per-VLAN basis for  the best path flow. PVST only ran over ISL trunks, but with PVST+ compatibility with 802.1q trunks arrived. The + version also added new features such as UplinkFast, BackboneFast, and PortFast.

RSTP is the IEEE’s answer to Cisco’s PVST+ implementation. RSTP took many of the added features of PVST+ and standardized them into IEEE 802.1w. RSTP added new bridge port roles and port states.

Cisco then responded to the IEEE 802.1w Rapid Spanning Tree Protocol with RPVST+, which is just RSTP with per-vlan support. RPVST+ supports both ISL and 802.1Q trunks.

When the concept of VLANs finally hit home when VoIP hit the LAN, everyone finally agreed that we needed VLAN support for STP. However, it was also determined that there are usually on three paths needed to support redundancy with Spanning Tree designs. But yet with Spanning Trees based on a per-VLAN approach, we may end up with way more than 3 instances of Spanning Tree running on the router.

This led to the introduction of Multiple Spanning Tree Protocol. It was originally defined with 802.1s and was later merged into IEEE 802.1Q-2005. MSTP creates on common Spanning Tree for the entire Layer 2 network. If a network contains multiple VLANs, we can create multiple Spanning Trees and then assign specific VLANs to specific Spanning Tree instances. Since most networks will need a maximum of two Spanning Tree instances, MSTP greatly reduces the overhead on the router compared to RPVST which needed a separate instance per VLAN.

Cisco MST supports both 802.1Q and ISL trunks.