---
layout: post
title: VTP Pruning
category: VTP
tag: knowledge
date: 2017-02-22 14:40:45
---
The principal of VTP pruning is if a client sends a broadcast to its connected switch's access port, that switch will flood the broadcast to all other connected switches in the VTP / Layer 2 domain. Because of VTP, all the other switches would be aware of the client VLAN, and would thus be required to flood the broadcast to all other switches.

But what if the other switches do not have any clients connected to access ports in that VLAN? They are still having to process the request, and the network segment still has to bear the broadcast traffic.

When you enable VTP pruning, you are enabling it for the entire VTP domain. 

VTP pruning is enabled on the VTP server(s) with the simple global configuration command `vtp pruning`. To verify what VLANs have been pruned, you should use `show interface trunk`. Note that the VLANs will still be seen in the output of `show vlan`, but you will see they are pruned in the command as shown below.
```
`SW4#sh int trunk

Port        Mode             Encapsulation  Status        Native vlan
Gi0/3       auto             802.1q         trunking      1
Gi1/0       auto             802.1q         trunking      1

Port        Vlans allowed on trunk
Gi0/3       1-4094
Gi1/0       1-4094

Port        Vlans allowed and active in management domain
Gi0/3       1,5,7-10,22,43,58,67,79,146
Gi1/0       1,5,7-10,22,43,58,67,79,146

Port        Vlans in spanning tree forwarding state and not pruned
Gi0/3       none
Gi1/0       none
```
`