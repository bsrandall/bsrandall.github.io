---
layout: post
title: RIP General
category: RIP
tag: knowledge
date: 2017-04-18 17:54:45
---
RIP exchanges UDP encapsulated packets over UDP port 520. RIP has two message types:
- **Request messages** are used to ask neighboring routers to send an update
- **Response message** carries the actual update

When a RIP router process starts, it broadcasts a Request message out *each* RIP-enabled interface. The begins the state machine with neighbors receiving a RIP request and responding with a RIP Response.

When the requesting router receives the Response message, it processes the enclosed information and responds in one of 3 ways, depending on the information in the RIP Response.
1. If a route in the Response is new, it is entered into the route table along with the address of the advertising router.
2. If there is a route for a network that RIP has already entered into the table and the new route has a lower metric (hop count), then the new route will replace the old route.
3. If there is a route for a network that RIP has already entered into the table and the new route has a higher hop count and the update was originated by the recorded next-hop router, the router will be marked as unreachable for a specified holddown period. If the same neighbor is still advertising the higher hop count at the end of the holddown timer, the routing table is updated with the new metric.

RIP does not store information received in a Topology table, nor do routers have a picture of the entire topology. They receive routes in Response messages, process the information in those messages, and then move on. The RIP Response messages contain that router’s full routing table, with the exception of routes that are stressed by the split-horizon rule.

Route Summarization means there are no routes for child addresses in the RIP routing table, reducing the size of the table and allowing the router to handle more routes. Summary IP address functions more efficiently than multiple individual advertised IP routes for the following reasons:
- The summarized routes in the Rip database are processed first
- Any associated child routes that are included in a summarized route are skipped as RIP looks through the routing database, reducing the processing time required.

If auto-summary is enabled, as soon as RIP determines a summary address is required in the RIP database, a summary entry is created in the RIP routing database. As long as there are child routes for a summary address, the address remains in the routing database.

RIPv2 route summarization requires that the lowest metric of an aggregated entry, or the lowest metric of all child routes, be advertised.

**show ip protocols** command will verify which routes are summarized for an interface.

 