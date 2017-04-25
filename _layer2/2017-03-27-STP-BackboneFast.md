---
layout: post
title: Spanning Tree BackboneFast
category: Spanning Tree
tag: knowledge
date: 2017-03-27 17:40:45
---
BackboneFast enables fast reconvergence due to indirect link failures. The key operation happens when a switch begins receiving inferior BPDUs.  When a switch loses the link off its Root Port, it immediately starts sending BPDUs announcing itself as the new Root. Usually, when a switch receives inferior BPDUs, it will wait for its Max Age timer to expire before beginning STP convergence. Once its Max Age timer expires, the inferior BPDU ages out and the switch will then forward its superior BPDU to the neighbor switch who was sending the inferior BPDU.

When BackboneFast is enabled, as soon as a switch receives an inferior BPDU, it will send RLQ (Root Link Query) messages out all it’s non-designated ports. The RLQ asks other switches if the current Root Bridge is accessible via that switch. Note it doesn’t wait for its Max Age timer to expire - it begins sending RLQ messages immediately. The RLQ is a new type of PDU defined within the BackboneFast specification. The RLQ is essentially a proactive way to age out ports compared to just waiting on the Max Age timer to expire.

Based on the received RLQ responses, the switch will update its root ports and designated ports accordingly.. However all ports still transition through the regular IEEE 802.1D STP port states - listening, learning, and forwarding/blocking.

To enable BackboneFast use the command `spanning-tree backbonefast` on all switches in the Layer 2 domain. The easiest way to verify that BackboneFast is enabled is to use the `show spanning-tree summary` command.

This is a great Cisco article describing the operation: [BackboneFast][1].

[1]:	http://www.cisco.com/c/en/us/support/docs/lan-switching/spanning-tree-protocol/12014-18.html