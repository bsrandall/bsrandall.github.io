---
layout: post
title: STP Root Bridge Election
category: Spanning Tree
tag: knowledge
date: 2017-03-20 14:40:45
---
STP Root Bridge Election is based on the Bridge ID of the switches in the active Layer 2 domain. The Bridge ID is made up of the 4-bit bridge priority, a 12-bit Systems ID, and the 48-bit MAC address. The bridge priority is configurable from 0 to 61440. The default is 32768. The System ID is taken from the VLAN number (IEEE 802.1t).

The election process is very simple. Each bridge starts off assuming it is the Root Bridge and sends BPDUs out advertising itself as such. If it receives a superior BPDU (a BPDU that has a Bridge ID lower than its current root bridge Bridge ID), it ceases advertising that Root Bridge and begins advertising the new Root Bridge with the lower Bridge ID. This process continues until all switches in the domain agree to the same Root Bridge.

Note that since MAC addresses are guaranteed to be unique, there will always be 1 Root Bridge elected. If all switches are set to the default priority, then the switch with the lowest MAC Address will become the Root Bridge. this is a bad idea for many reasons. One, you typically want your distribution layer switch to be the Root Bridge. Second, older switches will have lower MAC addresses, so your switch with the least resources ends up having a heavier load along with a higher chance for failure 