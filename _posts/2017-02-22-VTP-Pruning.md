---
layout: post
title: VTP Pruning
category: VTP
tag: knowledge
---
The principal of VTP pruning is if a client sends a broadcast to its connected switch's access port, that switch will flood the broadcast to all other connected switches in the VTP / Layer 2 domain. Because of VTP, all the other switches would be aware of the client VLAN, and would thus be required to flood the broadcast to all other switches.

But what if the other switches do not have any clients connected to access ports in that VLAN? They are still having to process the request, and the network segment still has to bear the broadcast traffic.

When you enable VTP pruning, you are enabling it for the entire VTP domain. 

NEED TO FINISH