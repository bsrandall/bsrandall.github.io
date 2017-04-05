---
layout: post
title: Floating Static Routes
category: General Routing
tag: knowledge
---
A Floating Static route is a static route whose administrative distance has been increased in order to make the route function as a backup route. The global command would look like this:
```
ip route 192.168.23.0 255.255.255.0 192.168.13.3 121
```
This would set the administrative distance to this route as 121, which would make it’s AD higher than a RIP, OSPF, or EIGRP learned route.