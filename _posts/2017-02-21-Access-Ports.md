---
layout: post
title: Access Ports
category: VLAN
tag: knowledge
---
Access ports are those ports that are connected to end devices, not other switches. We define an access port on the command line with 
SW1# switchport mode access

We will see later with Spanning Tree, that PortFast can and should be used on access ports. This does two things. First, it allows the port to skip the listening phase for faster availability. Second, it prevents the access port from sending TCNs (Topology Change Notifications) every time a user plugs or unplugs a device into the port.

Another Spanning Tree feature which will relate to Access ports is BPDU Guard. With BPDU Guard, if the switch receives a BPDU on a port where BPDU Guard was enabled, the port will transition to the errdisabled state.