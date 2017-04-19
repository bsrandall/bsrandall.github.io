---
layout: post
title: Policy Routing Order of Operation
category: General Routing
tag: knowledge
date: 2017-04-09 16:40:45
---
A route-map can have multiple set operations on a single match clause. The list below shows the order of operations, regardless of the sequence number we use or the order we input them.
- `set ip next-hop verify-availability track` - first when used with object tracking
- `set ip next-hop` - alone or with the CDP (but without default) version of `verify-availability`
- `set ip next-hop recursive`
- set interface
- Route table
- set ip default next-hop
- set default interface


