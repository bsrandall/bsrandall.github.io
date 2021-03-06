---
layout: post
title: Egress Interface vs Next Hop Static Routing
category: General Routing
tag: knowledge
---
There are some difference on router behavior depending on if you use a Next Hop IP address or an Egress Interface as the destination in your static route. This article will describe some of this e differences.

If you use the Next Hop IP address, the router will have to find the interface leading towards the destination address before the route will be installed in the forwarding table. When the router finds the egress interface it will then check to see if the interface is point-to-point or multipoint. If it is multipoint, then the router will need the MAC address of the Next Hop address. If it doesn’t have it, then it will need to use ARP.

If you use the outgoing interface the router does not have to do the recursive lookup to find the correct outgoing interface. But the problem is the router doesn’t know which layer 2 neighbor routers exist on that link. So the only choice the router has is to ARP for the final destination address (rather than next hop as above). Where this can get outrageous is that the router will need to have MAC addresses resolved for *all hosts* in the subnet and you will need proxy ARP enabled on all routers in the segment. The example gets even more outrageous if you define a default route that points to a multipoint interface. So it should be clear this should only be used on point-to-point interfaces.

Point-to-point interfaces do not have the same problem as the router knows there is only one host to receive the traffic on the other end. In other words, recursion will not be required nor will Layer 2 resolution be required.
