---
layout: post
title: IP in IP Tunnels
category: General Routing
tag: knowledge
date: 2017-04-10 14:40:45
---
With GRE Tunnels, IPv4 (or other protocols) are encapsulated in GRE packets. With IP in IP tunnels, IPv6 or IPv4 packets are encapsulated inside IPv4 or IPv6 packets. In IOS, three combinations are possible:
- IPv4 in IPv4 (ipip)
- IPv6 in IPv6 (ipv6)
- IPv6 in IPv4 (ipv6ip)

So there is no combination for IPv4 in IPv6. GRE adds the extra capability of encapsulating other protocols other than IP. GRE also allows you to enforce packet sequencing, add an additional checksum, and to specify a tunnel key. Of course, all of these features come at the cost of additional overhead.

IP in IP tunnels are created the same way as GRE tunnels, you just select a different tunnel mode.