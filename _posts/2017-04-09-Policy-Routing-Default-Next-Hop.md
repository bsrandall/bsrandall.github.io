---
layout: post
title: Policy Routing using next-hop, default, and recursive
category: General Routing
tag: knowledge
date: 2017-04-09 15:40:45
---
When using policy routing and the `ip next-hop` set option in a route map, you can optionally use the *default* keyword. The difference is simple.

When you do not use the default keyword, routing utilizes PBR first and consults the routing table if there is no match or non reachability. If you use the default keyword, then routing uses the routing table first and if no route can be found then attempts to use the Policy Based Routing process.

Both the `set ip next-hop` and the `set ip default next-hop` commands require that the next-hop be found on a directly-connected subnet, otherwise PBR will fail and normal forwarding will be used. However, we can use `set ip next-hop recursive` to use an address off a subnet that *is not* directly connected.