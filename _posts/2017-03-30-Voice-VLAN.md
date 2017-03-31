---
layout: post
title: Voice VLAN
category: Layer 2
tag: knowledge
---
On Cisco switch’s, you can configure a particular VLAN known as the voice VLAN. It is a special VLAN that Cisco developed that is meant to lead from the switch the the 3 port switch on the back of an IP Phone. The traffic from the computer will be sent untagged, regardless of whether the access VLAN for that port is the default VLAN. All traffic from the phone gets tagged to its assigned voice VLAN. It behaves in many way like a trunk, but from an operational perspective it is still a port in access mode. The configuration looks like this:
```
SW1(config)# interface GigabitEthernet0/1
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 100
SW1(config-if)# switchport voice vlan 101
```
If you you show commands, you will not find the interface to be in trunk operational mode, but remember it works like a rudimentary trunk.