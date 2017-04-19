---
layout: post
title: On Demand Routing
category: General Routing
tag: knowledge
date: 2017-04-10 16:40:45
---
ODR allows you to easily install IP stub networks where the hubs dynamically maintain routes to the stub networks. With ODR, this installation is accomplished without requiring the configuration of an IP routing protocol on the stubs.

A stub router supporting ODR advertises IP prefixes corresponding to the IP networks configured on all directly connected interfaces. If the network has multiple logical IP networks configured, only the primary IP network is advertised through ODR. ODR is able to pass VLSM information since it sends prefixes. Once ODR is enabled on a hub router, the hub router begins installing sub network routes in the IP forwarding table. The hub router can also be configured to distribute these routes into any configured dynamic IP routing protocols.

ODR uses Cisco Discovery Protocol (CDP) to carry minimal routing information between the hub and stub routers. The hub router provides default route information to the stubs routers, thereby eliminating the need to configure a default route on each stub router.

To disallow a particular interface from sending its prefix, disable CDP on that interface.

To enable ODR, simply issue the following.
```
`R1(conf)# router odr
```
`
