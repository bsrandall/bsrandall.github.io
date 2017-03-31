---
layout: post
title: Protected Port (PVLAN)
category: Layer 2
tag: knowledge
---
The protected port, also known as PVLAN edge, is a security feature used to prevent traffic from being directly exchanged at Layer 2 between two or more hosts that are within the same VLAN. Protected ports only have local switch significance. A protected port does not forward any traffic (unicast, multicast, or broadcast) to any other protected port in the same switch. If you need to pass traffic between protected ports, the only possible way is through a L3 device.

By default, all switch ports are unprotected. The configuration is as simple as below:
```
SW1(config)# interface gig0/1
SW1(config-if)# switchport protected
```
