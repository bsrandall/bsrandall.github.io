---
layout: post
title: EtherChannel Layer 3
category: EtherChannel
tag: knowledge
---

To configure Layer 3 EtherChannels, you have to ensure that the ports that are part of the EtherChannel are first set to `no switchport` before adding them to the channel-group. An example LACP config follows:

```
 interface port-channel 1
  no switchport
  ip address 10.0.0.1 255.255.255.0

interface GigabitEthernet0/1
  no ip address
  no switchport
  channel-group 1 mode active
```