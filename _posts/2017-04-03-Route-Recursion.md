---
layout: post
title: Route Recursion
category: General Routing
tag: knowledge
date: 2017-04-03 15:40:45
---
Every time a router has to do a router lookup, a recursive lookup will be performed, unless the destination is directly connected. When a route lists an IP address as the next hop, unless that next hop is directly connected the router must find the path to that route. It may have to work through multiple recursions in order to eventually find the correct interface to route out of.

When a particular interface goes down, all routes depending on that interface are removed from the RIB. One important thing to remember here is that the route is only removed if the next hop IP address is not reachable - if there is a secondary path via another interface, then that route will remain valid. However, if you use the interface as the destination for the static route, then the route will fail.