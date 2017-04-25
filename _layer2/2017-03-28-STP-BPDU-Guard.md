---
layout: post
title: Spanning Tree BPDU Guard
category: Spanning Tree
tag: knowledge
date: 2017-03-28 15:40:45
---
BPDU Guard is a STP PortFast safety enhancement. It works by disabling a port any time the interface hears a BPDU. PortFast by itself will not do that, so if you have PortFast enabled on an interface, and an end user plugs a switch into that link, all kinds of events can happen (including the plugged in switch becoming the Root Bridge!). BPDU Guard ensures that unauthorized switches cannot be plugged into the network. A sample configuration is below.
```
interface gig0/1
  spanning-tree bpduguard enable

errdisable recovery cause bpduguard
errdisable recovery interval 120
```

The errdisable section enables the port after 120 seconds, in case the port is placed into err disabled state to due BPDU Guard.

Optionally, you can set BPDU Guard as the default configuration on all interfaces with the following global commands:
```
spanning-tree portfast bpduguard default
spanning-tree portfast default
```