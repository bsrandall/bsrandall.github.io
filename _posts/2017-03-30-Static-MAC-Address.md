---
layout: post
title: Static MAC Address Entries
category: Layer 2
tag: knowledge
---
Sometimes you may need to add static MAC address entries to the CAM table. This is easily achieved with the following global configuration command:
```
SW1(cone)# mac address-table static 0022.5627.1fc1 vlan 10 interface GigabitEthernet0/1
```
You can also force traffic to a particular MAC address to be dropped, by either specifying an unused interface or with the following:
```
SW1(conf)# mac address-table static 0022.5627.1fc1 vlan 10 drop
```
