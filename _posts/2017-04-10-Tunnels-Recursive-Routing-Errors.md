---
layout: post
title: Tunnels and Recursive Routing Errors
category: General Routing
tag: knowledge
date: 2017-04-10 15:40:45
---
A recursive routing error occurs when a lookup for prefix X points to prefix Y, and a lookup for prefix Y points to prefix X. This happens with tunnels when the router has learned the destination IP address for the tunnel interface through the tunnel itself. What usually triggers it is enabling the IGP on the tunnel interface. Let’s say the tunnel destination is the loopback of the far end device, and the tunnel IP address is 192.168.13.1. Let there be a router between the two tunnel devices. Normally, the routing table will have a route to reach the loopback via the router in the middle. But once the IGP starts advertising the Tunnel routes, the route for the loopback will be the Tunnel IP address. The route for the Tunnel IP address will be the loopback. This is where our recursion exists.

The easiest solution is to not advertise the tunnel destination interface in the IGP. Either don’t advertise it or use route filtering.

The other options to solve are:
- Ensure the administrative distance of the tunnel destination IP address through the tunnel is higher than what you have in the routing table now
- Ensure the metric to the tunnel destination IP address through the tunnel is worse than what you have in the routing table now.

