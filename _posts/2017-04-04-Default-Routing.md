---
layout: post
title: Default Routing
category: General Routing
tag: knowledge
---
Because of route recursion and the need for Layer 2 lookups on multipoint interfaces, default routing should be set up in one of two ways:
- to a next hop IP address if the interface is multipoint or point-to-point
- to an interface ONLY if the interface is point-to-point.

One issue with default routes is that you lose a lot of the routing detail. One way this shows itself is the fact that sites with default routes will have no idea if the end destination network is available. Another issue with the loss of detail has to do with having multiple default routes. With only having default routes, there is no routing details to show which is the better path to reach the end destination.