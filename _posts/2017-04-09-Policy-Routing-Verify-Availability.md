---
layout: post
title: PBR - verify-availability
category: General Routing
tag: knowledge
date: 2017-04-09 14:40:45
---
Within the route-map statement, there is an option when using `ip next-hop` of `verify-availability`. This article will describe what it does and the two flavors of utilization.

If used solely by itself, `verify-availabilty` uses CDP to establish that the next-hop IP address is reachable. If the IP address used is in the CDP neighbor table, then the next-hop is deemed accessible, otherwise it is not.

`verify-availability` can be extended to also use a tracking object. Here is an example of that configuration.
```
`R2(config)#route-map PBR permit 10
R2(config-route-map)#match ip address HTTP-SERVER
R2(config-route-map)#set ip next-hop verify-availability 192.168.24.4 1 track 1
```
`
If using either of these methods to implement `verify-reachability`, if the next-hop IP address is not reachable then routing is not performed based on the policy but is routed according to the the routing table.

We can use a combination of commands to route a different way if our `verify-reachability` fails.
```
`R1(config)# route-map RM1
R1(config-route-map)# match ip address AL1
R1(config-route-map)# set ip next-hop 155.1.0.5
R1(config-route-map)# set ip next-hop verify reachability
R1(config-route-map)# set ip default next-hop 155.1.13.3
```
`In this example, if we match to AL1 AND 155.1.0.5 is reachable (CDP check), then we route to 155.1.0.5. However if we match AL1 and 155.1.0.5 is not in the CDP neighbor table, then we route to 155.1.13.3.