---
layout: post
title: RIPv2 General
category: RIP
tag: knowledge
date: 2017-04-19 17:56:45
---
RIPv2 is defined in RFC 1723. It is not a new protocol, but rather just RIPv1 with some extensions bringing it more up to date with modern routing environments. The improvements include:
- subnet masks carried with each route entry
- authentication of routing updates
- next-hop addresses carried with each route entry
- external route tags
- multicast route updates

Operation of RIPv2 is similar to RIPv1, and all the timer mechanisms remain the same. One difference is that updates are sent to the multicast address 224.0.0.9 instead of the broadcast address 255.255.255.255 that RIPv1 used.

![RIPv2 Message Format][1]

The RIPv2 message format is similar to RIPv1.

**Command** is set to 1 for a request message or 2 for a response message.

**Version** will be 2 for RIPv2. Note that RIPv2 will process valid RIPv1 messages.

**Address Family Identifier** is set to 2 for IPv4. The only exception is a request for a router’s full routing table, in which case it will be 0.

**Route tag** provides a field for tagging external routes or routes that have been distributed into the RIPv2 process. One possible use is to carry the AS number of of routes that have been imported into RIP. This might be needed in case the information is carried across the RIP domain and then shared back with the external routing protocol in another location.

**IP Address** is the IPv4 address of the destination of the route. It may be a major network address, a subnet, or a host.

**Subnet Mask** is a 32 bit mask that identifies the host and network portions of the IPv4 address.

**Next Hop** identifies a better next-hop address, if one exists, than the address of the advertising router. It will be populated if there is another router on the same subnet that is closer to the destination than the advertising router. If the field is set to 0.0.0.0, then the advertising router is the best next-hop address.

**Metric** is the hop count, between 1 and 16.

As RIPv2 is a classless routing protocol, when it goes to look up a destination in the routing table, it does not pay attention to the class of the destination address. Instead, it performs a bit-by-bit best match between the destination address and all of its known routes.

One interesting note in regards to all classless routing protocols - Cisco IOS rejects an attempt to configure an all-zeroes subnet. To override this enter the global configuration command **ip subnet-zero**


[1]:	/assets/ripv2-message-format.png