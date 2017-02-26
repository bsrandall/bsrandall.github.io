---
layout: post
title: EtherChannel LACP
category: EtherChannel
tag: knowledge
---
LACP is the IEEE standard for establishing a single logical channel out of several physical ports. It is popular as it can be used in mixed-vendor switch environments. LACP ensures that when an EtherChannel is created, all physical members all have the same speed, duplex, link-type, and VLAN information. LACP is a control protocol for LAG.

LACP assigns system priority, port priority, and and an administrative key.

*System priority* and the MAC address form the System ID. Between two LACP neighbors, the switch with the lowest System ID will be the decision maker using the LACP Port Priority

*Port priority* and the port number form the port identifier. The switch uses the port identifier to decide which ports to put in standby mode when a hardware limitation prevents all ports from aggregating. Port priority is also used when more than 8 physical ports are put into a channel group. Port priority will decide which 8 ports will be the active ports in the etherchannel.

*Administrative key* defines the capabilities of a port to aggregate with other ports, based on the port's physical characteristics.

Sample Configuration:
```
SW1# interface range GigabitEthernet0/1-2
SW1# channel-group 1 mode active
SW1# exit
SW1# interface port-channel 1
SW1# switchport trunk encapsulation dot1q
SW1# switchport mode trunk
```

A successful Layer 2 EtherChannel will show SU with the command `show etherchannel summary`. An unsuccessful layer 2 will show SD.
