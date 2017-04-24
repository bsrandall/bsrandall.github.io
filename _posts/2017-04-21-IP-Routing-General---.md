layout: post
title: IP Routing General
category: General Routing
tag: knowledge
date: 2017-04-21 19:56:45
---
Static routes that point to an interface are advertised via RIP (and EIGRP) regardless of whether **redistribute static** router configuration commands are specified for those routing protocols. This is because these routes are considered “connected” routes and lose their static nature. However, if there is no **network** command defined for that interface, then the default route will not be advertised unless a **redistribute static** command is configured.

There are 3 ways (outside of dynamic routing protocols) to generate a default route.
- ip default-gateway
- ip default-network
- ip route 0.0.0.0 0.0.0.0

**ip default-gateway** is used to define a default gateway when ip routing *is not* enabled on the device. This can be handy to transfer a Cisco software image to a device when the device is in boot mode.

**ip default-network** is used to define a default gateway when ip routing *is* enabled on the router. Default routes configured this way are propagated differently depending on which routing protocol is propagating the default route. For EIGRP to propagate the default route, the network specified by **ip default-network** must be known to EIGRP. The network must be an EIGRP derived network in the routing table, or the static route used to generate the route to the network must be redistributed into EIGRP.

RIP advertises a route to network 0.0.0.0 if a gateway of last resort is configured using the **ip default-network** command.

When using **ip route 0.0.0.0 0.0.0.0** to create a default route, EIGRP will propagate a route to network 0.0.0.0, but the static route must be redistributed into the routing protocol. With RIP, on most versions of IOS the default route created by **ip route 0.0.0.0 0.0.0.0** is automatically advertised by RIP. Not only are these routes not automatically propagated by OSPF, you cannot redistribute a default route into OSPF - you must use the **default-information originate** command.

