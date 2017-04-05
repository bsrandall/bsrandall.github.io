---
layout: post
title: Static Routing
category: General Routing
tag: knowledge
---
Static routes do have some advantages over dynamic routing:
- static routes are not advertised over the network by default, resulting in better security
- static routes use less bandwidth than dynamic routing protocols, as there is no exchange of routes
- no CPU cycles are used to calculate and communicate routes

Static routes have some disadvantages as well:
- initial configuration and maintenance is time consuming
- does not scale well
- requires complete knowledge of the whole network for proper implementation.
- can interfere with the use of backup routes

With backup routes, if the outage occurs downstream in the network, a router with a static route to a destination will never utilize the backup route, because it still sees a path to the destination from the backup route. To get around this, use an outbound interface as well as the destination IP in the static route as in `R1(config)# ip route 10.0.0.0 255.255.255.0 FastEthernet0/1 192.168.10.1`. The other option is to of course use a dynamic routing protocol and then the route will be removed 

To set up a static route, use the following syntax:
```
ip route 192.168.18.0 255.255.255.0 192.168.17.1
```
This would route any traffic destined for 192.168.18.0/24 to 192.168.17.1.

To set up a default route, use the following:
```
ip route 0.0.0.0 0.0.0.0 192.168.17.1
```
You could also specify an interface, but the better way is to use an IP address so no lookups are required.
